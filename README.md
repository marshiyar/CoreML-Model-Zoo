# CoreML-Model-Zoo

A curated collection of Core ML (`.mlpackage`) models for:
- super-resolution (RealESRGAN)
- denoising (NAFNet)
- colorization (DDColor)
- anime-to-sketch conversion (Anime2Sketch)

All models can be added directly to Xcode projects targeting iOS, iPadOS, macOS, and visionOS.

---

## At a glance

| Family | Task | Folder | Models | Baseline I/O |
| ------ | ---- | ------ | ------ | ------------ |
| RealESRGAN x2 | Super-resolution (2x) | `Models-List/RealESRGAN_x2/` | 5 | `1x3x256x256 -> 1x3x512x512` |
| RealESRGAN x4 | Super-resolution (4x) | `Models-List/RealESRGAN_x4/` | 3 | `1x3x256x256 -> 1x3x1024x1024` |
| NAFNet SIDD width64 | Denoising | `Models-List/NAFNet_SIDD_width64/` | 6 | `1x3x512x512 -> 1x3x512x512` |
| DDColor modelscope 512 | Colorization | `Models-List/DDColor/` | 9 | `gray_rgb:1x3x512x512 -> ab:1x2x512x512` |
| Anime2Sketch | Image-to-image sketching | `Models-List/anime2sketch/` | 4 | `512x512 -> 512x512` |

---

## Quick start

1. Clone or download this repository.
2. Drag the target `.mlpackage` folder into your Xcode app target.
3. Run prediction with Core ML (or compare variants with `Models-List/Scripts/compare_models.py`).
4. Use the section below for model-specific I/O details and sample outputs.

Each model’s license follows its original upstream project (linked in each section).

---

## Contents

- [At a glance](#at-a-glance)
- [Quick start](#quick-start)
- [Variant naming and compatibility](#variant-naming-and-compatibility)
- [Super Resolution (Real-ESRGAN)](#super-resolution-real-esrgan)
- [Image Denoising (NAFNet)](#image-denoising-nafnet)
- [Image Colorization (DDColor)](#image-colorization-ddcolor)
- [Image2Image (Anime2Sketch)](#image2image-anime2sketch)

---

## Variant naming and compatibility

This section reflects the current model filenames in `Models-List/*/*.mlpackage` and the scripts in `Models-List/Scripts/`.


| Pattern / suffix | Meaning |
| ---------------- | ------- |
| `_ios18_...` | iOS 18+ targeted package variant |
| `_lutN` | N-bit LUT compression variant |
| `_palN_kmeans` | N-bit k-means palette/LUT compression |
| `_palN_uniform` | N-bit uniform palette/LUT compression |
| `_quant4` | 4-bit linear quantization |
| `_quant8` | 8-bit linear quantization |
| `_xcode` | Xcode-converted/exported variant naming used in this repo |


Compatibility notes:

- `Models-List/Scripts/compare_models.py` expects single-input/single-output models and supports both `multiArrayType` and `imageType`.
- Variants with `_ios18_` are iOS 18+ packages.
- Local spec-version mapping used in this README: `spec4 -> iOS13+`, `spec6 -> iOS15+`, `spec7 -> iOS16+`, `spec9 -> iOS18+`.

Variant profile shorthand used in tables:

| Profile | Meaning |
| ------- | ------- |
| `base` | Original full-size package, highest fidelity, largest size |
| `quant8` | 8-bit linear quantization, strong size/runtime reduction |
| `quant4` | 4-bit linear quantization, aggressive compression |
| `palN` / `lutN` | Palette/LUT compression at N-bit depth |

---

## Super Resolution (Real-ESRGAN)

Real-world image super-resolution. Original project: [xinntao/Real-ESRGAN](https://github.com/xinntao/Real-ESRGAN) (BSD-3-Clause).

Models live in `Models-List/RealESRGAN_x2/` and `Models-List/RealESRGAN_x4/`.

### RealESRGAN x2

Model contract:

- **Nominal I/O:** `1x3x256x256 -> 1x3x512x512`
- **Runtime behavior:** arbitrary image sizes are supported in app/runtime via tiling/resizing
- **Minimum target:** `iOS16+`
- **Filename mapping:** `<model_id>.mlpackage`


| Model ID | Size | Input | Output | Profile |
| --------------------------------------- | ------- | ----- | ------ | ------- |
| <code>RealESRGAN_<wbr>x2plus</code> | 32.5 MB | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x2/RealESRGAN_x2_model_outputs/input_images/RealESRGAN_x2_model_Input1.png?raw=true" width="120" /> | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x2/RealESRGAN_x2_model_outputs/output_images/output_images1/RealESRGAN_x2plus.png?raw=true" width="120" /> | base |
| <code>RealESRGAN_<wbr>x2plus_<wbr>pal4</code> | 8.7 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x2/RealESRGAN_x2_model_outputs/output_images/output_images1/RealESRGAN_x2plus_pal4.png?raw=true" width="120" /> | pal4 |
| <code>RealESRGAN_<wbr>x2plus_<wbr>pal6</code> | 12.7 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x2/RealESRGAN_x2_model_outputs/output_images/output_images1/RealESRGAN_x2plus_pal6.png?raw=true" width="120" /> | pal6 |
| <code>RealESRGAN_<wbr>x2plus_<wbr>pal8</code> | 16.9 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x2/RealESRGAN_x2_model_outputs/output_images/output_images1/RealESRGAN_x2plus_pal8.png?raw=true" width="120" /> | pal8 |
| <code>RealESRGAN_<wbr>x2plus_<wbr>quant8</code> | 16.8 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x2/RealESRGAN_x2_model_outputs/output_images/output_images1/RealESRGAN_x2plus_quant8.png?raw=true" width="120" /> | quant8 |


### RealESRGAN x4

Model contract:

- **Nominal I/O:** `1x3x256x256 -> 1x3x1024x1024`
- **Minimum target:** base model `iOS15+` (`spec6`), compressed variants `iOS16+` (`spec7`)
- **Filename mapping:** `<model_id>.mlpackage`


| Model ID | Size | Input | Output | Profile |
| ----------------------------------- | ------- | ----- | ------ | ------- |
| <code>RealESRGAN_<wbr>x4</code> | 32.5 MB | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/input_images/RealESRGAN_x4_model_Input1.png?raw=true" width="120" /> | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/output_images/output_images1/RealESRGAN_x4.png?raw=true" width="120" /> | base |
| <code>RealESRGAN_<wbr>x4_<wbr>pal4</code> | 8.8 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/output_images/output_images1/RealESRGAN_x4_pal4.png?raw=true" width="120" /> | pal4 |
| <code>RealESRGAN_<wbr>x4_<wbr>quant8</code> | 16.8 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/output_images/output_images1/RealESRGAN_x4_quant8.png?raw=true" width="120" /> | quant8 |


---

## Image Denoising (NAFNet)

Image denoising with NAFNet (SIDD-trained, width 64). Original: [megvii-research/NAFNet](https://github.com/megvii-research/NAFNet).

Models live in `Models-List/NAFNet_SIDD_width64/`.

Model contract:

- **Nominal I/O:** `1x3x512x512 -> 1x3x512x512`
- **Core ML type:** `mlProgram`
- **Filename mapping:** `<model_id>.mlpackage`


| Model ID | Size | Input | Output | Profile |
| ------------------------------------------------ | -------- | ----- | ------ | ------------- |
| <code>NAFNet_<wbr>SIDD_<wbr>width64_<wbr>512</code> | 221.7 MB | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/NAFNet_SIDD_width64/NAFNet_SIDD_width64_model_outputs/input_images/NAFNet_SIDD_width64_model_Input1.png?raw=true" width="120" /> | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/NAFNet_SIDD_width64/NAFNet_SIDD_width64_model_outputs/output_images/output_images1/NAFNet_SIDD_width64_512.png?raw=true" width="120" /> | base |
| <code>NAFNet_<wbr>SIDD_<wbr>width64_<wbr>512_<wbr>ios18_<wbr>quant4</code> | 56.7 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/NAFNet_SIDD_width64/NAFNet_SIDD_width64_model_outputs/output_images/output_images1/NAFNet_SIDD_width64_512_ios18_quant4.png?raw=true" width="120" /> | ios18 quant4 |
| <code>NAFNet_<wbr>SIDD_<wbr>width64_<wbr>512_<wbr>pal6_<wbr>kmeans</code> | 83.9 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/NAFNet_SIDD_width64/NAFNet_SIDD_width64_model_outputs/output_images/output_images1/NAFNet_SIDD_width64_512_pal6_kmeans.png?raw=true" width="120" /> | pal6 kmeans |
| <code>NAFNet_<wbr>SIDD_<wbr>width64_<wbr>512_<wbr>pal8_<wbr>kmeans</code> | 111.6 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/NAFNet_SIDD_width64/NAFNet_SIDD_width64_model_outputs/output_images/output_images1/NAFNet_SIDD_width64_512_pal8_kmeans.png?raw=true" width="120" /> | pal8 kmeans |
| <code>NAFNet_<wbr>SIDD_<wbr>width64_<wbr>512_<wbr>pal8_<wbr>uniform</code> | 111.6 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/NAFNet_SIDD_width64/NAFNet_SIDD_width64_model_outputs/output_images/output_images1/NAFNet_SIDD_width64_512_pal8_uniform.png?raw=true" width="120" /> | pal8 uniform |
| <code>NAFNet_<wbr>SIDD_<wbr>width64_<wbr>512_<wbr>quant8</code> | 111.8 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/NAFNet_SIDD_width64/NAFNet_SIDD_width64_model_outputs/output_images/output_images1/NAFNet_SIDD_width64_512_quant8.png?raw=true" width="120" /> | quant8 |


---

## Image Colorization (DDColor)

Grayscale image colorization. ModelScope variant. Original: [piddnad/DDColor](https://github.com/piddnad/DDColor).

Models live in `Models-List/DDColor/`.

Model contract:

- **Nominal I/O:** `gray_rgb:1x3x512x512 -> ab:1x2x512x512`
- **Core ML type:** `mlProgram`
- **Filename mapping:** `<model_id>.mlpackage`


| Model ID | Size | Input | Output | Profile |
| --------------------------------------------------- | -------- | ----- | ------ | ------------- |
| <code>DDColor_<wbr>modelscope_<wbr>512</code> | 445.5 MB | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/DDColor/DDColor_Model_outputs/input_images/DDColor_model_Input1.png?raw=true" width="120" /> | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/DDColor/DDColor_Model_outputs/output_images/output_images1/DDColor_modelscope_512.png?raw=true" width="120" /> | base |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>ios18_<wbr>pal3_<wbr>kmeans</code> | 84.4 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/DDColor/DDColor_Model_outputs/output_images/output_images1/DDColor_modelscope_512_ios18_pal3_kmeans.png?raw=true" width="120" /> | ios18 pal3 kmeans |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>ios18_<wbr>quant4</code> | 112.7 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/DDColor/DDColor_Model_outputs/output_images/output_images1/DDColor_modelscope_512_ios18_quant4.png?raw=true" width="120" /> | ios18 quant4 |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>pal4_<wbr>kmeans</code> | 112.2 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/DDColor/DDColor_Model_outputs/output_images/output_images1/DDColor_modelscope_512_pal4_kmeans.png?raw=true" width="120" /> | pal4 kmeans |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>pal6_<wbr>kmeans</code> | 167.8 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/DDColor/DDColor_Model_outputs/output_images/output_images1/DDColor_modelscope_512_pal6_kmeans.png?raw=true" width="120" /> | pal6 kmeans |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>pal6_<wbr>uniform</code> | 167.8 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/DDColor/DDColor_Model_outputs/output_images/output_images1/DDColor_modelscope_512_pal6_uniform.png?raw=true" width="120" /> | pal6 uniform |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>pal8_<wbr>kmeans</code> | 223.4 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/DDColor/DDColor_Model_outputs/output_images/output_images1/DDColor_modelscope_512_pal8_kmeans.png?raw=true" width="120" /> | pal8 kmeans |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>pal8_<wbr>uniform</code> | 223.4 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/DDColor/DDColor_Model_outputs/output_images/output_images1/DDColor_modelscope_512_pal8_uniform.png?raw=true" width="120" /> | pal8 uniform |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>quant8</code> | 223.8 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/DDColor/DDColor_Model_outputs/output_images/output_images1/DDColor_modelscope_512_quant8.png?raw=true" width="120" /> | quant8 |


---

## Image2Image (Anime2Sketch)

Anime/style artwork to sketch conversion. Original: [Mukosame/Anime2Sketch](https://github.com/Mukosame/Anime2Sketch) (MIT).

Models live in `Models-List/anime2sketch/`.

Model contract:

- **Nominal I/O:** `512x512 -> 512x512`
- **Minimum target:** `iOS13+` (`spec4`)
- **Filename mapping:** `<model_id>.mlpackage`


| Model ID | Size | Input | Output | Profile |
| --------------------------------------------------------- | -------- | ----- | ------ | ------- |
| <code>anime2sketch</code> | 207.6 MB | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/anime2sketch/Anime2Sketch_x4_model_outputs/input_images/Anime2Sketch_model_Input1.png?raw=true" width="120" /> | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/anime2sketch/Anime2Sketch_x4_model_outputs/output_images/output_images1/anime2sketch.png?raw=true" width="120" /> | base |
| <code>anime2sketch_<wbr>xcode_<wbr>lut4</code> | 26.0 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/anime2sketch/Anime2Sketch_x4_model_outputs/output_images/output_images1/anime2sketch_xcode_lut4.png?raw=true" width="120" /> | lut4 |
| <code>anime2sketch_<wbr>xcode_<wbr>lut6</code> | 38.9 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/anime2sketch/Anime2Sketch_x4_model_outputs/output_images/output_images1/anime2sketch_xcode_lut6.png?raw=true" width="120" /> | lut6 |
| <code>anime2sketch_<wbr>xcode_<wbr>quant8</code> | 51.9 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/anime2sketch/Anime2Sketch_x4_model_outputs/output_images/output_images1/anime2sketch_xcode_quant8.png?raw=true" width="120" /> | quant8 |


---

## Thanks

Thanks to the authors of Real-ESRGAN, NAFNet, DDColor, and Anime2Sketch for the original models and code.

---

## Author

[Your Name]  
[Your Title / Role]  
Contact: [your@email.com](mailto:your@email.com)  
[GitHub](https://github.com/[your-username])
