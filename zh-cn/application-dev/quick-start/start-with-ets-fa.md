# 使用ArkTS语言开发（FA模型）


>  **说明：**
>
>  请使用**DevEco Studio V3.0.0.601 Beta1**及更高版本。
>
>  为确保运行效果，本文以使用**DevEco Studio 3.1 Beta2**版本为例，点击[此处](https://developer.harmonyos.com/cn/develop/deveco-studio)获取下载链接。


## 创建ArkTS工程

1. 若首次打开**DevEco Studio**，请点击**Create Project**创建工程。如果已经打开了一个工程，请在菜单栏选择**File** &gt; **New** &gt; **Create Project**来创建一个新工程。选择**Application**应用开发（本文以应用开发为例，**Atomic Service**对应为原子化服务开发），选择模板“**Empty Ability**”，点击**Next**进行下一步配置。

   ![createProject](figures/createProject.png)

2. 进入配置工程界面，**Compile SDK** 选择“**8**”（**Compile SDK**选择“**9**”时注意同步选择**Model** 为“**FA**”，此处以选择“**8**”为例），**Language**选择“**ArkTS**”，其他参数保持默认设置即可。

   ![chooseFAModel_ets](figures/chooseFAModel_ets.png)

   > **说明：**
   > 
   > DevEco Studio V3.0 Beta3及更高版本支持使用ArkTS[低代码开发](https://developer.harmonyos.com/cn/docs/documentation/doc-guides-V3/ide-low-code-overview-0000001480179573-V3)方式。
   > 
   > 低代码开发方式具有丰富的UI界面编辑功能，通过可视化界面开发方式快速构建布局，可有效降低开发者的上手成本并提升开发者构建UI界面的效率。
   > 
   > 如需使用低代码开发方式，请打开上图中的Enable Super Visual开关。

3. 点击**Finish**，工具会自动生成示例代码和相关资源，等待工程创建完成。
4. 工程创建完成后，在**entry > build-profile.json5**文件中，将targets中的runtimeOS改为“OpenHarmony”，然后点击右上角提示框的**Sync Now**以进行OpenHarmony应用开发。


## ArkTS工程目录结构（FA模型）

![zh-cn_image_0000001384652328](figures/zh-cn_image_0000001384652328.png)

- **entry**：OpenHarmony工程模块，编译构建生成一个[HAP](../../glossary.md#hap)包。
  - **src &gt; main &gt; ets**：用于存放ArkTS源码。
  - **src &gt; main &gt; ets &gt; MainAbility**：应用/服务的入口。
  - **src &gt; main &gt; ets &gt; MainAbility &gt; pages**：MainAbility包含的页面。
  - **src &gt; main &gt; ets &gt; MainAbility &gt; pages &gt; index.ets**：pages列表中的第一个页面，即应用的首页入口。
  - **src &gt; main &gt; ets &gt; MainAbility &gt; app.ets**：承载Ability生命周期。
  - **src &gt; main &gt; resources**：用于存放应用/服务所用到的资源文件，如图形、多媒体、字符串、布局文件等。关于资源文件，详见[资源文件的分类](resource-categories-and-access.md#资源分类)。
  - **src &gt; main &gt; config.json**：模块配置文件。主要包含HAP的配置信息、应用/服务在具体设备上的配置信息以及应用/服务的全局配置信息。具体的配置文件说明，详见[应用配置文件（FA模型）](application-configuration-file-overview-fa.md)。
  - **build-profile.json5**：当前的模块信息 、编译信息配置项，包括buildOption、targets配置等。其中targets中可配置当前运行环境，默认为HarmonyOS。若需开发OpenHarmony应用，则需开发者自行修改为OpenHarmony。
  - **hvigorfile.ts**：模块级编译构建任务脚本，开发者可以自定义相关任务和代码实现。
- **build-profile.json5**：应用级配置信息，包括签名、产品配置等。
- **hvigorfile.ts**：应用级编译构建任务脚本。


## 构建第一个页面

1. 使用文本组件。

   工程同步完成后，在“**Project**”窗口，点击“**entry &gt; src &gt; main &gt; ets &gt; MainAbility &gt; pages**”，打开“**index.ets**”文件，可以看到页面由Text组件组成。“**index.ets**”文件的示例如下：
   
   ```ts
   // index.ets
   @Entry
   @Component
   struct Index {
     @State message: string = 'Hello World'
   
     build() {
       Row() {
         Column() {
           Text(this.message)
             .fontSize(50)
             .fontWeight(FontWeight.Bold)
         }
         .width('100%')
       }
       .height('100%')
     }
   }
   ```

2. 添加按钮。

   在默认页面基础上，我们添加一个Button组件，作为按钮响应用户点击，从而实现跳转到另一个页面。“**index.ets**”文件的示例如下：
   
   ```ts
   // index.ets
   @Entry
   @Component
   struct Index {
     @State message: string = 'Hello World'
   
     build() {
       Row() {
         Column() {
           Text(this.message)
             .fontSize(50)
             .fontWeight(FontWeight.Bold)
           // 添加按钮，以响应用户点击
           Button() {
             Text('Next')
               .fontSize(30)
               .fontWeight(FontWeight.Bold)
           }
           .type(ButtonType.Capsule)
           .margin({
             top: 20
           })
           .backgroundColor('#0D9FFB')
           .width('40%')
           .height('5%')
         }
         .width('100%')
       }
       .height('100%')
     }
   }
   ```

3. 在编辑窗口右上角的侧边工具栏，点击Previewer，打开预览器。第一个页面效果如下图所示：

   ![zh-cn_image_0000001311334976](figures/zh-cn_image_0000001311334976.png)


## 构建第二个页面

1. 创建第二个页面。

   - 新建第二个页面文件。在“**Project**”窗口，打开“**entry &gt; src &gt; main &gt; ets &gt; MainAbility**”，右键点击“**pages**”文件夹，选择“**New &gt; ArkTS File**”，命名为“**second**”，点击“**Finish**”。可以看到文件目录结构如下：
      ![zh-cn_image_0000001311334932](figures/zh-cn_image_0000001311334932.png)

      > **说明：**
      > 
      > 开发者也可以在右键点击“**pages**”文件夹时，选择“**New &gt; Page**”，则无需手动配置相关页面路由。
   - 配置第二个页面的路由。在config.json文件中的“module - js - pages”下配置第二个页面的路由“pages/second”。示例如下：
     
      ```json
      {
        "module": {
          "js": [
            {
              "pages": [
                "pages/index",
                "pages/second"
              ]
              }
          ]
        }
      }
      ```

2. 添加文本及按钮。

   参照第一个页面，在第二个页面添加Text组件、Button组件等，并设置其样式。“**second.ets**”文件的示例如下：
   
   ```ts
   // second.ets
   @Entry
   @Component
   struct Second {
     @State message: string = 'Hi there'
   
     build() {
       Row() {
         Column() {
           Text(this.message)
             .fontSize(50)
             .fontWeight(FontWeight.Bold)
           Button() {
             Text('Back')
               .fontSize(25)
               .fontWeight(FontWeight.Bold)
           }
           .type(ButtonType.Capsule)
           .margin({
             top: 20
           })
           .backgroundColor('#0D9FFB')
           .width('40%')
           .height('5%')
         }
         .width('100%')
       }
       .height('100%')
     }
   }
   ```


## 实现页面间的跳转

页面间的导航可以通过[页面路由router](../reference/apis/js-apis-router.md)来实现。页面路由router根据页面url找到目标页面，从而实现跳转。使用页面路由请导入router模块。

1. 第一个页面跳转到第二个页面。

   在第一个页面中，跳转按钮绑定onClick事件，点击按钮时跳转到第二页。“**index.ets**”文件的示例如下：
   
   ```ts
   // index.ets
   // 导入页面路由模块
   import router from '@ohos.router';
   
   @Entry
   @Component
   struct Index {
     @State message: string = 'Hello World'
   
     build() {
       Row() {
         Column() {
           Text(this.message)
             .fontSize(50)
             .fontWeight(FontWeight.Bold)
           // 添加按钮，以响应用户点击
           Button() {
             Text('Next')
               .fontSize(30)
               .fontWeight(FontWeight.Bold)
           }
           .type(ButtonType.Capsule)
           .margin({
             top: 20
           })
           .backgroundColor('#0D9FFB')
           .width('40%')
           .height('5%')
           // 跳转按钮绑定onClick事件，点击时跳转到第二页
           .onClick(() => {
             router.push({ url: 'pages/second' })
             // 若为API 9工程，则可使用以下接口
             // router.pushUrl({ url: 'pages/second' })

           })
         }
         .width('100%')
       }
       .height('100%')
     }
   }
   ```

2. 第二个页面返回到第一个页面。

   在第二个页面中，返回按钮绑定onClick事件，点击按钮时返回到第一页。“**second.ets**”文件的示例如下：
   
   ```ts
   // second.ets
   // 导入页面路由模块
   import router from '@ohos.router';
   
   @Entry
   @Component
   struct Second {
     @State message: string = 'Hi there'
   
     build() {
       Row() {
         Column() {
           Text(this.message)
             .fontSize(50)
             .fontWeight(FontWeight.Bold)
           Button() {
             Text('Back')
               .fontSize(25)
               .fontWeight(FontWeight.Bold)
           }
           .type(ButtonType.Capsule)
           .margin({
             top: 20
           })
           .backgroundColor('#0D9FFB')
           .width('40%')
           .height('5%')
           // 返回按钮绑定onClick事件，点击按钮时返回到第一页
           .onClick(() => {
             router.back()
           })
         }
         .width('100%')
       }
       .height('100%')
     }
   }
   ```

3. 打开index.ets文件，点击预览器中的![zh-cn_image_0000001311015192](figures/zh-cn_image_0000001311015192.png)按钮进行刷新。效果如下图所示：

   ![zh-cn_image_0000001364254729](figures/zh-cn_image_0000001364254729.png)


## 使用真机运行应用

1. 将搭载OpenHarmony标准系统的开发板与电脑连接。

2. 点击**File** &gt; **Project Structure...** &gt; **Project** &gt; **SigningConfigs** 界面勾选“**Automatically generate signature**”，等待自动签名完成即可，点击“**OK**”。如下图所示：

   ![signConfig](figures/signConfig.png)

3. 在编辑窗口右上角的工具栏，点击![zh-cn_image_0000001364054485](figures/zh-cn_image_0000001364054485.png)按钮运行。效果如下图所示：

   ![zh-cn_image_0000001364254729](figures/zh-cn_image_0000001364254729.png)

恭喜您已经使用ArkTS语言开发（FA模型）完成了第一个OpenHarmony应用，快来[探索更多的OpenHarmony功能](../application-dev-guide.md)吧。
