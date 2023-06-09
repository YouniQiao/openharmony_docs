# @ohos.arkui.componentSnapshot（组件截图）

本模块提供获取组件截图的能力，包括已加载的组件的截图和没有加载的组件的截图。

> **说明：**
>
> 本模块首批接口从 API version 10 开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
>
> 示例效果请以真机运行为准，当前 IDE 预览器不支持。

## 导入模块

```js
import componentSnapshot from "@ohos.arkui.componentSnapshot";
```

## componentSnapshot.get

get(id: string, callback: AsyncCallback<image.PixelMap>): void

获取已加载的组件的截图，传入组件的[ID 标识](../arkui-ts/ts-universal-attributes-component-id.md#组件标识)，找到对应组件进行截图。通过回调返回结果。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名   | 类型                                | 必填 | 说明                                                                           |
| -------- | ----------------------------------- | ---- | ------------------------------------------------------------------------------ |
| id       | string                              | 是   | 目标组件的[ID 标识](../arkui-ts/ts-universal-attributes-component-id.md#组件标识) |
| callback | AsyncCallback&lt;image.PixelMap&gt; | 是   | 截图返回结果的回调。                                                             |

**示例：**

```js
import componentSnapshot from '@ohos.arkui.componentSnapshot'
import image from '@ohos.multimedia.image'

@Entry
@Component
struct SnapshotExample {
  @State pixmap: image.PixelMap = undefined

  build() {
    Column() {
      Image(this.pixmap)
        .width(300).height(300)
      // ...Component
      // ...Components
      // ...Components
      Button("click to generate UI snapshot")
        .onClick(() => {
          componentSnapshot.get("root", (error: BusinessError, pixmap: image.PixelMap) => {
                 this.pixmap = pixmap
                 // save pixmap to file
                 // ....
             })
        })
    }
    .width('80%')
    .margin({ left: 10, top: 5, bottom: 5 })
    .height(200)
    .border({ color: '#880606', width: 2 })
    .id("root")
  }
}
```

## componentSnapshot.get

get(id: string): Promise<image.PixelMap>

获取已加载的组件的截图，传入组件的[ID 标识](../arkui-ts/ts-universal-attributes-component-id.md#组件标识)，找到对应组件进行截图。通过Promise返回结果。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名  | 类型                                                    | 必填 | 说明                 |
| ------- | ------------------------------------------------------- | ---- | -------------------- |
| id       | string                              | 是   | 目标组件的[ID 标识](../arkui-ts/ts-universal-attributes-component-id.md#组件标识) |

**返回值：**

| 类型                          | 说明           |
| ----------------------------- | -------------- |
| Promise&lt;image.PixelMap&gt; | 截图返回的结果。 |

**示例：**

```js
import componentSnapshot from '@ohos.arkui.componentSnapshot'
import image from '@ohos.multimedia.image'

@Entry
@Component
struct SnapshotExample {
  @State pixmap: image.PixelMap = undefined

  build() {
    Column() {
      Image(this.pixmap)
        .width(300).height(300)
      // ...Component
      // ...Components
      // ...Components
      Button("click to generate UI snapshot")
        .onClick(() => {
          componentSnapshot.get("root")
            .then((pixmap: image.PixelMap) => {
              this.pixmap = pixmap
              // save pixmap to file
              // ....
            })
        })
    }
    .width('80%')
    .margin({ left: 10, top: 5, bottom: 5 })
    .height(200)
    .border({ color: '#880606', width: 2 })
    .id("root")
  }
}
```

## componentSnapshot.createFromBuilder

createFromBuilder(builder: CustomBuilder, callback: AsyncCallback<image.PixelMap>): void

在应用后台渲染CustomBuilder自定义组件，并输出其截图。通过回调返回结果。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名   | 类型                                                    | 必填 | 说明                 |
| -------- | ------------------------------------------------------- | ---- | -------------------- |
| builder  | [CustomBuilder](../arkui-ts/ts-types.md#custombuilder8) | 是   | 自定义组件构建函数。 |
| callback | AsyncCallback&lt;image.PixelMap&gt;                     | 是   | 截图返回结果的回调。   |

**示例：**

```js
import componentSnapshot from '@ohos.arkui.componentSnapshot'
import image from '@ohos.multimedia.image'
@Entry
@Component
struct OffscreenSnapshotExample {
  @State pixmap: image.PixelMap = undefined

  @Builder
  RandomBuilder() {
    Flex({ direction: FlexDirection.Column, justifyContent: FlexAlign.Center,   alignItems: ItemAlign.Center }) {
      Text('Test menu item 1')
        .fontSize(20)
        .width(100)
        .height(50)
        .textAlign(TextAlign.Center)
      Divider().height(10)
      Text('Test menu item 2')
        .fontSize(20)
        .width(100)
        .height(50)
        .textAlign(TextAlign.Center)
    }.width(100)
  }
  build() {
    Column() {
      Button("click to generate offscreen UI snapshot")
        .onClick(()=> {
             componentSnapshot.createFromBuilder(this.RandomBuilder.bind(this),
                        (error: BusinessError, pixmap: image.PixelMap) => {
                 this.pixmap = pixmap
                 // save pixmap to file
                 // ....
             })
        })
    }.width('80%').margin({ left: 10, top: 5, bottom: 5 }).height(200)
    .border({ color: '#880606', width: 2 })
  }
}
```

## componentSnapshot.createFromBuilder

createFromBuilder(builder: CustomBuilder): Promise<image.PixelMap>

在应用后台渲染CustomBuilder自定义组件，并输出其截图。通过Promise返回结果。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名  | 类型                                                    | 必填 | 说明                 |
| ------- | ------------------------------------------------------- | ---- | -------------------- |
| builder | [CustomBuilder](../arkui-ts/ts-types.md#custombuilder8) | 是   | 自定义组件构建函数。 |

**返回值：**

| 类型                          | 说明           |
| ----------------------------- | -------------- |
| Promise&lt;image.PixelMap&gt; | 截图返回的结果。 |

**示例：**

```js
import componentSnapshot from '@ohos.arkui.componentSnapshot'
import image from '@ohos.multimedia.image'
@Entry
@Component
struct OffscreenSnapshotExample {
  @State pixmap: image.PixelMap = undefined

  @Builder
  RandomBuilder() {
    Flex({ direction: FlexDirection.Column, justifyContent: FlexAlign.Center,   alignItems: ItemAlign.Center }) {
      Text('Test menu item 1')
        .fontSize(20)
        .width(100)
        .height(50)
        .textAlign(TextAlign.Center)
      Divider().height(10)
      Text('Test menu item 2')
        .fontSize(20)
        .width(100)
        .height(50)
        .textAlign(TextAlign.Center)
    }.width(100)
  }
  build() {
    Column() {
      Button("click to generate offscreen UI snapshot")
        .onClick(()=> {
             componentSnapshot.createFromBuilder(this.RandomBuilder.bind(this))
             .then((pixmap: image.PixelMap) {
                 this.pixmap = pixmap
                 // save pixmap to file
                 // ....
             })
        })
    }.width('80%').margin({ left: 10, top: 5, bottom: 5 }).height(200)
    .border({ color: '#880606', width: 2 })
  }
}
```
