# @ohos.enterprise.dateTimeManager (System Time Management)

The **dateTimeManager** module provides APIs for system time management. Only the enterprise device administrator applications can call the APIs provided by this module.

> **NOTE**
> 
> The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## Modules to Import

```js
import dateTimeManager from '@ohos.enterprise.dateTimeManager'
```

## dateTimeManager.setDateTime

setDateTime(admin: Want, time: number, callback: AsyncCallback\<void>): void

Sets the system time. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.ENTERPRISE_SET_DATETIME

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name  | Type                                 | Mandatory  | Description     |
| ----- | ----------------------------------- | ---- | ------- |
| admin | [Want](js-apis-app-ability-want.md) | Yes   | Device administrator application.|
| time  | number | Yes| Timestamp (ms).|
| callback | AsyncCallback\<void> | Yes| Callback used to return the result. If the operation is successful, **err** is **null**. Otherwise, **err** is an error object.|

**Error codes**

For details about the error codes, see [Enterprise Device Management Error Codes](../errorcodes/errorcode-enterpriseDeviceManager.md).

| ID| Error Message                                                                     |
| ------- | ---------------------------------------------------------------------------- |
| 9200001 | the application is not an administrator of the device.                       |
| 9200002 | the administrator application does not have permission to manage the device. |

**Example**

```js
let wantTemp = {
    bundleName: "bundleName",
    abilityName: "abilityName",
};
dateTimeManager.setDateTime(wantTemp, 1526003846000, (error) => {
    if (error) {
        console.log("error code:" + error.code + " error message:" + error.message);
    }
})
```

## dateTimeManager.setDateTime

setDateTime(admin: Want, time: number): Promise\<void>

Sets the system time. This API uses a promise to return the result.

**Required permissions**: ohos.permission.ENTERPRISE_SET_DATETIME

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name  | Type                                 | Mandatory  | Description     |
| ----- | ----------------------------------- | ---- | ------- |
| admin | [Want](js-apis-app-ability-want.md) | Yes   | Device administrator application.|
| time  | number | Yes| Timestamp (ms).|

**Return value**

| Type  | Description                                 |
| ----- | ----------------------------------- |
| Promise\<void> | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Enterprise Device Management Error Codes](../errorcodes/errorcode-enterpriseDeviceManager.md).

| ID| Error Message                                                                     |
| ------- | ---------------------------------------------------------------------------- |
| 9200001 | the application is not an administrator of the device.                        |
| 9200002 | the administrator application does not have permission to manage the device. |

**Example**

```js
let wantTemp = {
    bundleName: "bundleName",
    abilityName: "abilityName",
};
dateTimeManager.setDateTime(wantTemp, 1526003846000).then(() => {
}).catch((error) => {
    console.log("error code:" + error.code + " error message:" + error.message);
})
```

## dateTimeManager.disallowModifyDateTime<sup>10+</sup>

disallowModifyDateTime(admin: Want, disallow: boolean, callback: AsyncCallback\<void>): void

Disables modification of the system time. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.ENTERPRISE_SET_DATETIME

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name  | Type                                 | Mandatory  | Description     |
| ----- | ----------------------------------- | ---- | ------- |
| admin | [Want](js-apis-app-ability-want.md) | Yes   | Device administrator application.|
| disallow  | boolean | Yes| Whether to disable modification of the system time. The value **true** means to disable modification of the system time, and **false** means the opposite.|
| callback | AsyncCallback\<void> | Yes| Callback used to return the result. If the operation is successful, **err** is **null**. Otherwise, **err** is an error object.|

**Error codes**

For details about the error codes, see [Enterprise Device Management Error Codes](../errorcodes/errorcode-enterpriseDeviceManager.md).

| ID| Error Message                                                                     |
| ------- | ---------------------------------------------------------------------------- |
| 9200001 | the application is not an administrator of the device.                       |
| 9200002 | the administrator application does not have permission to manage the device. |

**Example**

```js
let wantTemp = {
    bundleName: "bundleName",
    abilityName: "abilityName",
};
dateTimeManager.disallowModifyDateTime(wantTemp, true, (error) => {
    if (error) {
        console.log("error code:" + error.code + " error message:" + error.message);
    }
})
```

## dateTimeManager.disallowModifyDateTime<sup>10+</sup>

disallowModifyDateTime(admin: Want, disallow: boolean): Promise\<void>

Disables modification of the system time. This API uses a promise to return the result.

**Required permissions**: ohos.permission.ENTERPRISE_SET_DATETIME

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name  | Type                                 | Mandatory  | Description     |
| ----- | ----------------------------------- | ---- | ------- |
| admin | [Want](js-apis-app-ability-want.md) | Yes   | Device administrator application.|
| disallow  | boolean | Yes| Whether to disable modification of the system time. The value **true** means to disable modification of the system time, and **false** means the opposite.|

**Return value**

| Type  | Description                                 |
| ----- | ----------------------------------- |
| Promise\<void> | that returns no value. If the operation fails, an error object is thrown.|

**Error codes**

For details about the error codes, see [Enterprise Device Management Error Codes](../errorcodes/errorcode-enterpriseDeviceManager.md).

| ID| Error Message                                                                     |
| ------- | ---------------------------------------------------------------------------- |
| 9200001 | the application is not an administrator of the device.                        |
| 9200002 | the administrator application does not have permission to manage the device. |

**Example**

```js
let wantTemp = {
    bundleName: "bundleName",
    abilityName: "abilityName",
};
dateTimeManager.disallowModifyDateTime(wantTemp, true).then(() => {
}).catch((error) => {
    console.log("error code:" + error.code + " error message:" + error.message);
})
```

## dateTimeManager.isModifyDateTimeDisallowed<sup>10+</sup>

isModifyDateTimeDisallowed(admin: Want, callback: AsyncCallback\<boolean>): void

Checks whether modification of the system time is disabled. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.ENTERPRISE_SET_DATETIME

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name  | Type                                 | Mandatory  | Description     |
| ----- | ----------------------------------- | ---- | ------- |
| admin | [Want](js-apis-app-ability-want.md) | Yes   | Device administrator application.|
| callback | AsyncCallback\<boolean> | Yes| Callback used to return the result. The value **true** means that modification of the system time is disabled, and **false** means the opposite.|

**Error codes**

For details about the error codes, see [Enterprise Device Management Error Codes](../errorcodes/errorcode-enterpriseDeviceManager.md).

| ID| Error Message                                                                     |
| ------- | ---------------------------------------------------------------------------- |
| 9200001 | the application is not an administrator of the device.                       |
| 9200002 | the administrator application does not have permission to manage the device. |

**Example**

```js
let wantTemp = {
    bundleName: "bundleName",
    abilityName: "abilityName",
};
dateTimeManager.isModifyDateTimeDisallowed(wantTemp, (error) => {
    if (error) {
        console.log("error code:" + error.code + " error message:" + error.message);
    }
})
```

## dateTimeManager.isModifyDateTimeDisallowed<sup>10+</sup>

isModifyDateTimeDisallowed(admin: Want): Promise\<boolean>

Checks whether modification of the system time is disabled. This API uses a promise to return the result.

**Required permissions**: ohos.permission.ENTERPRISE_SET_DATETIME

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name  | Type                                 | Mandatory  | Description     |
| ----- | ----------------------------------- | ---- | ------- |
| admin | [Want](js-apis-app-ability-want.md) | Yes   | Device administrator application.|

**Return value**

| Type  | Description                                 |
| ----- | ----------------------------------- |
| Promise\<boolean> | Promise Promise used to return the result. The value **true** means that modification of the system time is disabled, and **false** means the opposite.|

**Error codes**

For details about the error codes, see [Enterprise Device Management Error Codes](../errorcodes/errorcode-enterpriseDeviceManager.md).

| ID| Error Message                                                                     |
| ------- | ---------------------------------------------------------------------------- |
| 9200001 | the application is not an administrator of the device.                        |
| 9200002 | the administrator application does not have permission to manage the device. |

**Example**

```js
let wantTemp = {
    bundleName: "bundleName",
    abilityName: "abilityName",
};
dateTimeManager.disallowModifyDateTime(wantTemp).then(() => {
}).catch((error) => {
    console.log("error code:" + error.code + " error message:" + error.message);
})
```
