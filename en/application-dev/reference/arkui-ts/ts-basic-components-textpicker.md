# TextPicker

The **\<TextPicker>** component allows users to scroll to select text.

>  **NOTE**
>
>  This component is supported since API version 8. Updates will be marked with a superscript to indicate their earliest API version.


## Child Components

Not supported


## APIs

TextPicker(options?: {range: string[]|Resource|TextPickerRangeContent[], selected?: number, value?: string})

Creates a text picker based on the selection range specified by **range**.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| range | string[] \| [Resource](ts-types.md#resource)\|[TextPickerRangeContent](#textpickerrangecontent10)[]<sup>10+</sup> | Yes| Data selection range of the picker. This parameter cannot be set to an empty array. If set to an empty array, it will not be displayed. If it is dynamically changed to an empty array, the current value remains displayed.|
| selected | number | No| Index of the default item in the range.<br>Default value: **0**|
| value | string | No| Value of the default item in the range. The priority of this parameter is lower than that of **selected**.<br>Default value: value of the first item<br>**NOTE**\<br>This parameter works only for a text list. It does not work for an image list or a list consisting of text and images.|

## TextPickerRangeContent<sup>10+</sup>

| Name| Type                                                | Mandatory| Description  |
| ------ | -------------------------------------------------------- | ---- | ---------- |
| icon   | string \| [Resource](ts-types.md#resource) | Yes  | Image resource.|
| text   | string \| [Resource](ts-types.md#resource) | No  | Text information.|

## Attributes

In addition to the [universal attributes](ts-universal-attributes-size.md), the following attributes are supported.

| Name| Type| Description|
| -------- | -------- | -------- |
| defaultPickerItemHeight | number \| string | Height of each item in the picker.|
| disappearTextStyle<sup>10+</sup> | [PickerTextStyle](ts-basic-components-datepicker.md#pickertextstyle10) | Font color, font size, and font width for the top and bottom items.|
| textStyle<sup>10+</sup> | [PickerTextStyle](ts-basic-components-datepicker.md#pickertextstyle10) | Font color, font size, and font width of all items except the top, bottom, and selected items.|
| selectedTextStyle<sup>10+</sup> | [PickerTextStyle](ts-basic-components-datepicker.md#pickertextstyle10) | Font color, font size, and font width of the selected item.|

## Events

In addition to the [universal events](ts-universal-events-click.md), the following events are supported.

| Name| Description|
| -------- | -------- |
| onChange(callback: (value: string, index: number) =&gt; void) | Triggered when an item in the picker is selected.<br>- **value**: value of the selected item.<br>**NOTE**<br>For a text list or a list consisting of text and images, **value** indicates the text value of the selected item. For an image list, **value** is empty.<br>- **index**: index of the selected item. |


## Example

```ts
// xxx.ets
@Entry
@Component
struct TextPickerExample {
  private select: number = 1
  private fruits: string[] = ['apple1', 'orange2', 'peach3', 'grape4']

  build() {
    Column() {
      TextPicker({ range: this.fruits, selected: this.select })
        .onChange((value: string, index: number) => {
          console.info('Picker item changed, value: ' + value + ', index: ' + index)
        })
    }
  }
}
```

![en-us_image_0000001257058417](figures/en-us_image_0000001257058417.png)
