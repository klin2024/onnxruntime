## Operators Support Table

The following table shows ONNX
operators and the supported opset domain/versions in **WebNN EP** by ONNX Runtime Web. For example,
`7-12, 13+` means ONNX Runtime Web currently supports opset version 7 to 12, 13 and above.

(**Note**: ONNX Runtime only *guarantees* support for models stamped with opset version 7 or above for opset domain 'ai.onnx'.)

[WebNN API](https://webmachinelearning.github.io/webnn) provides two device types `cpu` and `gpu` to leverage different on-device accelerators. WebNN API implementation in Chromium uses TFLite XNNPack delegate backend for `cpu` device type and DirectML backend for `gpu` device type. [The op support status](https://webmachinelearning.github.io/webnn-status/) behind these two backends is inconsistent.


| Operator | Opset | WebNN API | WebNN CPU | WebNN GPU | Comments |
|:------:|:------:|:------:|:-:|:-:|:------|
| Abs | ai.onnx(7-12, 13+) | abs | ✓ | ✓ | |
| Add | ai.onnx(7-12, 13, 14+) | add | ✓ | ✓ | |
| ArgMax | ai.onnx(7-10, 11, 12, 13+) | argMax | ✓ | ✓ | |
| ArgMin | ai.onnx(7-10, 11, 12, 13+) | argMin | ✓ | ✓ | |
| AveragePool | ai.onnx(7-9, 10, 11, 12-18, 19+) | averagePool2d | ✓ | ✓ | Only supports 4-D input, 2-D 'kernel_shape', 'count_include_pad' value is 0 |
| BatchNormalization | ai.onnx(7-8, 9-13, 14, 15+) | batchNormalization | ✓ | ✓ | Only supports 'training_mode' value is 0, one output |
| Cast | ai.onnx(7-8, 9-12, 13-18, 19-20, 21+) | cast | ✓ | ✓ | WebNN CPU backend doesn't support casting to uint64 data type |
| Ceil | ai.onnx(7-12, 13+) | ceil | ✓ | ✓ | |
| Clip | ai.onnx(7-10, 11, 12, 13+) | clamp | ✓ | ✓ | WebNN CPU backend only supports 3 specific ranges: [0.0, infinity], [-1.0, 1.0], [0.0, 6.0] (Chromium issue: https://issues.chromium.org/issues/326156496) |
| Concat | ai.onnx(7-10, 11-12, 13+) | concat | ✓ | ✓ | |
| Conv | ai.onnx(7-10, 11+) | conv2d | ✓ | ✓ | Only supports 3-D or 4-D input and 'W' (weight) |
| ConvTranspose | ai.onnx(7-10, 11+) | convTranspose2d | ✓ | ✓ | Only supports 3-D or 4-D input and 'W' (weight). WebNN CPU backend only supports default dilations and group |
| Cos | ai.onnx(7+) | cos | ✓ | ✓ | |
| Div | ai.onnx(7-12, 13, 14+) | div | ✓ | ✓ | |
| DequantizeLinear | ai.onnx(10-12, 13-18, 19-20, 21-22, 23+) | dequantizeLinear | ✗ | ✓ | |
| Dropout | ai.onnx(7-9, 10-11, 12, 13-21, 22+) | identity | ✓ | ✓ | Only supports test mode |
| Elu | ai.onnx(7+) | elu | ✓ | ✓ | WebNN CPU backend only supports 'alpha' value is 1.0 |
| Equal | ai.onnx(7-10, 11-12, 13-18, 19+) | equal | ✓ | ✓ | |
| Erf | ai.onnx(7-9, 10-12, 13+) | erf | ✓ | ✓ | |
| Exp | ai.onnx(7-12, 13+) | exp | ✓ | ✓ | |
| Expand | ai.onnx(8-12, 13+) | expand | ✓ | ✓ | 'shape' input should be a constant |
| Flatten | ai.onnx(7-8, 9-10, 11-12, 13-20, 21+) | reshape | ✓ | ✓ | |
| Floor | ai.onnx(7-12, 13+) | floor | ✓ | ✓ | |
| Gather | ai.onnx(7-10, 11-12, 13+) | gather | ✓ | ✓ | |
| Gelu | ai.onnx(20+) | gelu | ✓ | ✓ | |
| Gemm | ai.onnx(7-8, 9-10, 11-12, 13+) | gemm | ✓ | ✓ | Only supports 1-D 'C' input |
| GlobalAveragePool | ai.onnx(7+) | averagePool2d | ✓ | ✓ | Only supports 4-D input |
| GlobalMaxPool | ai.onnx(7+) | maxPool2d | ✓ | ✓ | Only supports 4-D input |
| GlobalLpPool| ai.onnx(7+) | l2Pool2d | ✗ | ✓ | Only supports 4-D input, 'p' value is 2 |
| Greater | ai.onnx(7-8, 9-12, 13+) | greater | ✓ | ✓ | |
| GreaterOrEqual | ai.onnx(12-15, 16+) | greaterOrEqual | ✓ | ✓ | |
| GRU | ai.onnx(7-13, 14-21, 22+) | gru | ✓ | ✓ | Only supports 'layout' == 0. 'clip' is not supported. The activation functions in 'activations' must be one of 'Relu', 'Tanh', 'Sigmoid'. Forward and backward activations must be the same if bidirectional. 'sequence_lens' if present should be constant with values equal to the first dimension length of input 'X' |
| HardSigmoid | ai.onnx(7+) | hardSigmoid | ✓ | ✓ | |
| HardSwish | ai.onnx(14+) | hardSwish | ✓ | ✓ | |
| Identity | ai.onnx(7-13, 14-15, 16-18, 19-20, 21+) | identity | ✓ | ✓ | |
| InstanceNormalization | ai.onnx(7+) | instanceNormalization | ✓ | ✓ | |
| LayerNormalization | ai.onnx(7-16, 17+) | layerNormalization | ✓ | ✓ | |
| LeakyRelu | ai.onnx(7-15, 16+) | leakyRelu | ✓ | ✓ | |
| Less | ai.onnx(7-8, 9-12, 13+) | lesser | ✓ | ✓ | |
| LessOrEqual | ai.onnx(12-15, 16+) | lesserOrEqual | ✓ | ✓ | |
| Log | ai.onnx(7-12, 13+) | log | ✓ | ✓ | |
| LpPool | ai.onnx(7-10, 11-17, 18+) | l2Pool2d | ✗ | ✓ | Only supports 4-D input, 2-D 'kernel_shape', 'p' value is 2 |
| LSTM | ai.onnx(7-13, 14-21, 22+) | lstm | ✓ | ✓ | Only supports 'layout' == 0, 'input_forget' == 0. 'clip' is not supported. The activation functions in 'activations' must be one of 'Relu', 'Tanh', 'Sigmoid'. Forward and backward activations must be the same if bidirectional. 'sequence_lens' if present should be constant with values equal to the first dimension length of input 'X' |
| MatMul | ai.onnx(7-8, 9-12, 13+) | matmul | ✓ | ✓ | |
| Max | ai.onnx(7, 8-11, 12, 13+) | max | ✓ | ✓ | |
| MaxPool | ai.onnx(7, 8-9, 10, 11, 12+) | maxPool2d | ✓ | ✓ | Only supports 4-D input, 2-D 'kernel_shape', 'storage_order' != 1, one output |
| Min | ai.onnx(7, 8-11, 12, 13+) | min | ✓ | ✓ | |
| Mul | ai.onnx(7-12, 13, 14+) | mul | ✓ | ✓ | |
| Neg | ai.onnx(7-12, 13+) | neg | ✓ | ✓ | |
| Not | ai.onnx(7+) | logicalnot | ✓ | ✓ | |
| Pad | ai.onnx(7-10, 11-12, 13-17, 18, 19-20, 21+) | pad | ✓ | ✓ | modes == 'wrap' is not supported |
| Pow | ai.onnx(7-11, 12, 13-14, 15+) | pow | ✓ | ✓ | |
| PRelu | ai.onnx(7-8, 9-15, 16+) | prelu | ✓ | ✓ | WebNN CPU backend restricts the last dimension of input and slope to be same (Chromium issue: https://issues.chromium.org/issues/335517470) |
| QuantizeLinear | ai.onnx(10-12, 13-18, 19-20, 21-22, 23+) | quantizeLinear | ✗ | ✓ | |
| Reciprocal | ai.onnx(7-12, 13+) | reciprocal | ✓ | ✓ | |
| ReduceL1 | ai.onnx(7-10, 11-12, 13-17, 18+) | reduceL1 | ✓ | ✓ | Input 'axes' if present should be a constant |
| ReduceL2 | ai.onnx(7-10, 11-12, 13-17, 18+) | reduceL2 | ✓ | ✓ | Input 'axes' if present should be a constant |
| ReduceLogSum| ai.onnx(7-10, 11-12, 13-17, 18+) | reduceLogSum| ✓ | ✓ | Input 'axes' if present should be a constant |
| ReduceLogSumExp | ai.onnx(7-10, 11-12, 13-17, 18+) | reduceLogSumExp | ✓ | ✓ | Input 'axes' if present should be a constant |
| ReduceMax | ai.onnx(7-10, 11, 12, 13-17, 18-19, 20+) | reduceMax | ✓ | ✓ | Input 'axes' if present should be a constant |
| ReduceMean | ai.onnx(7-10, 11-12, 13-17, 18+) | reduceMean | ✓ | ✓ | Input 'axes' if present should be a constant |
| ReduceMin | ai.onnx(7-10, 11, 12, 13-17, 18-19, 20+) | reduceMin | ✓ | ✓ | Input 'axes' if present should be a constant |
| ReduceProd | ai.onnx(7-10, 11-12, 13-17, 18+) | reduceProduct | ✓ | ✓ | Input 'axes' if present should be a constant |
| ReduceSum | ai.onnx(7-10, 11-12, 13+) | reduceSum | ✓ | ✓ | Input 'axes' if present should be a constant |
| ReduceSumSquare | ai.onnx(7-10, 11-12, 13-17, 18+) | reduceSumSquare | ✓ | ✓ | Input 'axes' if present should be a constant |
| Relu | ai.onnx(7-12, 13, 14+) | relu | ✓ | ✓ | |
| Reshape | ai.onnx(7-12, 13, 14-18, 19-20, 21+) | reshape | ✓ | ✓ | Input 'shape' should be a constant, 0 dimension value in 'shape' is not supported |
| Resize | ai.onnx(11-12, 13-17, 18, 19+) | resample2d | ✓ | ✓ | Only supports 4-D input, exclude_outside != 0, input 'scales' and 'sizes' if present must be a constant, 'linear' and 'nearest' modes |
| Shape | ai.onnx(7-12, 13-14, 15-18, 19-20, 21+) | slice | ✓ | ✓ | |
| Sigmoid | ai.onnx(7-12, 13+) | sigmoid | ✓ | ✓ | |
| Softplus | ai.onnx(7+) | softplus | ✓ | ✓ | |
| Softsign | ai.onnx(7+) | softsign | ✓ | ✓ | |
| Sin | ai.onnx(7+) | sin | ✓ | ✓ | |
| Slice | ai.onnx(7-9, 10, 11-12, 13+) | slice | ✓ | ✓ | Input 'starts', 'ends', 'axes', and 'steps' if present must be a constant, only supports 'steps' value 1 |
| Softmax | ai.onnx(7-10, 11-12, 13+) | softmax | ✓ | ✓ | |
| Split | ai.onnx(7-10, 11-12, 13-17, 18+) | split | ✓ | ✓ | Input 'split' if present should be a constant |
| Sqrt | ai.onnx(7-12, 13+) | sqrt | ✓ | ✓ | |
| Squeeze | ai.onnx(7-10, 11-12, 13-20, 21+) | reshape | ✓ | ✓ | Input 'axes' if present should be a constant |
| Sub | ai.onnx(7-12, 13, 14+) | sub | ✓ | ✓ | |
| Tan | ai.onnx(7+) | tan | ✓ | ✓ | |
| Tanh | ai.onnx(7-12, 13+) | tanh | ✓ | ✓ | |
| Tile | ai.onnx(7-12, 13+) | tile | ✗ | ✓ | Input 'repeats' should be a constant |
| Transpose | ai.onnx(7-12, 13-20, 21+) | transpose | ✓ | ✓ | |
| Trilu | ai.onnx(14+) | triangular | ✓ | ✓ | Input 'k' (option 'diagonal' for WebNN) if present should be a constant |
| Unsqueeze | ai.onnx(7-10, 11-12, 13-20, 21+) | reshape | ✓ | ✓ | |
| Where | ai.onnx(7-8, 9-15, 16+) | where | ✓ | ✓ | |
