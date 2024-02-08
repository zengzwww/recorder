# TensorRT

## Debug NaN or Inf

Get a fp16 ONNX model first:
```bash
polygraphy convert --fp-to-fp16 -o ./data/weights/inswapper_128_fp16.onnx ./data/weights/inswapper_128.onnx 
```

Detect NaN or Inf:
```bash
polygraphy run data/weights/inswapper_128_fp16.onnx --onnx-outputs mark all --onnxrt --validate --log-file nan.log
```

take Inswapper_128.onnx as example:
```text
onnx::ReduceMean_162	ReduceMean_66		Add_68		Sqrt_69	Mul_65		Div_71
onnx::ReduceMean_216	ReduceMean_111	1	Mul_110	Div_116
onnx::Add_217		Add_113
onnx::Sqrt_219		Sqrt_114
onnx::ReduceMean_270	ReduceMean_156	2	Mul_155	Div_161
onnx::Add_271		Add_158
onnx::Sqrt_273		Sqrt_159
onnx::ReduceMean_324	ReduceMean_201	3	Mul_200	Div_206
onnx::Add_325		Add_203
onnx::Sqrt_327		Sqrt_204
onnx::ReduceMean_378	ReduceMean_246	4	Mul_245	Div_251
onnx::Add_379		Add_248
onnx::Sqrt_381		Sqrt_249
onnx::ReduceMean_432	ReduceMean_291		Add_293	Sqrt_294	Mul_290	Div_296
onnx::ReduceMean_486	ReduceMean_336	5	Mul_335	Div_341
onnx::Add_487		Add_338
onnx::Sqrt_489		Sqrt_339
onnx::ReduceMean_540	ReduceMean_381		Add_383	Sqrt_384	Mul_380	Div_386
onnx::ReduceMean_594	ReduceMean_426	6	Mul_425	Div_431
onnx::Add_595		Add_428
onnx::Sqrt_597		Sqrt_429
onnx::ReduceMean_648	ReduceMean_471		Add_473	Sqrt_474	Mul_470	Div_476
onnx::ReduceMean_702	ReduceMean_516	7	Mul_515	Div_521
onnx::Add_703		Add_518
onnx::Sqrt_705		Sqrt_519
onnx::ReduceMean_756	ReduceMean_561		Add_563	Sqrt_564	Mul_560	Div_566
```
