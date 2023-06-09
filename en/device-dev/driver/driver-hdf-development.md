# Driver Development


## Driver Model

The Hardware Driver Foundation (HDF) is designed based on a modular driver model to enable refined driver management and streamline driver development and deployment. The HDF allows the same type of device drivers to be placed in a host. The host manages the start and loading of a group of devices. You can deploy dependent drivers to the same host, and deploy independent drivers to different hosts.

The figure below shows the HDF driver model. A device refers to a physical device. A DeviceNode is a component of a device. A device has at least one DeviceNode. Each DeviceNode can publish a device service. Each DevicdNode has a unique driver to interact with the hardware.

  **Figure 1** HDF driver model

  ![](figures/hdf-driver-model.png)


## How to Develop

The HDF-based driver development involves driver implementation, write of the driver compilation script, and driver configuration. The procedure is as follows:

1. Implement a driver.

   Write the driver code and register the driver entry with the HDF.

   - Write the driver service code. <br>The following is an example:
     
      ```c
      #include "hdf_device_desc.h"          // Header file that defines the driver development APIs provided by the HDF.
      #include "hdf_log.h"                  // Header file that defines the log APIs provided by the HDF.
      
      #define HDF_LOG_TAG "sample_driver"   // Tag contained in logs. If no tag is not specified, the default HDF_TAG is used.
      
      // Bind the service APIs provided by the driver to the HDF.
      int32_t HdfSampleDriverBind(struct HdfDeviceObject *deviceObject)
      {
          HDF_LOGD("Sample driver bind success");
          return HDF_SUCCESS;
      }
      
      // Initialize the driver service.
      int32_t HdfSampleDriverInit(struct HdfDeviceObject *deviceObject)
      {
          HDF_LOGD("Sample driver Init success");
          return HDF_SUCCESS;
      }
      
      // Release the driver resources.
      void HdfSampleDriverRelease(struct HdfDeviceObject *deviceObject)
      {
          HDF_LOGD("Sample driver release success");
          return;
      }
      ```
   - Register the driver entry with the HDF.
     
      ```c
      // Define a driver entry object. It must be a global variable of the HdfDriverEntry type (defined in hdf_device_desc.h). 
      struct HdfDriverEntry g_sampleDriverEntry = {
          .moduleVersion = 1,
          .moduleName = "sample_driver",
          .Bind = HdfSampleDriverBind,
          .Init = HdfSampleDriverInit,
          .Release = HdfSampleDriverRelease,
      };
      
      // Call HDF_INIT to register the driver entry with the HDF. When loading the driver, the HDF calls Bind() and then Init(). If Init() fails to be called, the HDF will call Release() to release driver resources and exit the driver model.
      HDF_INIT(g_sampleDriverEntry);
      ```

2. Write the driver compilation script.

   - LiteOS

     Modify **makefile** and **BUILD.gn** files.

     - **Makefile**:

       Use the **makefile** template provided by the HDF to compile the driver code.

       
       ```c
       include $(LITEOSTOPDIR)/../../drivers/hdf_core/adapter/khdf/liteos/lite.mk # (Mandatory) Import the HDF predefined content.
       MODULE_NAME :=        # File to be generated.
       LOCAL_INCLUDE: =      # Directory of the driver header files.
       LOCAL_SRCS : =        # Source code files of the driver.
       LOCAL_CFLAGS : =      # Custom build options.
       include $(HDF_DRIVER) # Import the makefile template to complete the build.
       ```

       Add the path of the generated file to **hdf_lite.mk** in the **drivers/hdf_core/adapter/khdf/liteos** directory to link the file to the kernel image. <br>The following is an example:

       
       ```c
       LITEOS_BASELIB += -lxxx # Static library generated by the link.
       LIB_SUBDIRS    +=         # Directory in which makefile is located.
       ```

     - **BUILD.gn**:

       Add **BUILD.gn**. The content of **BUILD.gn** is as follows:

       
       ```c
       import("//build/lite/config/component/lite_component.gni")
       import("//drivers/hdf_core/adapter/khdf/liteos/hdf.gni")
       module_switch = defined(LOSCFG_DRIVERS_HDF_xxx)
       module_name = "xxx"
       hdf_driver(module_name) {
           sources = [
               "xxx/xxx/xxx.c",           # Source code to compile.
           ]
           public_configs = [ ":public" ] # Head file configuration of the dependencies.
       }
       config("public") {                 # Define the head file configuration of the dependencies.
           include_dirs = [
               "xxx/xxx/xxx",             # Directory of dependency header files.
           ]
       }
       ```

       Add the **BUILD.gn** directory to **/drivers/hdf_core/adapter/khdf/liteos/BUILD.gn**.

       
       ```c
       group("liteos") {
           public_deps = [ ":$module_name" ]
               deps = [
                   "xxx/xxx", # Directory where the BUILD.gn of the driver is located. It is a relative path to /drivers/hdf_core/adapter/khdf/liteos.
               ]
       }
       ```
   - Linux

     To define the driver control macro, add the **Kconfig** file to the driver directory **xxx** and add the path of the **Kconfig** file to **drivers/hdf_core/adapter/khdf/linux/Kconfig**.

     
     ```c
     source "drivers/hdf/khdf/xxx/Kconfig" # Kernel directory to which the HDF module is soft linked.
     ```

     Add the driver directory to **drivers/hdf_core/adapter/khdf/linux/Makefile**.

     
     ```c
     obj-$(CONFIG_DRIVERS_HDF)  += xxx/
     ```

     Add a **Makefile** to the driver directory **xxx** and add code compiling rules of the driver to the **Makefile** file.

     
     ```c
     obj-y  += xxx.o
     ```

3. Configure the driver.

   The HDF Configuration Source (HCS) contains the source code of HDF configuration. For details about the HCS, see [Configuration Management](../driver/driver-hdf-manage.md).

   The driver configuration consists of the driver device description defined by the HDF and the private driver configuration.

   - (Mandatory) Set driver device information.

     The HDF loads a driver based on the driver device description defined by the HDF. Therefore, the driver device description must be added to the **device_info.hcs** file defined by the HDF. <br>The following is an example:

     
      ```
      root {
          device_info {
              match_attr = "hdf_manager";
              template host {       // Host template. If a node (for example, sample_host) uses the default values in this template, the node fields can be omitted.
                  hostName = "";
                  priority = 100;
                  uid = "";         // User ID (UID) of the user-mode process. It is left empty by default. If you do not set the value, this parameter will be set to the value of hostName, which indicates a common user.
                  gid = "";         // Group ID (GID) of the user-mode process. It is left empty by default. If you do not set the value, this parameter will be set to the value of hostName, which indicates a common user group.
                  caps = [""]];     // Linux capabilities of the user-mode process. It is left empty by default. Set this parameter based on service requirements.
                  template device {
                      template deviceNode {
                          policy = 0;
                          priority = 100;
                          preload = 0;
                          permission = 0664;
                          moduleName = "";
                          serviceName = "";
                          deviceMatchAttr = "";
                      }
                  }
              }
              sample_host :: host{
                  hostName = "host0";    // Host name. The host node is used as a container to hold a type of drivers.
                  priority = 100;        // Host startup priority (0-200). A smaller value indicates a higher priority. The default value 100 is recommended. The hosts with the same priority start based on the time when the priority was configured. The host configured first starts first.
                  caps = ["DAC_OVERRIDE", "DAC_READ_SEARCH"];   // Linux capabilities of a user-mode process.
                  device_sample :: device {        // Sample device node.
                      device0 :: deviceNode {      // DeviceNode of the sample driver.
                          policy = 1;              // Policy for publishing the driver service. For details, see Driver Service Management.
                          priority = 100;          // Driver startup priority (0-200). A smaller value indicates a higher priority. The default value 100 is recommended. The drivers with the same priority start based on the time when the priority was configured. The driver configured first starts first.
                          preload = 0;             // The value 0 means to load the driver by default during the startup of the system.
                          permission = 0664;       // Permission for the DeviceNode created.
                          moduleName = "sample_driver";      // Driver name. The value must be the same as that of moduleName in the HdfDriverEntry structure.
                          serviceName = "sample_service";    // Name of the service published by the driver. The service name must be unique.
                          deviceMatchAttr = "sample_config"; // Keyword for matching the private data of the driver. The value must be the same as that of match_attr in the private data configuration table of the driver.
                      }
                  }
              }
          }
      }
      ```
     
      > ![icon-note.gif](public_sys-resources/icon-note.gif) **NOTE**<br/>
      >
      > - **uid**, **gid**, and **caps** are startup parameters for user-mode drivers only.
      >
      > - According to the principle of least privilege for processes, **uid** and **gid** do not need to be configured for service modules. In the preceding example, **uid** and **gid** are left empty (granted with the common user rights) for sample_host.
      >
      > - If you need to set **uid** and **gid** to **system** or **root** due to service requirements, contact security experts for review.
      >
      > - The process UIDs are configured in **base/startup/init/services/etc/passwd**, and the process GIDs are configured in **base/startup/init/services/etc/group**. For details, see [Adding a System Service User Group]( https://gitee.com/openharmony/startup_init_lite/wikis).
      >
      > - The **caps** value is in the caps = ["xxx"] format. To configure **CAP_DAC_OVERRIDE**, set this parameter to **caps = ["DAC_OVERRIDE"]**. Do not set it to **caps = ["CAP_DAC_OVERRIDE"]**.
      >
      > - **preload** specifies the driver loading policy. For details, see [Driver Loading](../driver/driver-hdf-load.md).


   - (Optional) Set driver private information.

     If the driver has private configuration, add a driver configuration file to set default driver configuration. When loading the driver, the HDF obtains and saves the driver private information in **property** of **HdfDeviceObject**, and passes the information to the driver using **Bind()** and **Init()** (see step 1). <br>The following is an example of the driver configuration:

     
      ```
      root {
          SampleDriverConfig {
              sample_version = 1;
              sample_bus = "I2C_0";
              match_attr = "sample_config"; // The value must be the same as that of deviceMatchAttr in device_info.hcs.
          }
      }
      ```

      Add the configuration file to the **hdf.hcs** file. <br>The following is an example:

     
      ```
      #include "device_info/device_info.hcs"
      #include "sample/sample_config.hcs"
      ```
