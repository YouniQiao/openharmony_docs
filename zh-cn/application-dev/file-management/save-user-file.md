# 保存用户文件

在从网络下载文件到本地、或将已有用户文件另存为新的文件路径等场景下，需要使用FilePicker提供的保存用户文件的能力。

对音频、图片、视频、文档类文件的保存操作类似，均通过调用对应picker的save()接口并传入对应的saveOptions来实现。


## 保存图片或视频类文件

1. 导入选择器模块。

   ```ts
   import picker from '@ohos.file.picker';
   ```

2. 创建图库保存选项实例。

   ```ts
   const photoSaveOptions = new picker.PhotoSaveOptions(); // 创建文件管理器保存选项实例
   photoSaveOptions.newFileNames = ["PhotoViewPicker01.jpg"]; // 保存文件名（可选）
   ```

3. 创建图库选择器实例，调用[save()](../reference/apis/js-apis-file-picker.md#save)接口拉起FilePicker界面进行文件保存。
     用户选择目标文件夹，用户选择与文件类型相对应的文件夹，即可完成文件保存操作。保存成功后，返回保存文档的URI。

   ```ts
   const photoViewPicker = new picker.PhotoViewPicker();
   photoViewPicker.save(photoSaveOptions)
     .then(async (photoSaveResult) => {
       let uri = photoSaveResult[0];
       // 获取到到图片或者视频文件的URI后进行文件读取等操作
     })
     .catch((err) => {
       console.error(`Invoke documentPicker.select failed, code is ${err.code}, message is ${err.message}`);
     })
   ```

## 保存文档类文件

1. 导入选择器模块。

   ```ts
   import picker from '@ohos.file.picker';
   ```

2. 创建文档保存选项实例。

   ```ts
   const documentSaveOptions = new picker.DocumentSaveOptions(); // 创建文件管理器选项实例
   documentSaveOptions.newFileNames = ["DocumentViewPicker01.txt"]; // 保存文件名（可选）
   ```

3. 创建文档选择器实例。调用[save()](../reference/apis/js-apis-file-picker.md#save-3)接口拉起FilePicker界面进行文件保存。
   用户选择目标文件夹，用户选择与文件类型相对应的文件夹，即可完成文件保存操作。保存成功后，返回保存文档的URI。

   > **说明：**
   >
   > 目前DocumentSelectOptions不支持参数配置，默认可以选择所有类型的用户文件。

   ```ts
   const documentViewPicker = new picker.DocumentViewPicker(); // 创建文件选择器实例
   documentViewPicker.save(documentSaveOptions)
     .then(async (documentSaveResult) => {
       let uri = documentSaveResult[0];
       // 例如，可以根据获取的URI进行文件写入等操作
     })
     .catch((err) => {
       console.error(`Invoke documentPicker.save failed, code is ${err.code}, message is ${err.message}`);
     })
   ```

## 保存音频类文件

1. 导入选择器模块。

   ```ts
   import picker from '@ohos.file.picker';
   ```

2. 创建音频保存选项实例。

   ```ts
   const audioSaveOptions = new picker.AudioSaveOptions(); // 创建文件管理器选项实例
   audioSaveOptions.newFileNames = ['AudioViewPicker01.mp3']; // 保存文件名（可选）
   ```

3. 创建音频选择器实例。调用[save()](../reference/apis/js-apis-file-picker.md#save-6)接口拉起FilePicker界面进行文件保存。
     用户选择目标文件夹，用户选择与文件类型相对应的文件夹，即可完成文件保存操作。保存成功后，返回保存文档的URI。
   > **说明：**
   >
   > 目前AudioSelectOptions不支持参数配置，默认可以选择所有类型的用户文件。

   ```ts
   const audioViewPicker = new picker.AudioViewPicker();
   audioViewPicker.save(audioSaveOptions)
     .then((audioSelectResult) => {
       let uri = audioSelectResult[0];
       // 获取到到音频文件的URI后进行文件读取等操作
     })
     .catch((err) => {
       console.error(`Invoke audioPicker.select failed, code is ${err.code}, message is ${err.message}`);
     })
   ```
