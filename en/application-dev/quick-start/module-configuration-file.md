# module.json5 Configuration File


This document gives an overview of the **module.json5** configuration file. To start with, let's go through an example of what this file contains.

```json
{
  "module": {
    "name": "entry",
    "type": "entry",
    "description": "$string:module_desc",
    "mainElement": "EntryAbility",
    "deviceTypes": [
      "default",
      "tablet"
    ],
    "deliveryWithInstall": true,
    "installationFree": false,
    "pages": "$profile:main_pages",
    "virtualMachine": "ark",
    "metadata": [
      {
        "name": "string",
        "value": "string",
        "resource": "$profile:distrofilter_config"
      }
    ],
    "abilities": [
      {
        "name": "EntryAbility",
        "srcEntrance": "./ets/entryability/EntryAbility.ts",
        "description": "$string:EntryAbility_desc",
        "icon": "$media:icon",
        "label": "$string:EntryAbility_label",
        "startWindowIcon": "$media:icon",
        "startWindowBackground": "$color:start_window_background",
        "visible": true,
        "skills": [
          {
            "entities": [
              "entity.system.home"
            ],
            "actions": [
              "action.system.home"
            ]
          }
        ]
      }
    ],
    "requestPermissions": [
      {
        "name": "ohos.abilitydemo.permission.PROVIDER",
        "reason": "$string:reason",
        "usedScene": {
          "abilities": [
            "FormAbility"
          ],
          "when": "inuse"
        }
      }
    ]
  }
}
```


As shown above, the **module.json5** file contains several tags.


  **Table 1** Tags in the module.json5 file

| Name| Description| Data Type| Initial Value Allowed|
| -------- | -------- | -------- | -------- |
| name | Name of the module. The value is a string with a maximum of 31 bytes and must be unique in the entire application.| String| No|
| type | Type of the module. The value can be **entry** or **feature**.<br>- **entry**: main module of the application.<br>- **feature**: dynamic feature module of the application.| String| No|
| srcEntrance | Code path corresponding to the module. The value is a string with a maximum of 127 bytes.| String| Yes (initial value: left empty)|
| description | Description of the module. The value is a string with a maximum of 255 bytes or a string resource index. | String| Yes (initial value: left empty)|
| process | Process name of the current module. The value is a string with a maximum of 31 bytes. If **process** is configured under **HAP**, all UIAbility, DataShareExtensionAbility, and ServiceExtensionAbility components of the application run in the specified process.<br>**NOTE**<br>This tag applies only to system applications and does not take effect for third-party applications.| String| Yes (initial value: value of **bundleName** under **app** in the **app.json5** file)|
| mainElement | Name of the entry UIAbility or ExtensionAbility of the module. The value contains a maximum of 255 bytes.| String| Yes (initial value: left empty)|
| [deviceTypes](#devicetypes) | Type of the device on which the module can run.| String array| No (can be left empty)|
| deliveryWithInstall | Whether the HAP file of the module will be installed when the user installs the application.<br>- **true**: The HAP file will be installed when the user installs the application.<br>- **false**: The HAP file will not be installed when the user installs the application.| Boolean| No|
| installationFree | Whether the module supports the installation-free feature.<br>- **true**: The module supports the installation-free feature and meets installation-free constraints.<br>- **false**: The module does not support the installation-free feature.<br>**NOTE**<br>- If this tag is set to **true** for an entry-type module, it must also be set to **true** for feature-type modules of the same application.<br>- If this tag is set to **false** for an entry-type module, it can be set to **true** or **false** for feature-type modules of the same application based on service requirements.| Boolean| No|
| virtualMachine | Type of the target virtual machine (VM) where the module runs. It is used for cloud distribution, such as distribution by the application market and distribution center.<br>If the target VM type is ArkTS engine, the value is **ark**+*version number*. | String| Yes (initial value: automatically inserted when DevEco Studio builds the HAP file)|
| uiSyntax (deprecated)| Syntax type of the JS component defined by the module syntax. This tag is deprecated since API version 9.<br>- **"hml"**: The JS component is developed using HML, CSS, or JS.<br>- **"ets"**: The JS component is developed using ArkTS. | String| Yes (initial value: **"hml"**)|
| [pages](#pages)| Profile that represents information about each page in the JS component. The value can contain a maximum of 255 bytes.| String| No in the UIAbility scenario|
| [metadata](#metadata)| Custom metadata of the module. The setting is valid only for the current module, UIAbility, or ExtensionAbility.| Object array| Yes (initial value: left empty)|
| [abilities](#abilities) | UIAbility configuration of the module, which is valid only for the current UIAbility component.| Object| Yes (initial value: left empty)|
| [extensionAbilities](#extensionabilities) | ExtensionAbility configuration of the module, which is valid only for the current ExtensionAbility component.| Object| Yes (initial value: left empty)|
| [requestPermissions](#requestpermissions) | A set of permissions that the application needs to request from the system for running correctly.| Object| Yes (initial value: left empty)|
| [testRunner](#testrunner) | Test runner configuration of the module.| Object| Yes (initial value: left empty)|


## deviceTypes

  **Table 2** deviceTypes

| Device Type| Value| Description|
| -------- | -------- | -------- |
| Tablet| tablet | - |
| Smart TV| tv | - |
| Smart watch| wearable | Watch that provides call features.|
| Head unit| car | - |
| Default device| default | OpenHarmony device that provides full access to system capabilities.|

Example of the **deviceTypes** structure:


```json
{
  "module": {
    "name": "myHapName",
    "type": "feature",
    "deviceTypes" : [
       "tablet"
    ]
  }
}
```


## pages

The **pages** tag is a profile that represents information about specified pages.


```json
{
  "module": {
    // ...
    "pages": "$profile:main_pages", // Configured through the resource file in the profile
  }
}
```

Define the **main_pages.json** file under **resources/base/profile** in the development view. The base name of the file (**main_pages** in this example) can be customized, but must be consistent with the information specified by the **pages** tag. The file lists the page information of the current application.


```json
{
  "src": [
    "pages/index/mainPage",
    "pages/second/payment",
    "pages/third/shopping_cart",
    "pages/four/owner"
  ]
}
```


## metadata

The **metadata** tag represents the custom metadata of the HAP file. The tag value is an array and contains three subtags: **name**, **value**, and **resource**.

  **Table 3** metadata

| Name| Description| Data Type| Initial Value Allowed|
| -------- | -------- | -------- | -------- |
| name | Name of the data item. The value is a string with a maximum of 255 bytes.| String| Yes (initial value: left empty)|
| value | Value of the data item. The value is a string with a maximum of 255 bytes.| String| Yes (initial value: left empty)|
| resource | Custom data format. The value is a resource index. It contains a maximum of 255 bytes. | String| Yes (initial value: left empty)|


```json
{
  "module": {
    "metadata": [{
      "name": "module_metadata",
      "value": "a test demo for module metadata",
      "resource": "$profile:shortcuts_config",
    }],

    "abilities": [{
      "metadata": [{
        "name": "ability_metadata",
        "value": "a test demo for ability",
        "resource": "$profile:config_file"
      },
      {
        "name": "ability_metadata_2",
        "value": "a string test",
        "resource": "$profile:config_file"
      }],
    }],

    "extensionAbilities": [{
      "metadata": [{
        "name": "extensionAbility_metadata",
        "value": "a test for extensionAbility",
        "resource": "$profile:config_file"
      },
      {
        "name": "extensionAbility_metadata_2",
        "value": "a string test",
        "resource": "$profile:config_file"
      }],
    }]
  }
}
```


## abilities

The **abilities** tag describes the UIAbility configuration of the component, which is valid only for the current UIAbility component. The tag value is an array.

  **Table 4** abilities

| Name| Description| Data Type| Initial Value Allowed|
| -------- | -------- | -------- | -------- |
| name | Name of the UIAbility component, which must be unique in the entire application. The value is a string with a maximum of 127 bytes.| String| No|
| srcEntrance | Code path of the entry UIAbility component. The value is a string with a maximum of 127 bytes.| String| No|
| [launchType](../application-models/uiability-launch-type.md) | Launch type of the UIAbility component. The options are as follows:<br>- **standard**: A new UIAbility instance is created each time the UIAbility component is started.<br>- **singleton**: A new UIAbility instance is created only when the UIAbility component is started for the first time.<br>- **specified**: You can determine whether to create a new UIAbility instance when the application is running.| String| Yes (initial value: **"singleton"**)|
| description | Description of the UIAbility component. The value is a string with a maximum of 255 bytes or a resource index to the description in multiple languages. | String| Yes (initial value: left empty)|
| icon | Icon of the UIAbility component. The value is an icon resource index.<br/>If **UIAbility** is set to **MainElement** of the current module, this attribute is mandatory. | String| Yes (initial value: left empty) |
| label | Name of the UIAbility component displayed to users. The value is a string resource index.<br>If **UIAbility** is set to **MainElement** of the current module, this attribute is mandatory and its value must be unique in the application. | String| No|
| permissions | Permissions required for another application to access the UIAbility component.<br>The value is an array of permission names predefined by the system, generally in the reverse domain name notation. It contains a maximum of 255 bytes.| String array| Yes (initial value: left empty)|
| [metadata](#metadata)| Metadata information of the UIAbility component.| Object array| Yes (initial value: left empty)|
| visible | Whether the UIAbility component can be called by other applications.<br>- **true**: The UIAbility component can be called by other applications.<br>- **false**: The UIAbility component cannot be called by other applications.| Boolean| Yes (initial value: **false**)|
| continuable | Whether the UIAbility component can be [migrated](../application-models/hop-cross-device-migration.md).<br>- **true**: The UIAbility component can be migrated.<br>- **false**: The UIAbility component cannot be migrated.| Boolean| Yes (initial value: **false**)|
| [skills](#skills) | Feature set of [wants](../application-models/want-overview.md) that can be received by the current UIAbility or ExtensionAbility component.<br>Configuring rule:<br>- For HAPs of the entry type, you can configure multiple **skills** attributes with the entry capability for an OpenHarmony application. (A **skills** attribute with the entry capability is the one that has **action.system.home** and **entity.system.home** configured.)<br>- For HAPs of the feature type, you can configure **skills** attributes with the entry capability for an OpenHarmony application, but not for an OpenHarmony service.| Object array| Yes (initial value: left empty)|
| backgroundModes | Continuous tasks of the UIAbility component.<br>Continuous tasks are classified into the following types:<br>- **dataTransfer**: service for downloading, backing up, sharing, or transferring data from the network or peer devices.<br>- **audioPlayback**: audio playback service.<br>- **audioRecording**: audio recording service.<br>- **location**: location and navigation services.<br>- **bluetoothInteraction**: Bluetooth scanning, connection, and transmission services (wearables).<br>- **multiDeviceConnection**: multi-device interconnection service.<br>- **wifiInteraction**: Wi-Fi scanning, connection, and transmission services (as used in the Multi-screen Collaboration and clone features)<br>- **voip**: voice/video call and VoIP services.<br>- **taskKeeping**: computing service.| String array| Yes (initial value: left empty)|
| startWindowIcon | Index to the icon file of the UIAbility component startup page. Example: **$media:icon**.<br>The value is a string with a maximum of 255 bytes.| String| No|
| startWindowBackground | Index to the background color resource file of the UIAbility component startup page. Example: **$color:red**.<br>The value is a string with a maximum of 255 bytes.| String| No|
| removeMissionAfterTerminate | Whether to remove the relevant task from the task list after the UIAbility component is destroyed.<br>- **true**: Remove the relevant task from the task list after the UIAbility component is destroyed.<br>- **false**: Do not remove the relevant task from the task list after the UIAbility component is destroyed.| Boolean| Yes (initial value: **false**)|
| orientation | Orientation of the UIAbility component when it is started. The options are as follows:<br>- **unspecified**: automatically determined by the system.<br>- **landscape**: landscape mode.<br>- **portrait**: portrait mode.<br>- **landscape_inverted**: inverted landscape mode.<br>- **portrait_inverted**: inverted portrait mode.<br>- **auto_rotation**: determined by the sensor.<br>- **auto_rotation_landscape**: determined by the sensor in the horizontal direction, including landscape and inverted landscape modes.<br>- **auto_rotation_portrait**: determined by the sensor in the vertical direction, including portrait and inverted portrait modes.<br>- **auto_rotation_restricted**: determined by the sensor when the sensor switch is enabled.<br>- **auto_rotation_landscape_restricted**: determined by the sensor in the horizontal direction, including landscape and inverted landscape modes, when the sensor switch is enabled.<br>- **auto_rotation_portrait_restricted**: determined by the sensor in the vertical direction, including portrait and inverted portrait modes, when the sensor switch is enabled.<br>- **locked**: auto rotation disabled.| String| Yes (initial value: **"unspecified"**)|
| supportWindowMode | Window mode supported by the UIAbility component. The options are as follows:<br>- **fullscreen**: full-screen mode.<br>- **split**: split-screen mode.<br>- **floating**: floating window mode.| String array| Yes (initial value:<br>["fullscreen", "split", "floating"])|
| priority | Priority of the UIAbility component. This attribute applies only to system applications and does not take effect for third-party applications. In the case of [implicit query](../application-models/explicit-implicit-want-mappings.md), UIAbility components with a higher priority are at the higher place of the returned list. The value is an integer ranging from 0 to 10. The greater the value, the higher the priority.| Number| Yes (initial value: **0**)|
| maxWindowRatio | Maximum aspect ratio supported by the UIAbility component. The minimum value is 0.| Number| Yes (initial value: maximum aspect ratio supported by the platform)|
| minWindowRatio | Minimum aspect ratio supported by the UIAbility component. The minimum value is 0.| Number| Yes (initial value: minimum aspect ratio supported by the platform)|
| maxWindowWidth | Maximum window width supported by the UIAbility component, in vp. The minimum value is 0.| Number| Yes (initial value: maximum window width supported by the platform)|
| minWindowWidth | Minimum window width supported by the UIAbility component, in vp. The minimum value is 0.| Number| Yes (initial value: minimum window width supported by the platform)|
| maxWindowHeight | Maximum window height supported by the UIAbility component, in vp. The minimum value is 0.| Number| Yes (initial value: maximum window height supported by the platform)|
| minWindowHeight | Minimum window height supported by the UIAbility component, in vp. The minimum value is 0.| Number| Yes (initial value: minimum window height supported by the platform)|
| excludeFromMissions | Whether the UIAbility component is displayed in the recent task list.<br>- **true**: displayed in the recent task list.<br>- **false**: not displayed in the recent task list.<br>**NOTE**<br>This tag applies only to system applications and does not take effect for third-party applications.| Boolean| Yes (initial value: **false**)|

Example of the **abilities** structure:


```json
{
  "abilities": [{
    "name": "EntryAbility",
    "srcEntrance": "./ets/entryability/EntryAbility.ts",
    "launchType":"standard",
    "description": "$string:description_main_ability",
    "icon": "$media:icon",
    "label": "Login",
    "permissions": [],
    "metadata": [],
    "visible": true,
    "continuable": true,
    "skills": [{
      "actions": ["action.system.home"],
      "entities": ["entity.system.home"],
      "uris": []
    }],
    "backgroundModes": [
      "dataTransfer",
      "audioPlayback",
      "audioRecording",
      "location",
      "bluetoothInteraction",
      "multiDeviceConnection",
      "wifiInteraction",
      "voip",
      "taskKeeping"
    ],
    "startWindowIcon": "$media:icon",
    "startWindowBackground": "$color:red",
    "removeMissionAfterTerminate": true,
    "orientation": " ",
    "supportWindowMode": ["fullscreen", "split", "floating"],
    "maxWindowRatio": 3.5,
    "minWindowRatio": 0.5,
    "maxWindowWidth": 2560,
    "minWindowWidth": 1400,
    "maxWindowHeight": 300,
    "minWindowHeight": 200,
    "excludeFromMissions": false
  }]
}
```


## skills

The **skills** tag represents the feature set of [wants](../application-models/want-overview.md) that can be received by the UIAbility or ExtensionAbility component.

  **Table 5** skills

| Name| Description| Data Type| Initial Value Allowed|
| -------- | -------- | -------- | -------- |
| actions | [Actions](../application-models/actions-entities.md) of wants that can be received, which can be predefined or customized.| String array| Yes (initial value: left empty)|
| entities | [Entities](../application-models/actions-entities.md) of wants that can be received.| String array| Yes (initial value: left empty)|
|uris | URIs that match the wants.| Object array| Yes (initial value: left empty)|

  **Table 6** uris

| Name| Description| Data Type| Initial Value Allowed|
| -------- | -------- | -------- | -------- |
| scheme | Scheme of the URI, such as HTTP, HTTPS, file, and FTP.| String| Yes when only **type** is set in **uris** (initial value: left empty) |
| host | Host address of the URI. This attribute is valid only when **schema** is set. Common methods:<br>- domain name, for example, **example.com**.<br>- IP address, for example, **10.10.10.1**.| String| Yes (initial value: left empty)|
| port | Port number of the URI. For example, the default HTTP port number is 80, the default HTTPS port number is 443, and the default FTP port number is 21. This attribute is valid only when both **scheme** and **host** are set.| String| Yes (initial value: left empty)|
| path \| pathStartWith \| pathRegex | Path of the URI. **path**, **pathStartWith**, and **pathRegex** represent different matching modes between the paths in the URI and the want. Set any one of them as needed. **path** indicates full matching, **pathStartWith** indicates prefix matching, and **pathRegex** indicates regular expression matching. This attribute is valid only when both **scheme** and **host** are set.| String| Yes (initial value: left empty)|
| type | Data type that matches the want. The value compiles with the [Multipurpose Internet Mail Extensions (MIME)](https://www.iana.org/assignments/media-types/media-types.xhtml?utm_source=ld246.com %E3%80%82) type specification. This attribute can be configured together with **scheme** or be configured separately. | String| Yes (initial value: left empty)|

Example of the **skills** structure:


```json
{
  "abilities": [
    {
      "skills": [
        {
          "actions": [
            "action.system.home"
          ],
          "entities": [
            "entity.system.home"
          ],
          "uris": [
            {
              "scheme":"http",
              "host":"example.com",
              "port":"80",
              "path":"path",
              "type": "text/*"
            }
          ]
        }
      ]
    }
  ]
}
```


## extensionAbilities

The **extensionAbilities** tag represents the configuration of extensionAbilities, which is valid only for the current extensionAbility.

  **Table 7** extensionAbilities

| Name| Description| Data Type| Initial Value Allowed|
| -------- | -------- | -------- | -------- |
| name | Name of the ExtensionAbility component. The value is a string with a maximum of 127 bytes. The name must be unique in the entire application.| String| No|
| srcEntrance | Code path corresponding to the ExtensionAbility component. The value is a string with a maximum of 127 bytes.| String| No|
| description | Description of the ExtensionAbility component. The value is a string with a maximum of 255 bytes or a resource index to the description. | String| Yes (initial value: left empty)|
| icon | Icon of the ExtensionAbility component. The value is the index to an icon resource file. If **ExtensionAbility** is set to **MainElement** of the current module, this attribute is mandatory and its value must be unique in the application.| String| Yes (initial value: left empty)|
| label | Name of the ExtensionAbility component displayed to users. The value is the index to a string resource.<br>**NOTE**<br>If **ExtensionAbility** is set to **MainElement** of the current module, this attribute is mandatory and its value must be unique in the application.| String| No|
| type | Type of the ExtensionAbility component. The options are as follows:<br>- **form**: ExtensionAbility of a widget.<br>- **workScheduler**: ExtensionAbility of a Work Scheduler task.<br>- **inputMethod**: ExtensionAbility of an input method.<br>- **service**: service component running in the background.<br>- **accessibility**: ExtensionAbility of an accessibility feature.<br>- **dataShare**: ExtensionAbility for data sharing.<br>- **fileShare**: ExtensionAbility for file sharing.<br>- **staticSubscriber**: ExtensionAbility for static broadcast.<br>- **wallpaper**: ExtensionAbility of the wallpaper.<br>- **backup**: ExtensionAbility for data backup.<br>- **window**: ExtensionAbility of a window. This type of ExtensionAbility creates a window during startup for which you can develop the GUI. The window is then combined with other application windows through **abilityComponent**.<br>- **thumbnail**: ExtensionAbility for obtaining file thumbnails. You can provide thumbnails for files of customized file types.<br>- **preview**: ExtensionAbility for preview. This type of ExtensionAbility can parse the file and display it in a window. You can combine the window with other application windows.<br>**NOTE**<br>The **service** and **dataShare** types apply only to system applications and do not take effect for third-party applications. | String| No|
| permissions | Permissions required for another application to access the ExtensionAbility component.<br>The value is generally in the reverse domain name notation and contains a maximum of 255 bytes. It is an array of permission names predefined by the system or customized. The name of a customized permission must be the same as the **name** value of a permission defined in the **defPermissions** attribute.| String array| Yes (initial value: left empty)|
| uri | Data URI provided by the ExtensionAbility component. The value is a string with a maximum of 255 bytes, in the reverse domain name notation.<br>**NOTE**<br>This attribute is mandatory when **type** of the ExtensionAbility component is set to **dataShare**.| String| Yes (initial value: left empty)|
|skills | Feature set of [wants](../application-models/want-overview.md) that can be received by the ExtensionAbility component.<br>Configuration rule: In an entry package, you can configure multiple **skills** attributes with the entry capability. (A **skills** attribute with the entry capability is the one that has **action.system.home** and **entity.system.home** configured.) The **label** and **icon** in the first ExtensionAbility that has **skills** configured are used as the **label** and **icon** of the entire OpenHarmony service/application.<br>**NOTE**<br>The **skills** attribute with the entry capability can be configured for the feature-type package of an OpenHarmony application, but not for an OpenHarmony service. | Array| Yes (initial value: left empty)|
| [metadata](#metadata)| Metadata of the ExtensionAbility component.| Object| Yes (initial value: left empty)|
| visible | Whether the ExtensionAbility component can be called by other applications. <br>- **true**: The ExtensionAbility component can be called by other applications.<br>- **false**: The ExtensionAbility component cannot be called by other applications.| Boolean| Yes (initial value: **false**)|

Example of the **extensionAbilities** structure:


```json
{
  "extensionAbilities": [
    {
      "name": "FormName",
      "srcEntrance": "./form/MyForm.ts",
      "icon": "$media:icon",
      "label" : "$string:extension_name",
      "description": "$string:form_description",
      "type": "form", 
      "permissions": ["ohos.abilitydemo.permission.PROVIDER"],
      "readPermission": "",
      "writePermission": "",
      "visible": true,
      "uri":"scheme://authority/path/query",
      "skills": [{
        "actions": [],
        "entities": [],
        "uris": []
      }],
      "metadata": [
        {
          "name": "ohos.extension.form",
          "resource": "$profile:form_config", 
        }
      ]
    }
  ]
}
```


## requestPermissions

The **requestPermissions** tage represents a set of permissions that the application needs to request from the system for running correctly.

  **Table 8** requestPermissions

| Name| Description| Data Type| Value Range| Default Value|
| -------- | -------- | -------- | -------- | -------- |
| name | Permission name. This attribute is mandatory.| String| Custom| –|
| reason | Reason for requesting the permission. This attribute is mandatory when the permission to request is **user_grant**.<br>**NOTE**<br>If the permission to request is **user_grant**, this attribute is required for the application to be released to the application market, and multi-language adaptation is required. | String| Resource reference of the string type in $string: \*\*\* format| A null value|
| usedScene | Scene under which the permission is used. It consists of the **abilities** and **when** sub-attributes. Multiple abilities can be configured.<br>**NOTE**<br>This attribute is optional by default. If the permission to request is **user_grant**, the **abilities** sub-attribute is mandatory and **when** is optional. | **abilities**: string array<br>**when**: string| **abilities**: array of names of UIAbility or ExtensionAbility components<br>**when**: **inuse** or **always**| **abilities**: null<br>**when**: null|

Example of the **requestPermissions** structure:


```json
{
  "module" : {
    "requestPermissions": [
      {
        "name": "ohos.abilitydemo.permission.PROVIDER",
        "reason": "$string:reason",
        "usedScene": {
          "abilities": [
            "EntryFormAbility"
          ],
          "when": "inuse"
        }
      }
    ]
  }
}
```


## shortcuts

The **shortcuts** tag provides the shortcut information of an application. The value is an array of up to four shortcuts. It consists of four sub-attributes: **shortcutId**, **label**, **icon**, and **wants**.

The **shortcut** information is identified in **metadata**, where:

- **name** indicates the name of the shortcut, identified by **ohos.ability.shortcuts**.

- **resource** indicates where the resources of the shortcut are stored.
  
| Attribute| Description| Data Type | Default Value|
| -------- | -------- | -------- | -------- |
| shortcutId | ID of the shortcut. The value is a string with a maximum of 63 bytes.| String| No|
| label | Label of the shortcut, that is, the text description displayed for the shortcut. The value can be a string or a resource index to the label, with a maximum of 255 bytes.| String| Yes (initial value: left empty)|
| icon | Icon of the shortcut. The value is an icon resource index. | String| Yes (initial value: left empty)|
| [wants](../application-models/want-overview.md) | Wants to which the shortcut points. Each want consists of the **bundleName** and **abilityName** sub-attributes.<br>**bundleName**: target bundle name of the shortcut. The value is a string.<br>**abilityName**: target component name of the shortcut. The value is a string.| Object| Yes (initial value: left empty)|


1. Configure the **shortcuts_config.json** file in **/resource/base/profile/**.
   
   ```json
   {
     "shortcuts": [
       {
         "shortcutId": "id_test1",
         "label": "$string:shortcut",
         "icon": "$media:aa_icon",
         "wants": [
           {
             "bundleName": "com.ohos.hello",
             "abilityName": "EntryAbility"
           }
         ]
       }
     ]
   }
   ```

2. In the **abilities** tag of the **module.json5** file, configure the **metadata** tag for the UIAbility component to which a shortcut needs to be added so that the shortcut configuration file takes effect for the UIAbility.
   
   ```json
   {
     "module": {
       // ...
       "abilities": [
         {
           "name": "EntryAbility",
           "srcEntrance": "./ets/entryability/EntryAbility.ts",
           // ...
           "skills": [
             {
               "entities": [
                 "entity.system.home"
               ],
               "actions": [
                 "action.system.home"
               ]
             }
           ],
           "metadata": [
             {
               "name": "ohos.ability.shortcuts",
               "resource": "$profile:shortcuts_config"
             }
           ]
         }
       ]
     }
   }
   ```


## distroFilter

The **distroFilter** tag defines the rules for distributing HAP files based on different device specifications, so that precise matching can be performed when the application market distributes applications. Distribution rules cover five factors: API version, screen shape, screen size, screen resolution, and country code. During distribution, a unique HAP is determined based on the mapping between **deviceType** and these five factors. This tag must be configured in the **/resource/profile resource** directory.

  **Table 9** distroFilter

| Name| Description| Data Type| Initial Value Allowed|
| -------- | -------- | -------- | -------- |
| apiVersion | Supported API versions.| Object array| Yes (initial value: left empty)|
| screenShape | Supported screen shapes.| Object array| Yes (initial value: left empty)|
| screenWindow | Supported window resolutions for when the application is running. This attribute applies only to the lite wearables.| Object array| Yes (initial value: left empty)|
| screenDensity | Pixel density of the screen, in dots per inch (DPI). This attribute is optional. The options are as follows:<br>- **sdpi**: small-scale DPI. This value is applicable to devices with a DPI range of (0, 120].<br>- **mdpi**: medium-scale DPI. This value is applicable to devices with a DPI range of (120, 160].<br>- **ldpi**: large-scale DPI. This value is applicable to devices with a DPI range of (160, 240].<br>- **xldpi**: extra-large-scale DPI. This value is applicable to devices with a DPI range of (240, 320].<br>- **xxldpi**: extra-extra-large-scale DPI. This value is applicable to devices with a DPI range of (320, 480].<br>- **xxxldpi**: extra-extra-extra-large-scale DPI. This value is applicable to devices with a DPI range of (480, 640]. | Object array| Yes (initial value: left empty)|
| countryCode | Code of the country or region to which the application is to be distributed. The value is subject to the [ISO-3166-1](https://developer.harmonyos.com/en/docs/documentation/doc-guides/basic-resource-file-categories-0000001052066099) standard. Enumerated definitions of multiple countries and regions are supported.| Object array| Yes (initial value: left empty)|

  **Table 10** apiVersion

| Name| Description| Data Type| Initial Value Allowed|
| -------- | -------- | -------- | -------- |
| policy | Rule for the sub-attribute value. Set this attribute to **exclude** or **include**.<br>- **exclude**: Exclude the matches of the sub-attribute value.<br>- **include**: Include the matches of the sub-attribute value.| String| No|
| value | API versions, for example, 4, 5, or 6. Example: If an application comes with two versions developed using API version 5 and API version 6 for the same device model, two installation packages of the entry type can be released for the application.| Array| No|

  **Table 11** screenShape

| Name| Description| Data Type| Initial Value Allowed|
| -------- | -------- | -------- | -------- |
| policy | Rule for the sub-attribute value. Set this attribute to **exclude** or **include**.<br>- **exclude**: Exclude the matches of the sub-attribute value.<br>- **include**: Include the matches of the sub-attribute value.| String| No|
| value | Screen shapes. The value can be **circle**, **rect**, or both. Example: Different HAP files can be provided for a smart watch with a circular face and that with a rectangular face.| String array| No|

  **Table 12** screenWindow

| Name| Description| Data Type| Initial Value Allowed|
| -------- | -------- | -------- | -------- |
| policy | Rule for the sub-attribute value. Set this attribute to **exclude** or **include**.<br>- **exclude**: Exclude the matches of the sub-attribute value.<br>- **include**: Include the matches of the sub-attribute value.| String| No|
| value | Screen width and height, in pixels. The value an array of supported width and height pairs, each in the "width * height" format, for example, **"454 * 454"**.| String array| No|

  **Table 13** screenDensity

| Name| Description| Data Type| Initial Value Allowed|
| -------- | -------- | -------- | -------- |
| policy | Rule for the sub-attribute value. Set this attribute to **exclude** or **include**.<br>- **exclude**: Exclude the matches of the sub-attribute value.<br>- **include**: Include the matches of the sub-attribute value.| String| No|
| value | Pixel density of the screen, in DPI.| String array| No|

  **Table 14** countryCode

| Name| Description| Data Type| Initial Value Allowed|
| -------- | -------- | -------- | -------- |
| policy | Rule for the sub-attribute value. Set this attribute to **exclude** or **include**.<br>- **exclude**: Exclude the matches of the sub-attribute value.<br>- **include**: Include the matches of the sub-attribute value.| String| No|
| value | Code of the country or region to which the application is to be distributed.| String array| No|

Configure the **distro_filter_config.json** file (this file name is customizable) in **resources/base/profile** under the development view.


```json
{
  "distroFilter": {
    "apiVersion": {
      "policy": "include",
      "value": [
        3,
        4
      ]
    },
    "screenShape": {
      "policy": "include",
      "value": [
        "circle",
        "rect"
      ]
    },
    "screenWindow": {
      "policy": "include",
      "value": [
        "454*454",
        "466*466"
      ]
    },
    "screenDensity": {
      "policy": "exclude",
      "value": [
        "ldpi",
        "xldpi"
      ]
    },
    "countryCode": {// Distribution to the Chinese mainland and Hong Kong, China is supported.
      "policy": "include",
      "value": [
        "CN",
        "HK"
      ]
    }
  }
}
```

Configure **metadata** in the **module** tag in the **module.json5** file.


```json
{
  "module": {
    // ...
    "metadata": [
      {
        "name": "ohos.module.distro",
        "resource": "$profile:distro_filter_config",
      }
    ]
  }
}
```


## testRunner

The **testRunner** tag represents the supported test runner.

  **Table 15** testRunner

| Name| Description| Data Type| Initial Value Allowed|
| -------- | -------- | -------- | -------- |
| name | Name of the test runner object. The value is a string with a maximum of 255 bytes.| String| No|
| srcPath | Code path of the test runner. The value is a string with a maximum of 255 bytes. | String| No|

Example of the / structure:


```json
{
  "module": {
    // ...
    "testRunner": {
      "name": "myTestRunnerName",
      "srcPath": "etc/test/TestRunner.ts"
    }
  }
}
```