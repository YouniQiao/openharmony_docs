# ServiceExtensionContext

The **ServiceExtensionContext** module, inherited from **ExtensionContext**, provides context for Service Extension abilities.

You can use the APIs of this module to start, terminate, connect, and disconnect abilities.

> **NOTE**
> 
>  - The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.
>  - The APIs of this module can be used only in the stage model.

## Usage

Before using the **ServiceExtensionContext** module, you must define a child class that inherits from **ServiceExtensionAbility**.

```ts
  import ServiceExtensionAbility from '@ohos.app.ability.ServiceExtensionAbility';

  let context = undefined;
  class MainAbility extends ServiceExtensionAbility {
    onCreate() {
      context = this.context;
    }
  }
```

## ServiceExtensionContext.startAbility

startAbility(want: Want, callback: AsyncCallback&lt;void&gt;): void;

Starts an ability. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

  | Name| Type| Mandatory| Description| 
  | -------- | -------- | -------- | -------- |
  | want | [Want](js-apis-application-Want.md)  | Yes| Want information about the target ability, such as the ability name and bundle name.| 
  | callback | AsyncCallback&lt;void&gt; | Yes| Callback used to return the result.| 

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 401 | Invalid input parameter. |
| Other IDs| See [Ability Error Codes](../errorcodes/errorcode-ability.md).|

**Example**

  ```ts
  var want = {
    bundleName: "com.example.myapp",
    abilityName: "MyAbility"
  };

  try {
    this.context.startAbility(want, (error) => {
      if (error.code) {
        // Process service logic errors.
        console.log('startAbility failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
        return;
      }
      // Carry out normal service processing.
      console.log('startAbility succeed');
    });
  } catch (paramError) {
    // Process input parameter errors.
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## ServiceExtensionContext.startAbility

startAbility(want: Want, options?: StartOptions): Promise\<void>;

Starts an ability. This API uses a promise to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

  | Name| Type| Mandatory| Description| 
  | -------- | -------- | -------- | -------- |
  | want | [Want](js-apis-application-Want.md)  | Yes| Want information about the target ability, such as the ability name and bundle name.| 
  | options | [StartOptions](js-apis-application-StartOptions.md) | No| Parameters used for starting the ability.|

**Return value**

  | Type| Description| 
  | -------- | -------- |
  | Promise&lt;void&gt; | Promise used to return the result.| 

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 401 | Invalid input parameter. |
| Other IDs| See [Ability Error Codes](../errorcodes/errorcode-ability.md).|

**Example**

  ```ts
  var want = {
    bundleName: "com.example.myapp",
    abilityName: "MyAbility"
  };
  var options = {
  	windowMode: 0,
  };

  try {
    this.context.startAbility(want, options)
      .then((data) => {
        // Carry out normal service processing.
        console.log('startAbility succeed');
      })
      .catch((error) => {
        // Process service logic errors.
        console.log('startAbility failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
      });
  } catch (paramError) {
    // Process input parameter errors.
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## ServiceExtensionContext.startAbility

startAbility(want: Want, options: StartOptions, callback: AsyncCallback&lt;void&gt;): void

Starts an ability with the start options specified. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-Want.md)  | Yes| Want information about the target ability.|
| options | [StartOptions](js-apis-application-StartOptions.md) | Yes| Parameters used for starting the ability.|
| callback | AsyncCallback&lt;void&gt; | Yes| Callback used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 401 | Invalid input parameter. |
| Other IDs| See [Ability Error Codes](../errorcodes/errorcode-ability.md).|

**Example**

  ```ts
  var want = {
    deviceId: "",
    bundleName: "com.extreme.test",
    abilityName: "MainAbility"
  };
  var options = {
    windowMode: 0
  };

  try {
    this.context.startAbility(want, options, (error) => {
      if (error.code) {
        // Process service logic errors.
        console.log('startAbility failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
        return;
      }
      // Carry out normal service processing.
      console.log('startAbility succeed');
    });
  } catch (paramError) {
    // Process input parameter errors.
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## ServiceExtensionContext.startAbilityWithAccount

startAbilityWithAccount(want: Want, accountId: number, callback: AsyncCallback\<void>): void;

Starts an ability with the account ID specified. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-Want.md) | Yes| Want information about the target ability.|
| accountId | number | Yes| ID of a system account. For details, see [getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess).|
| callback | AsyncCallback\<void\> | Yes| Callback used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 401 | Invalid input parameter. |
| Other IDs| See [Ability Error Codes](../errorcodes/errorcode-ability.md).|

**Example**

  ```ts
  var want = {
    deviceId: "",
    bundleName: "com.extreme.test",
    abilityName: "MainAbility"
  };
  var accountId = 100;

  try {
    this.context.startAbilityWithAccount(want, accountId, (error) => {
      if (error.code) {
        // Process service logic errors.
        console.log('startAbilityWithAccount failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
        return;
      }
      // Carry out normal service processing.
      console.log('startAbilityWithAccount succeed');
    });
  } catch (paramError) {
    // Process input parameter errors.
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## ServiceExtensionContext.startAbilityWithAccount

startAbilityWithAccount(want: Want, accountId: number, options: StartOptions, callback: AsyncCallback\<void\>): void;

Starts an ability with the account ID and start options specified. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-Want.md) | Yes| Want information about the target ability.|
| accountId | number | Yes| ID of a system account. For details, see [getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess).|
| options | [StartOptions](js-apis-application-StartOptions.md) | Yes| Parameters used for starting the ability.|
| callback | AsyncCallback\<void\> | Yes| Callback used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 401 | Invalid input parameter. |
| Other IDs| See [Ability Error Codes](../errorcodes/errorcode-ability.md).|

**Example**

  ```ts
  var want = {
    deviceId: "",
    bundleName: "com.extreme.test",
    abilityName: "MainAbility"
  };
  var accountId = 100;
  var options = {
    windowMode: 0
  };

  try {
    this.context.startAbilityWithAccount(want, accountId, options, (error) => {
      if (error.code) {
        // Process service logic errors.
        console.log('startAbilityWithAccount failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
        return;
      }
      // Carry out normal service processing.
      console.log('startAbilityWithAccount succeed');
    });
  } catch (paramError) {
    // Process input parameter errors.
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```


## ServiceExtensionContext.startAbilityWithAccount

startAbilityWithAccount(want: Want, accountId: number, options?: StartOptions): Promise\<void>;

Starts an ability with the account ID specified. This API uses a promise to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-Want.md) | Yes| Want information about the target ability.|
| accountId | number | Yes| ID of a system account. For details, see [getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess).|
| options | [StartOptions](js-apis-application-StartOptions.md) | No| Parameters used for starting the ability.|

**Return value**

  | Type| Description| 
  | -------- | -------- |
  | Promise&lt;void&gt; | Promise used to return the result.| 

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 401 | Invalid input parameter. |
| Other IDs| See [Ability Error Codes](../errorcodes/errorcode-ability.md).|

**Example**

  ```ts
  var want = {
    deviceId: "",
    bundleName: "com.extreme.test",
    abilityName: "MainAbility"
  };
  var accountId = 100;
  var options = {
    windowMode: 0
  };

  try {
    this.context.startAbilityWithAccount(want, accountId, options)
      .then((data) => {
        // Carry out normal service processing.
        console.log('startAbilityWithAccount succeed');
      })
      .catch((error) => {
        // Process service logic errors.
        console.log('startAbilityWithAccount failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
      });
  } catch (paramError) {
    // Process input parameter errors.
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## ServiceExtensionContext.startServiceExtensionAbility

startServiceExtensionAbility(want: Want, callback: AsyncCallback\<void>): void;

Starts a new Service Extension ability. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-Want.md) | Yes| Want information about the target ability.|
| callback | AsyncCallback\<void\> | Yes| Callback used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 401 | Invalid input parameter. |
| Other IDs| See [Ability Error Codes](../errorcodes/errorcode-ability.md).|

**Example**

  ```ts
  var want = {
    deviceId: "",
    bundleName: "com.extreme.test",
    abilityName: "MainAbility"
  };

  try {
    this.context.startServiceExtensionAbility(want, (error) => {
      if (error.code) {
        // Process service logic errors.
        console.log('startServiceExtensionAbility failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
        return;
      }
      // Carry out normal service processing.
      console.log('startServiceExtensionAbility succeed');
    });
  } catch (paramError) {
    // Process input parameter errors.
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## ServiceExtensionContext.startServiceExtensionAbility

startServiceExtensionAbility(want: Want): Promise\<void>;

Starts a new Service Extension ability. This API uses a promise to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-Want.md) | Yes| Want information about the target ability.|

**Return value**

  | Type| Description| 
  | -------- | -------- |
  | Promise&lt;void&gt; | Promise used to return the result.| 

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 401 | Invalid input parameter. |
| Other IDs| See [Ability Error Codes](../errorcodes/errorcode-ability.md).|

**Example**

  ```ts
  var want = {
    deviceId: "",
    bundleName: "com.extreme.test",
    abilityName: "MainAbility"
  };

  try {
    this.context.startServiceExtensionAbility(want)
      .then((data) => {
        // Carry out normal service processing.
        console.log('startServiceExtensionAbility succeed');
      })
      .catch((error) => {
        // Process service logic errors.
        console.log('startServiceExtensionAbility failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
      });
  } catch (paramError) {
    // Process input parameter errors.
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## ServiceExtensionContext.startServiceExtensionAbilityWithAccount

startServiceExtensionAbilityWithAccount(want: Want, accountId: number, callback: AsyncCallback\<void>): void;

Starts a new Service Extension ability with the account ID specified. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-Want.md) | Yes| Want information about the target ability.|
| accountId | number | Yes| ID of a system account. For details, see [getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess).|
| callback | AsyncCallback\<void\> | Yes| Callback used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 401 | Invalid input parameter. |
| Other IDs| See [Ability Error Codes](../errorcodes/errorcode-ability.md).|


**Example**

  ```ts
  var want = {
    deviceId: "",
    bundleName: "com.extreme.test",
    abilityName: "MainAbility"
  };
  var accountId = 100;

  try {
    this.context.startServiceExtensionAbilityWithAccount(want, accountId, (error) => {
      if (error.code) {
        // Process service logic errors.
        console.log('startServiceExtensionAbilityWithAccount failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
        return;
      }
      // Carry out normal service processing.
      console.log('startServiceExtensionAbilityWithAccount succeed');
    });
  } catch (paramError) {
    // Process input parameter errors.
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## ServiceExtensionContext.startServiceExtensionAbilityWithAccount

startServiceExtensionAbilityWithAccount(want: Want, accountId: number): Promise\<void>;

Starts a new Service Extension ability with the account ID specified. This API uses a promise to return the result.

**Required permissions**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-Want.md) | Yes| Want information about the target ability.|
| accountId | number | Yes| ID of a system account. For details, see [getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess).|

**Return value**

  | Type| Description| 
  | -------- | -------- |
  | Promise&lt;void&gt; | Promise used to return the result.| 

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 401 | Invalid input parameter. |
| Other IDs| See [Ability Error Codes](../errorcodes/errorcode-ability.md).|

**Example**

  ```ts
  var want = {
    deviceId: "",
    bundleName: "com.extreme.test",
    abilityName: "MainAbility"
  };
  var accountId = 100;

  try {
    this.context.startServiceExtensionAbilityWithAccount(want, accountId)
      .then((data) => {
        // Carry out normal service processing.
        console.log('startServiceExtensionAbilityWithAccount succeed');
      })
      .catch((error) => {
        // Process service logic errors.
        console.log('startServiceExtensionAbilityWithAccount failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
      });
  } catch (paramError) {
    // Process input parameter errors.
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## ServiceExtensionContext.stopServiceExtensionAbility

stopServiceExtensionAbility(want: Want, callback: AsyncCallback\<void>): void;

Stops a Service Extension ability in the same application. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-Want.md) | Yes| Want information about the target ability.|
| callback | AsyncCallback\<void\> | Yes| Callback used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 401 | Invalid input parameter. |
| Other IDs| See [Ability Error Codes](../errorcodes/errorcode-ability.md).|

**Example**

  ```ts
  var want = {
    deviceId: "",
    bundleName: "com.extreme.test",
    abilityName: "MainAbility"
  };

  try {
    this.context.stopServiceExtensionAbility(want, (error) => {
      if (error.code) {
        // Process service logic errors.
        console.log('stopServiceExtensionAbility failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
        return;
      }
      // Carry out normal service processing.
      console.log('stopServiceExtensionAbility succeed');
    });
  } catch (paramError) {
    // Process input parameter errors.
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## ServiceExtensionContext.stopServiceExtensionAbility

stopServiceExtensionAbility(want: Want): Promise\<void>;

Stops a Service Extension ability in the same application. This API uses a promise to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-Want.md) | Yes| Want information about the target ability.|

**Return value**

  | Type| Description| 
  | -------- | -------- |
  | Promise&lt;void&gt; | Promise used to return the result.| 

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 401 | Invalid input parameter. |
| Other IDs| See [Ability Error Codes](../errorcodes/errorcode-ability.md).|

**Example**

  ```ts
  var want = {
    deviceId: "",
    bundleName: "com.extreme.test",
    abilityName: "MainAbility"
  };

  try {
    this.context.stopServiceExtensionAbility(want)
      .then((data) => {
        // Carry out normal service processing.
        console.log('stopServiceExtensionAbility succeed');
      })
      .catch((error) => {
        // Process service logic errors.
        console.log('stopServiceExtensionAbility failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
      });
  } catch (paramError) {
    // Process input parameter errors.
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## ServiceExtensionContext.stopServiceExtensionAbilityWithAccount

stopServiceExtensionAbilityWithAccount(want: Want, accountId: number, callback: AsyncCallback\<void>): void;

Stops a Service Extension ability in the same application with the account ID specified. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-Want.md) | Yes| Want information about the target ability.|
| accountId | number | Yes| ID of a system account. For details, see [getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess).|
| callback | AsyncCallback\<void\> | Yes| Callback used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 401 | Invalid input parameter. |
| Other IDs| See [Ability Error Codes](../errorcodes/errorcode-ability.md).|

**Example**

  ```ts
  var want = {
    deviceId: "",
    bundleName: "com.extreme.test",
    abilityName: "MainAbility"
  };
  var accountId = 100;

  try {
    this.context.stopServiceExtensionAbilityWithAccount(want, accountId, (error) => {
      if (error.code) {
        // Process service logic errors.
        console.log('stopServiceExtensionAbilityWithAccount failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
        return;
      }
      // Carry out normal service processing.
      console.log('stopServiceExtensionAbilityWithAccount succeed');
    });
  } catch (paramError) {
    // Process input parameter errors.
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## ServiceExtensionContext.stopServiceExtensionAbilityWithAccount

stopServiceExtensionAbilityWithAccount(want: Want, accountId: number): Promise\<void>;

Stops a Service Extension ability in the same application with the account ID specified. This API uses a promise to return the result.

**Required permissions**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-Want.md) | Yes| Want information about the target ability.|
| accountId | number | Yes| ID of a system account. For details, see [getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess).|

**Return value**

  | Type| Description| 
  | -------- | -------- |
  | Promise&lt;void&gt; | Promise used to return the result.| 

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 401 | Invalid input parameter. |
| Other IDs| See [Ability Error Codes](../errorcodes/errorcode-ability.md).|

**Example**

  ```ts
  var want = {
    deviceId: "",
    bundleName: "com.extreme.test",
    abilityName: "MainAbility"
  };
  var accountId = 100;

  try {
    this.context.stopServiceExtensionAbilityWithAccount(want, accountId)
      .then((data) => {
        // Carry out normal service processing.
        console.log('stopServiceExtensionAbilityWithAccount succeed');
      })
      .catch((error) => {
        // Process service logic errors.
        console.log('stopServiceExtensionAbilityWithAccount failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
      });
  } catch (paramError) {
    // Process input parameter errors.
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## ServiceExtensionContext.terminateSelf

terminateSelf(callback: AsyncCallback&lt;void&gt;): void;

Terminates this ability. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

  | Name| Type| Mandatory| Description| 
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;void&gt; | Yes| Callback used to return the result.| 

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 401 | Invalid input parameter. |
| Other IDs| See [Ability Error Codes](../errorcodes/errorcode-ability.md).|

**Example**

  ```ts
  this.context.terminateSelf((error) => {
    if (error.code) {
      // Process service logic errors.
      console.log('terminateSelf failed, error.code: ' + JSON.stringify(error.code) +
        ' error.message: ' + JSON.stringify(error.message));
      return;
    }
    // Carry out normal service processing.
    console.log('terminateSelf succeed');
  });
  ```

## ServiceExtensionContext.terminateSelf

terminateSelf(): Promise&lt;void&gt;;

Terminates this ability. This API uses a promise to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Return value**

  | Type| Description| 
  | -------- | -------- |
  | Promise&lt;void&gt; | Promise used to return the result.| 

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 401 | Invalid input parameter. |
| Other IDs| See [Ability Error Codes](../errorcodes/errorcode-ability.md).|

**Example**

  ```ts
  this.context.terminateSelf().then((data) => {
    // Carry out normal service processing.
    console.log('terminateSelf succeed');
  }).catch((error) => {
    // Process service logic errors.
    console.log('terminateSelf failed, error.code: ' + JSON.stringify(error.code) +
      ' error.message: ' + JSON.stringify(error.message));
  });
  ```

## ServiceExtensionContext.connectServiceExtensionAbility

connectServiceExtensionAbility(want: Want, options: ConnectOptions): number;

Connects this ability to a Service ability.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

  | Name| Type| Mandatory| Description| 
  | -------- | -------- | -------- | -------- |
  | want | [Want](js-apis-application-Want.md)  | Yes| Want information about the target ability, such as the ability name and bundle name.| 
  | options | [ConnectOptions](js-apis-featureAbility.md#connectoptions) | Yes| Callback used to return the information indicating that the connection is successful, interrupted, or failed.| 

**Return value**

  | Type| Description| 
  | -------- | -------- |
  | number | A number, based on which the connection will be interrupted.| 

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 401 | Invalid input parameter. |
| Other IDs| See [Ability Error Codes](../errorcodes/errorcode-ability.md).|

**Example**

  ```ts
  var want = {
    bundleName: "com.example.myapp",
    abilityName: "MyAbility"
  };
  var options = {
    onConnect(elementName, remote) { console.log('----------- onConnect -----------') },
    onDisconnect(elementName) { console.log('----------- onDisconnect -----------') },
    onFailed(code) { console.log('----------- onFailed -----------') }
  }

  var connection = null;
  try {
    connection = this.context.connectServiceExtensionAbility(want, options);
  } catch (paramError) {
    // Process input parameter errors.
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## ServiceExtensionContext.connectServiceExtensionAbilityWithAccount

connectServiceExtensionAbilityWithAccount(want: Want, accountId: number, options: ConnectOptions): number;

Uses the **AbilityInfo.AbilityType.SERVICE** template and account ID to connect this ability to another ability.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-Want.md) | Yes| Want information about the target ability.|
| accountId | number | Yes| ID of a system account. For details, see [getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess).|
| options | ConnectOptions | Yes| Remote object instance.|

**Return value**

| Type| Description|
| -------- | -------- |
| number | Result code of the ability connection.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 401 | Invalid input parameter. |
| Other IDs| See [Ability Error Codes](../errorcodes/errorcode-ability.md).|

**Example**

  ```ts
  var want = {
    deviceId: "",
    bundleName: "com.extreme.test",
    abilityName: "MainAbility"
  };
  var accountId = 100;
  var options = {
    onConnect(elementName, remote) { console.log('----------- onConnect -----------') },
    onDisconnect(elementName) { console.log('----------- onDisconnect -----------') },
    onFailed(code) { console.log('----------- onFailed -----------') }
  }

  var connection = null;
  try {
    connection = this.context.connectServiceExtensionAbilityWithAccount(want, accountId, options);
  } catch (paramError) {
    // Process input parameter errors.
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## ServiceExtensionContext.disconnectServiceExtensionAbility

disconnectServiceExtensionAbility(connection: number, callback:AsyncCallback&lt;void&gt;): void;

Disconnects this ability from the Service ability. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

  | Name| Type| Mandatory| Description| 
  | -------- | -------- | -------- | -------- |
  | connection | number | Yes| Number returned after **connectAbility** is called.| 
  | callback | AsyncCallback&lt;void&gt; | Yes| Callback used to return the result.| 

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 401 | Invalid input parameter. |
| Other IDs| See [Ability Error Codes](../errorcodes/errorcode-ability.md).|

**Example**

  ```ts
  // connection is the return value of connectServiceExtensionAbility.
  var connection = 1;

  try {
    this.context.disconnectServiceExtensionAbility(connection, (error) => {
      if (error.code) {
        // Process service logic errors.
        console.log('disconnectServiceExtensionAbility failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
        return;
      }
      // Carry out normal service processing.
      console.log('disconnectServiceExtensionAbility succeed');
    });
  } catch (paramError) {
    // Process input parameter errors.
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## ServiceExtensionContext.disconnectServiceExtensionAbility

disconnectServiceExtensionAbility(connection: number): Promise&lt;void&gt;;

Disconnects this ability from the Service ability. This API uses a promise to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

  | Name| Type| Mandatory| Description| 
  | -------- | -------- | -------- | -------- |
  | connection | number | Yes| Number returned after **connectAbility** is called.| 

**Return value**

  | Type| Description| 
  | -------- | -------- |
  | Promise&lt;void&gt; | Promise used to return the result.| 

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 401 | Invalid input parameter. |
| Other IDs| See [Ability Error Codes](../errorcodes/errorcode-ability.md).|

**Example**

  ```ts
  // connection is the return value of connectAbility.
  var connection = 1;

  try {
    this.context.disconnectServiceExtensionAbility(connection)
      .then((data) => {
        // Carry out normal service processing.
        console.log('disconnectServiceExtensionAbility succeed');
      })
      .catch((error) => {
        // Process service logic errors.
        console.log('disconnectServiceExtensionAbility failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
      });
  } catch (paramError) {
    // Process input parameter errors.
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## ServiceExtensionContext.startAbilityByCall

startAbilityByCall(want: Want): Promise&lt;Caller&gt;;

Starts an ability in the foreground or background and obtains the caller object for communicating with the ability.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-Want.md) | Yes| Information about the ability to start, including **abilityName**, **moduleName**, **bundleName**, **deviceId** (optional), and **parameters** (optional). If **deviceId** is left blank or null, the local ability is started. If **parameters** is left blank or null, the ability is started in the background.|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;Caller&gt; | Promise used to return the caller object to communicate with.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 401 | Invalid input parameter. |
| Other IDs| See [Ability Error Codes](../errorcodes/errorcode-ability.md).|

**Example**

  Start an ability in the background.

  ```ts
  var caller = undefined;

  // Start an ability in the background by not passing parameters.
  var wantBackground = {
      bundleName: "com.example.myservice",
      moduleName: "entry",
      abilityName: "MainAbility",
      deviceId: ""
  };

  try {
    this.context.startAbilityByCall(wantBackground)
      .then((obj) => {
        // Carry out normal service processing.
        caller = obj;
        console.log('startAbilityByCall succeed');
      }).catch((error) => {
        // Process service logic errors.
        console.log('startAbilityByCall failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
      });
  } catch (paramError) {
    // Process input parameter errors.
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

  Start an ability in the foreground.

  ```ts
  var caller = undefined;

  // Start an ability in the foreground with ohos.aafwk.param.callAbilityToForeground in parameters set to true.
  var wantForeground = {
      bundleName: "com.example.myservice",
      moduleName: "entry",
      abilityName: "MainAbility",
      deviceId: "",
      parameters: {
        "ohos.aafwk.param.callAbilityToForeground": true
      }
  };

  try {
    this.context.startAbilityByCall(wantForeground)
      .then((obj) => {
        // Carry out normal service processing.
        caller = obj;
        console.log('startAbilityByCall succeed');
      }).catch((error) => {
        // Process service logic errors.
        console.log('startAbilityByCall failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
      });
  } catch (paramError) {
    // Process input parameter errors.
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```
  