# @ohos.arkui.drawableDescriptor (DrawableDescriptor)

The **DrawableDescriptor** module provides APIs for obtaining **pixelMap** objects, including the foreground, background, mask, and layered icons.

> **NOTE**
>
> The initial APIs of this module are supported since API version 10. Newly added APIs will be marked with a superscript to indicate their earliest API version.
>
> You can preview how this component looks on a real device. The preview is not yet available in the DevEco Studio Previewer.

## Modules to Import

```js
import { DrawableDescriptor, LayeredDrawableDescriptor } from '@ohos.arkui.drawableDescriptor';
```

## DrawableDescriptor.constructor
constructor()

Creates a **DrawableDescriptor** or **LayeredDrawableDescriptor** object. The globalization API [getDrawableDescriptor](js-apis-resource-manager.md##getdrawabledescriptor) or [getDrawableDescriptorByName](js-apis-resource-manager.md##getdrawabledescriptorbyname) is required for object construction.

**System API**: This is a system API.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

### DrawableDescriptor

Creates a **DrawableDescriptor** object when the passed resource ID or name belongs to a common image.

### LayeredDrawableDescriptor

Creates a **LayeredDrawableDescriptor** object when the passed resource ID or name belongs to a JSON file that contains foreground and background resources.

**Example**
```js
@Entry
@Component
struct Index {
  private resManager = getContext().resourceManager
  let drawable1 = resManager.getDrawableDescriptor($r('app.media.icon').id)
  let drawable2 = resManager.getDrawableDescriptorByName(icon)
  let layeredDrawable1 = resManager.getDrawableDescriptor($r('app.media.file').id)
  let layeredDrawable1 = resManager.getDrawableDescriptor(file)
 }
```

## DrawableDescriptor.getPixelMap
getPixelMap(): image.PixelMap;

Obtains this **pixelMap** object.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Return value**

| Type                             | Description             |
| --------------------------------- | ---------------- |
| [image.PixelMap](../apis/js-apis-image.md#pixelmap7) | **pixelMap** object.|

**Example**
  ```js
  @State pixmap: PixelMap = drawable1.getPixelMap();
  ```

## LayeredDrawableDescriptor.getPixelMap
getPixelMap(): image.PixelMap;

Obtains the **pixelMap** object where the foreground, background, and mask are blended and cropped.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Return value**

| Type                             | Description             |
| --------------------------------- | ---------------- |
| [image.PixelMap](../apis/js-apis-image.md#pixelmap7) | **pixelMap** object.|

**Example**
  ```js
  @State pixmap: PixelMap = layeredDrawable1.getPixelMap();
  ```

## LayeredDrawableDescriptor.getForeground
getForeground(): DrawableDescriptor;

Obtains the **DrawableDescriptor** object of the foreground.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Return value**

| Type                             | Description             |
| --------------------------------- | ---------------- |
| [DrawableDescriptor](#drawabledescriptor) | **DrawableDescriptor** object.|

**Example**
  ```js
  @State drawable: DrawableDescriptor = layeredDrawable1.getForeground();
  ```

## LayeredDrawableDescriptor.getBackground
getBackground(): DrawableDescriptor;

Obtains the **DrawableDescriptor** object of the background.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Return value**

| Type                             | Description             |
| --------------------------------- | ---------------- |
| [DrawableDescriptor](#drawabledescriptor) | **DrawableDescriptor** object.|

**Example**
  ```js
  @State drawable: DrawableDescriptor = layeredDrawable1.getBackground();
  ```

## LayeredDrawableDescriptor.getMask
getMask(): DrawableDescriptor;

Obtains the **DrawableDescriptor** object of the mask.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Return value**

| Type                             | Description             |
| --------------------------------- | ---------------- |
| [DrawableDescriptor](#drawabledescriptor) | **DrawableDescriptor** object.|

**Example**
  ```js
  @State drawable: DrawableDescriptor = layeredDrawable1.getMask();
  ```
<!--no_check-->