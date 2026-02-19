# Xcode-Accessible Input/Output For RealESRGAN

Use this command to generate a model with stable, readable Core ML feature names for Xcode:

```bash
python slim_architecture.py \
  --num-blocks 12 \
  --post pal4 \
  --deployment-target iOS16 \
  --input-name inputTensor \
  --output-name outputTensor \
  -o RealESRGAN_x4_arch_b12_xcode.mlpackage
```

Output model created in this repo:

- `RealESRGAN_x4_arch_b12_xcode_pal4.mlpackage`
- Input: `inputTensor` (`MLMultiArray`, shape `[1, 3, 256, 256]`)
- Output: `outputTensor` (`MLMultiArray`, shape `[1, 3, 1024, 1024]`)

## iPhone presets (lighter / faster)

Fast preset (recommended first for iPhone):

```bash
python slim_architecture.py \
  --num-blocks 8 \
  --num-feat 48 \
  --num-grow-ch 24 \
  --post quant8 \
  --deployment-target iOS16 \
  --input-name inputTensor \
  --output-name outputTensor \
  -o RealESRGAN_x4_iphone_fast.mlpackage
```

Generated: `RealESRGAN_x4_iphone_fast_quant8.mlpackage` (~3.5 MB)

Ultra-light preset (smallest, biggest quality drop):

```bash
python slim_architecture.py \
  --num-blocks 6 \
  --num-feat 40 \
  --num-grow-ch 20 \
  --post pal4 \
  --deployment-target iOS16 \
  --input-name inputTensor \
  --output-name outputTensor \
  -o RealESRGAN_x4_iphone_ultralite.mlpackage
```

Generated: `RealESRGAN_x4_iphone_ultralite_pal4.mlpackage` (~1.1 MB)

## Batch test all model outputs with one image

Run every model on the same input and save one PNG per model:

```bash
python compare_models.py \
  --image 01169-3398297000.png \
  --models "RealESRGAN_x4*.mlpackage" \
  --out-dir model_outputs
```

This creates:

- `model_outputs/RealESRGAN_x4_*.png` (one output image per model)

Then compare visually in Finder/Preview.

By default this uses tiled full-image inference (`--inference-mode tile4x`), so
saved output resolution is approximately `original_width*4 x original_height*4`.

If you want old single-pass resized behavior, use:

```bash
--inference-mode single --resize-mode fit
```

## Batch test anime2sketch variants

Run the same test flow on all anime2sketch model packages:

```bash
python compare_models.py \
  --image 01169-3398297000.png \
  --models "anime2sketch*.mlpackage" \
  --out-dir model_outputs_anime
```

For anime2sketch, output is same-scale (about `1x`), not `4x`.

Current generated anime2sketch variants in this repo:

- `anime2sketch.mlpackage` (~208 MB)
- `anime2sketch_xcode_quant8.mlpackage` (~52 MB)
- `anime2sketch_xcode_lut6.mlpackage` (~39 MB)
- `anime2sketch_xcode_lut4.mlpackage` (~26 MB)

You can still use one-pass behavior:

```bash
python compare_models.py \
  --image 01169-3398297000.png \
  --models "anime2sketch*.mlpackage" \
  --out-dir model_outputs_anime_single \
  --inference-mode single --resize-mode fit
```

For sharper black-and-white sketches with less jagged pixelation:

```bash
python compare_models.py \
  --image 01169-3398297000.png \
  --models "anime2sketch_xcode_{lut4,lut6,quant8}.mlpackage" \
  --out-dir model_outputs_anime_hybrid_bw \
  --bw-enhance --bw-depixel 1.2 --bw-sharpness 1.1 --bw-threshold 170
```

To merge the 3 model outputs into one image (darkest black from each is kept):

```bash
python compare_models.py \
  --image 01169-3398297000.png \
  --models "anime2sketch_xcode_{lut4,lut6,quant8}.mlpackage" \
  --out-dir model_outputs_anime_hybrid_bw \
  --bw-enhance --bw-depixel 1.2 --bw-sharpness 1.1 --bw-threshold 170 \
  --overlay-black --overlay-name anime2sketch_overlay_black.png --overlay-threshold 170
```

To chain that merged sketch into `RealESRGAN_x4_quant8` in one run:

```bash
python compare_models.py \
  --image 01169-3398297000.png \
  --models "anime2sketch_xcode_{lut4,lut6,quant8}.mlpackage" \
  --out-dir model_outputs_anime_chain \
  --bw-enhance --bw-depixel 1.2 --bw-sharpness 1.1 --bw-threshold 170 \
  --overlay-black --overlay-name anime2sketch_overlay_black.png --overlay-threshold 170 \
  --chain-upscale-model RealESRGAN_x4_quant8.mlpackage --chain-source overlay
```

## One fused model (single .mlpackage)

Build one model package that already includes:
- the 3 anime models
- black-overlap merge (darkest pixel wins)
- resize to ESRGAN input
- `RealESRGAN_x4_quant8`

```bash
python build_fused_anime_esrgan_model.py \
  --anime-q4 anime2sketch_xcode_lut4.mlpackage \
  --anime-lut4 anime2sketch_xcode_lut6.mlpackage \
  --anime-hybrid anime2sketch_xcode_quant8.mlpackage \
  --esrgan RealESRGAN_x4_quant8.mlpackage \
  -o anime2sketch_ensemble_overlay_esrgan_one_model.mlpackage
```

Generated model:
- `anime2sketch_ensemble_overlay_esrgan_one_model.mlpackage`
- Input: `inputImage` (`imageType`, `512x512`)
- Output: `outputImage` (`imageType`, `1024x1024`)

If you only want iPhone variants:

```bash
python compare_models.py \
  --image 01169-3398297000.png \
  --models "RealESRGAN_x4_iphone*.mlpackage" \
  --out-dir model_outputs_iphone
```

## Xcode usage (Swift)

```swift
import CoreML

let config = MLModelConfiguration()
config.computeUnits = .all

let model = try RealESRGAN_x4_arch_b12_xcode_pal4(configuration: config)

// 1x3x256x256, Float32, CHW layout, values usually normalized to 0...1.
let input = try MLMultiArray(shape: [1, 3, 256, 256], dataType: .float32)

// Fill `input` here...

let prediction = try model.prediction(inputTensor: input)
let output = prediction.outputTensor  // shape: [1, 3, 1024, 1024]
```

## Important

- Channel order is `C,H,W` (not HWC).
- Input tensor must match shape exactly: `[1,3,256,256]`.
- Output tensor is `[1,3,1024,1024]`.
