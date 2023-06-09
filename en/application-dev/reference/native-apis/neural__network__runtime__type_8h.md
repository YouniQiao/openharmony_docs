# neural_network_runtime_type.h


## Overview

Defines the structure and enumeration for Neural Network Runtime.

**Since:**
9

**Related Modules:**

[NeuralNeworkRuntime](_neural_nework_runtime.md)


## Summary


### Structs

| Name | Description | 
| -------- | -------- |
| [OH_NN_UInt32Array](_o_h___n_n___u_int32_array.md) | This structure is used to store a 32-bit unsigned integer array.  | 
| [OH_NN_QuantParam](_o_h___n_n___quant_param.md) | Quantization information.  | 
| [OH_NN_Tensor](_o_h___n_n___tensor.md) | Defines the tensor structure.  | 
| [OH_NN_Memory](_o_h___n_n___memory.md) | Defines the memory structure.  | 


### Types

| Name | Description | 
| -------- | -------- |
| [OH_NNModel](_neural_nework_runtime.md#oh_nnmodel) | Defines the handles of models for Neural Network Runtime.  | 
| [OH_NNCompilation](_neural_nework_runtime.md#oh_nncompilation) | Defines the compiler handle for Neural Network Runtime.  | 
| [OH_NNExecutor](_neural_nework_runtime.md#oh_nnexecutor) | Defines the executor handle for Neural Network Runtime.  | 
| [OH_NN_UInt32Array](_neural_nework_runtime.md#oh_nn_uint32array) | This structure is used to store a 32-bit unsigned integer array.  | 
| [OH_NN_QuantParam](_neural_nework_runtime.md#oh_nn_quantparam) | Quantization information.  | 
| [OH_NN_Tensor](_neural_nework_runtime.md#oh_nn_tensor) | Defines the tensor structure.  | 
| [OH_NN_Memory](_neural_nework_runtime.md#oh_nn_memory) | Defines the memory structure.  | 


### Enums

| Name | Description | 
| -------- | -------- |
| [OH_NN_PerformanceMode](_neural_nework_runtime.md#oh_nn_performancemode) {<br/>OH_NN_PERFORMANCE_NONE = 0, OH_NN_PERFORMANCE_LOW = 1, OH_NN_PERFORMANCE_MEDIUM = 2, OH_NN_PERFORMANCE_HIGH = 3,<br/>OH_NN_PERFORMANCE_EXTREME = 4<br/>} | Defines the hardware performance mode.  | 
| [OH_NN_Priority](_neural_nework_runtime.md#oh_nn_priority) { OH_NN_PRIORITY_NONE = 0, OH_NN_PRIORITY_LOW = 1, OH_NN_PRIORITY_MEDIUM = 2, OH_NN_PRIORITY_HIGH = 3 } | Defines the model inference task priority.  | 
| [OH_NN_ReturnCode](_neural_nework_runtime.md#oh_nn_returncode) {<br/>OH_NN_SUCCESS = 0, OH_NN_FAILED = 1, OH_NN_INVALID_PARAMETER = 2, OH_NN_MEMORY_ERROR = 3,<br/>OH_NN_OPERATION_FORBIDDEN = 4, OH_NN_NULL_PTR = 5, OH_NN_INVALID_FILE = 6, OH_NN_UNAVALIDABLE_DEVICE = 7,<br/>OH_NN_INVALID_PATH = 8<br/>} | Defines error codes for Neural Network Runtime.  | 
| [OH_NN_FuseType](_neural_nework_runtime.md#oh_nn_fusetype) : int8_t { OH_NN_FUSED_NONE = 0, OH_NN_FUSED_RELU = 1, OH_NN_FUSED_RELU6 = 2 } | Defines activation function types in the fusion operator for Neural Network Runtime.  | 
| [OH_NN_Format](_neural_nework_runtime.md#oh_nn_format) { OH_NN_FORMAT_NONE = 0, OH_NN_FORMAT_NCHW = 1, OH_NN_FORMAT_NHWC = 2 } | Defines the layout type of tensor data.  | 
| [OH_NN_DeviceType](_neural_nework_runtime.md#oh_nn_devicetype) { OH_NN_OTHERS = 0, OH_NN_CPU = 1, OH_NN_GPU = 2, OH_NN_ACCELERATOR = 3 } | Defines device types supported by Neural Network Runtime.  | 
| [OH_NN_DataType](_neural_nework_runtime.md#oh_nn_datatype) {<br/>OH_NN_UNKNOWN = 0, OH_NN_BOOL = 1, OH_NN_INT8 = 2, OH_NN_INT16 = 3,<br/>OH_NN_INT32 = 4, OH_NN_INT64 = 5, OH_NN_UINT8 = 6, OH_NN_UINT16 = 7,<br/>OH_NN_UINT32 = 8, OH_NN_UINT64 = 9, OH_NN_FLOAT16 = 10, OH_NN_FLOAT32 = 11,<br/>OH_NN_FLOAT64 = 12<br/>} | Defines tensor data types supported by Neural Network Runtime.  | 
| [OH_NN_OperationType](_neural_nework_runtime.md#oh_nn_operationtype) {<br/>OH_NN_OPS_ADD = 1, OH_NN_OPS_AVG_POOL = 2, OH_NN_OPS_BATCH_NORM = 3, OH_NN_OPS_BATCH_TO_SPACE_ND = 4,<br/>OH_NN_OPS_BIAS_ADD = 5, OH_NN_OPS_CAST = 6, OH_NN_OPS_CONCAT = 7, OH_NN_OPS_CONV2D = 8,<br/>OH_NN_OPS_CONV2D_TRANSPOSE = 9, OH_NN_OPS_DEPTHWISE_CONV2D_NATIVE = 10, OH_NN_OPS_DIV = 11, OH_NN_OPS_ELTWISE = 12,<br/>OH_NN_OPS_EXPAND_DIMS = 13, OH_NN_OPS_FILL = 14, OH_NN_OPS_FULL_CONNECTION = 15, OH_NN_OPS_GATHER = 16,<br/>OH_NN_OPS_HSWISH = 17, OH_NN_OPS_LESS_EQUAL = 18, OH_NN_OPS_MATMUL = 19, OH_NN_OPS_MAXIMUM = 20,<br/>OH_NN_OPS_MAX_POOL = 21, OH_NN_OPS_MUL = 22, OH_NN_OPS_ONE_HOT = 23, OH_NN_OPS_PAD = 24,<br/>OH_NN_OPS_POW = 25, OH_NN_OPS_SCALE = 26, OH_NN_OPS_SHAPE = 27, OH_NN_OPS_SIGMOID = 28,<br/>OH_NN_OPS_SLICE = 29, OH_NN_OPS_SOFTMAX = 30, OH_NN_OPS_SPACE_TO_BATCH_ND = 31, OH_NN_OPS_SPLIT = 32,<br/>OH_NN_OPS_SQRT = 33, OH_NN_OPS_SQUARED_DIFFERENCE = 34, OH_NN_OPS_SQUEEZE = 35, OH_NN_OPS_STACK = 36,<br/>OH_NN_OPS_STRIDED_SLICE = 37, OH_NN_OPS_SUB = 38, OH_NN_OPS_TANH = 39, OH_NN_OPS_TILE = 40,<br/>OH_NN_OPS_TRANSPOSE = 41, OH_NN_OPS_REDUCE_MEAN = 42, OH_NN_OPS_RESIZE_BILINEAR = 43, OH_NN_OPS_RSQRT = 44,<br/>OH_NN_OPS_RESHAPE = 45, OH_NN_OPS_PRELU = 46, OH_NN_OPS_RELU = 47, OH_NN_OPS_RELU6 = 48,<br/>OH_NN_OPS_LAYER_NORM = 49, OH_NN_OPS_REDUCE_PROD = 50, OH_NN_OPS_REDUCE_ALL = 51, OH_NN_OPS_QUANT_DTYPE_CAST = 52,<br/>OH_NN_OPS_TOP_K = 53, OH_NN_OPS_ARG_MAX = 54, OH_NN_OPS_UNSQUEEZE = 55, OH_NN_OPS_GELU = 56<br/>} | Defines operator types supported by Neural Network Runtime.  | 
| [OH_NN_TensorType](_neural_nework_runtime.md#oh_nn_tensortype) {<br/>OH_NN_TENSOR = 0, OH_NN_ADD_ACTIVATIONTYPE = 1, OH_NN_AVG_POOL_KERNEL_SIZE = 2, OH_NN_AVG_POOL_STRIDE = 3,<br/>OH_NN_AVG_POOL_PAD_MODE = 4, OH_NN_AVG_POOL_PAD = 5, OH_NN_AVG_POOL_ACTIVATION_TYPE = 6, OH_NN_BATCH_NORM_EPSILON = 7,<br/>OH_NN_BATCH_TO_SPACE_ND_BLOCKSIZE = 8, OH_NN_BATCH_TO_SPACE_ND_CROPS = 9, OH_NN_CONCAT_AXIS = 10, OH_NN_CONV2D_STRIDES = 11,<br/>OH_NN_CONV2D_PAD = 12, OH_NN_CONV2D_DILATION = 13, OH_NN_CONV2D_PAD_MODE = 14, OH_NN_CONV2D_ACTIVATION_TYPE = 15,<br/>OH_NN_CONV2D_GROUP = 16, OH_NN_CONV2D_TRANSPOSE_STRIDES = 17, OH_NN_CONV2D_TRANSPOSE_PAD = 18, OH_NN_CONV2D_TRANSPOSE_DILATION = 19,<br/>OH_NN_CONV2D_TRANSPOSE_OUTPUT_PADDINGS = 20, OH_NN_CONV2D_TRANSPOSE_PAD_MODE = 21, OH_NN_CONV2D_TRANSPOSE_ACTIVATION_TYPE = 22, OH_NN_CONV2D_TRANSPOSE_GROUP = 23,<br/>OH_NN_DEPTHWISE_CONV2D_NATIVE_STRIDES = 24, OH_NN_DEPTHWISE_CONV2D_NATIVE_PAD = 25, OH_NN_DEPTHWISE_CONV2D_NATIVE_DILATION = 26, OH_NN_DEPTHWISE_CONV2D_NATIVE_PAD_MODE = 27,<br/>OH_NN_DEPTHWISE_CONV2D_NATIVE_ACTIVATION_TYPE = 28, OH_NN_DIV_ACTIVATIONTYPE = 29, OH_NN_ELTWISE_MODE = 30, OH_NN_FULL_CONNECTION_AXIS = 31,<br/>OH_NN_FULL_CONNECTION_ACTIVATIONTYPE = 32, OH_NN_MATMUL_TRANSPOSE_A = 33, OH_NN_MATMUL_TRANSPOSE_B = 34, OH_NN_MATMUL_ACTIVATION_TYPE = 35,<br/>OH_NN_MAX_POOL_KERNEL_SIZE = 36, OH_NN_MAX_POOL_STRIDE = 37, OH_NN_MAX_POOL_PAD_MODE = 38, OH_NN_MAX_POOL_PAD = 39,<br/>OH_NN_MAX_POOL_ACTIVATION_TYPE = 40, OH_NN_MUL_ACTIVATION_TYPE = 41, OH_NN_ONE_HOT_AXIS = 42, OH_NN_PAD_CONSTANT_VALUE = 43,<br/>OH_NN_SCALE_ACTIVATIONTYPE = 44, OH_NN_SCALE_AXIS = 45, OH_NN_SOFTMAX_AXIS = 46, OH_NN_SPACE_TO_BATCH_ND_BLOCK_SHAPE = 47,<br/>OH_NN_SPACE_TO_BATCH_ND_PADDINGS = 48, OH_NN_SPLIT_AXIS = 49, OH_NN_SPLIT_OUTPUT_NUM = 50, OH_NN_SPLIT_SIZE_SPLITS = 51,<br/>OH_NN_SQUEEZE_AXIS = 52, OH_NN_STACK_AXIS = 53, OH_NN_STRIDED_SLICE_BEGIN_MASK = 54, OH_NN_STRIDED_SLICE_END_MASK = 55,<br/>OH_NN_STRIDED_SLICE_ELLIPSIS_MASK = 56, OH_NN_STRIDED_SLICE_NEW_AXIS_MASK = 57, OH_NN_STRIDED_SLICE_SHRINK_AXIS_MASK = 58, OH_NN_SUB_ACTIVATIONTYPE = 59,<br/>OH_NN_REDUCE_MEAN_KEEP_DIMS = 60, OH_NN_RESIZE_BILINEAR_NEW_HEIGHT = 61, OH_NN_RESIZE_BILINEAR_NEW_WIDTH = 62, OH_NN_RESIZE_BILINEAR_PRESERVE_ASPECT_RATIO = 63,<br/>OH_NN_RESIZE_BILINEAR_COORDINATE_TRANSFORM_MODE = 64, OH_NN_RESIZE_BILINEAR_EXCLUDE_OUTSIDE = 65, OH_NN_LAYER_NORM_BEGIN_NORM_AXIS = 66, OH_NN_LAYER_NORM_EPSILON = 67,<br/>OH_NN_LAYER_NORM_BEGIN_PARAM_AXIS = 68, OH_NN_LAYER_NORM_ELEMENTWISE_AFFINE = 69, OH_NN_REDUCE_PROD_KEEP_DIMS = 70, OH_NN_REDUCE_ALL_KEEP_DIMS = 71,<br/>OH_NN_QUANT_DTYPE_CAST_SRC_T = 72, OH_NN_QUANT_DTYPE_CAST_DST_T = 73, OH_NN_TOP_K_SORTED = 74, OH_NN_ARG_MAX_AXIS = 75,<br/>OH_NN_ARG_MAX_KEEPDIMS = 76, OH_NN_UNSQUEEZE_AXIS = 77<br/>} | Enumerates the tensor data types.  | 
