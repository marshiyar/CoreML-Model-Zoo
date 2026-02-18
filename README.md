# CoreML-Model-Zoo

A collection of Core ML (`.mlpackage`) models for image super-resolution, denoising, colorization, and anime-to-sketch conversion. Add any model folder to your Xcode project and use it with the Core ML framework.

Core ML is Apple’s machine learning framework. You can use these models in iOS, iPadOS, macOS, and visionOS apps.

---

## Contents

- [How to use](#how-to-use)
- [Section links](#section-links)
- [Super Resolution (Real-ESRGAN)](#super-resolution-real-esrgan)
- [Image Denoising (NAFNet)](#image-denoising-nafnet)
- [Image Colorization (DDColor)](#image-colorization-ddcolor)
- [Image2Image (Anime2Sketch)](#image2image-anime2sketch)

---

## How to use

1. Clone or download this repository.
2. Open your Xcode project and add the `.mlpackage` you need:
  - Drag the model folder (e.g. `RealESRGAN_x4/RealESRGAN_x4.mlpackage`) into your app target, or
  - Copy the `.mlpackage` into your project and add it to the target.
3. Use the generated Swift API or `MLModel` / `VNCoreMLRequest` in your code.

Each model’s license follows the original project (see links below). Check the respective repos for terms.

---

## Section links

- **[Super Resolution (Real-ESRGAN)](#super-resolution-real-esrgan)**
  - [RealESRGAN ×2](#real-esrgan-x2)
  - [RealESRGAN ×4](#real-esrgan-x4)
- **[Image Denoising (NAFNet)](#image-denoising-nafnet)**
- **[Image Colorization (DDColor)](#image-colorization-ddcolor)**
- **[Image2Image (Anime2Sketch)](#image2image-anime2sketch)**

---

## Super Resolution (Real-ESRGAN)

Real-world image super-resolution. Original project: [xinntao/Real-ESRGAN](https://github.com/xinntao/Real-ESRGAN) (BSD-3-Clause).

Models live in `**RealESRGAN_x2/`** and `**RealESRGAN_x4/`**.

### RealESRGAN ×2


| Model                                  | Size    | Input            | Output   | Notes                                 |
| -------------------------------------- | ------- | ---------------- | -------- | ------------------------------------- |
| `RealESRGAN_x2plus.mlpackage`          | 33 MB   | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/input_images/RealESRGAN_x4_model_Input1.png?raw=true" width="120" />            | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/output_images/output_images1/RealESRGAN_x4.png?raw=true" width="120" /> | Base 2× upscale                       |
| `RealESRGAN_x2plus_flex.mlpackage`     | 33 MB   | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/input_images/RealESRGAN_x4_model_Input1.png?raw=true" width="120" />      | Image 2× | Flexible input size                   |
| `RealESRGAN_x2plus_flex1280.mlpackage` | 33 MB   | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/input_images/RealESRGAN_x4_model_Input1.png?raw=true" width="120" />  | Image 2× | Flex, max side 1280                   |
| `RealESRGAN_x2plus_pruned.mlpackage`   | 33 MB   | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/input_images/RealESRGAN_x4_model_Input1.png?raw=true" width="120" />             | Image 2× | Pruned (smaller)                      |
| `RealESRGAN_x2plus_quant8.mlpackage`   | 17 MB   | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/input_images/RealESRGAN_x4_model_Input1.png?raw=true" width="120" />             | Image 2× | INT8 quantized                        |
| `RealESRGAN_x2plus_pal4.mlpackage`     | 9 MB    | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/input_images/RealESRGAN_x4_model_Input1.png?raw=true" width="120" />             | Image 2× | Palette (4-bit)                       |
| `RealESRGAN_x2plus_pal6.mlpackage`     | 13 MB   | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/input_images/RealESRGAN_x4_model_Input1.png?raw=true" width="120" />             | Image 2× | Palette (6-bit)                       |
| `RealESRGAN_x2plus_pal8.mlpackage`     | 17 MB   | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/input_images/RealESRGAN_x4_model_Input1.png?raw=true" width="120" />             | Image 2× | Palette (8-bit)                       |
| `RealESRGAN_x2plus_flex1280_`*         | 9–33 MB | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/input_images/RealESRGAN_x4_model_Input1.png?raw=true" width="120" />  | Image 2× | Flex1280 + pruned / quant8 / pal4/6/8 |
| `RealESRGAN_x2_wrapped.mlpackage`      | 33 MB   | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/input_images/RealESRGAN_x4_model_Input1.png?raw=true" width="120" />             | Image 2× | Wrapped variant                       |


### RealESRGAN ×4


| Model                                           | Size   | Input | Output   | Notes                         |
| ----------------------------------------------- | ------ | ----- | -------- | ----------------------------- |
| `RealESRGAN_x4.mlpackage`                       | 33 MB  | Image | Image 4× | Base 4× upscale               |
| `RealESRGAN_x4_slim.mlpackage`                  | 17 MB  | Image | Image 4× | Slimmer architecture          |
| `RealESRGAN_x4_slimmer.mlpackage`               | 9 MB   | Image | Image 4× | Even slimmer                  |
| `RealESRGAN_x4_pruned.mlpackage`                | 33 MB  | Image | Image 4× | Pruned                        |
| `RealESRGAN_x4_quant8.mlpackage`                | 17 MB  | Image | Image 4× | INT8 quantized                |
| `RealESRGAN_x4_pal4.mlpackage`                  | 9 MB   | Image | Image 4× | Palette 4-bit                 |
| `RealESRGAN_x4_pal6.mlpackage`                  | 13 MB  | Image | Image 4× | Palette 6-bit                 |
| `RealESRGAN_x4_pal8.mlpackage`                  | 17 MB  | Image | Image 4× | Palette 8-bit                 |
| `RealESRGAN_x4_arch_b8_xcode.mlpackage`         | 12 MB  | Image | Image 4× | Block 8, Xcode-optimized      |
| `RealESRGAN_x4_arch_b10_xcode.mlpackage`        | 14 MB  | Image | Image 4× | Block 10, Xcode-optimized     |
| `RealESRGAN_x4_arch_b12.mlpackage`              | 17 MB  | Image | Image 4× | Block 12 (larger)             |
| `RealESRGAN_x4_arch_b12_xcode.mlpackage`        | 17 MB  | Image | Image 4× | Block 12, Xcode-optimized     |
| `RealESRGAN_x4_arch_b12_quant8.mlpackage`       | 9 MB   | Image | Image 4× | Block 12, INT8                |
| `RealESRGAN_x4_arch_*_pal4.mlpackage`           | 1–5 MB | Image | Image 4× | Same archs with 4-bit palette |
| `RealESRGAN_x4_iphone_ultralite.mlpackage`      | 3.5 MB | Image | Image 4× | Smallest / fastest            |
| `RealESRGAN_x4_iphone_ultralite_pal4.mlpackage` | 1.1 MB | Image | Image 4× | Ultralite + pal4              |


---

## Image Denoising (NAFNet)

Image denoising with NAFNet (SIDD-trained, width 64). Original: [megvii-research/NAFNet](https://github.com/megvii-research/NAFNet).

Models live in `NAFNet_SIDD_width64/`.


| Variant                                          | Size      | Input       | Output      | Notes                      |
| ------------------------------------------------ | --------- | ----------- | ----------- | -------------------------- |
| `NAFNet_SIDD_width64_512.mlpackage`              | 222 MB    | RGB 512×512 | RGB 512×512 | Base                       |
| `NAFNet_SIDD_width64_512_quant8.mlpackage`       | 112 MB    | RGB 512×512 | RGB 512×512 | INT8                       |
| `NAFNet_SIDD_width64_512_ios18.mlpackage`        | 222 MB    | RGB 512×512 | RGB 512×512 | iOS 18 runtime             |
| `NAFNet_SIDD_width64_512_ios18_quant4.mlpackage` | 57 MB     | RGB 512×512 | RGB 512×512 | iOS 18, 4-bit quant        |
| `NAFNet_SIDD_width64_512_pal1_kmeans.mlpackage`  | 15 MB     | RGB 512×512 | RGB 512×512 | 1-bit palette (k-means)    |
| `NAFNet_SIDD_width64_512_pal2_kmeans.mlpackage`  | 29 MB     | RGB 512×512 | RGB 512×512 | 2-bit palette              |
| `NAFNet_SIDD_width64_512_pal4_kmeans.mlpackage`  | 56 MB     | RGB 512×512 | RGB 512×512 | 4-bit palette              |
| `NAFNet_SIDD_width64_512_pal6_kmeans.mlpackage`  | 84 MB     | RGB 512×512 | RGB 512×512 | 6-bit palette              |
| `NAFNet_SIDD_width64_512_pal8_kmeans.mlpackage`  | 112 MB    | RGB 512×512 | RGB 512×512 | 8-bit palette              |
| `NAFNet_SIDD_width64_512_pal*_uniform.mlpackage` | 15–112 MB | RGB 512×512 | RGB 512×512 | Same bits, uniform palette |
| `NAFNet_SIDD_width64_512_ios18_pal3_*.mlpackage` | 43 MB     | RGB 512×512 | RGB 512×512 | iOS 18 + 3-bit palette     |


---

## Image Colorization (DDColor)

Grayscale image colorization. ModelScope variant. Original: [piddnad/DDColor](https://github.com/piddnad/DDColor).

Models live in `DDColor/`.


| Variant                                               | Size      | Input                   | Output                 | Notes                      |
| ----------------------------------------------------- | --------- | ----------------------- | ---------------------- | -------------------------- |
| `DDColor_modelscope_512.mlpackage`                    | 446 MB    | Grayscale 512×512 (3ch) | Lab `ab` 512×512 (2ch) | Base                       |
| `DDColor_modelscope_512_pruned.mlpackage`             | 446 MB    | Grayscale 512×512 (3ch) | Lab `ab` 512×512 (2ch) | Pruned                     |
| `DDColor_modelscope_512_quant8.mlpackage`             | 224 MB    | Grayscale 512×512 (3ch) | Lab `ab` 512×512 (2ch) | INT8                       |
| `DDColor_modelscope_512_ios18.mlpackage`              | 446 MB    | Grayscale 512×512 (3ch) | Lab `ab` 512×512 (2ch) | iOS 18                     |
| `DDColor_modelscope_512_ios18_quant4.mlpackage`       | 113 MB    | Grayscale 512×512 (3ch) | Lab `ab` 512×512 (2ch) | iOS 18, 4-bit              |
| `DDColor_modelscope_512_ios18_pal3_kmeans.mlpackage`  | 84 MB     | Grayscale 512×512 (3ch) | Lab `ab` 512×512 (2ch) | iOS 18, 3-bit palette      |
| `DDColor_modelscope_512_ios18_pal3_uniform.mlpackage` | 84 MB     | Grayscale 512×512 (3ch) | Lab `ab` 512×512 (2ch) | iOS 18, 3-bit uniform      |
| `DDColor_modelscope_512_pal1_kmeans.mlpackage`        | 29 MB     | Grayscale 512×512 (3ch) | Lab `ab` 512×512 (2ch) | 1-bit palette              |
| `DDColor_modelscope_512_pal2_kmeans.mlpackage`        | 57 MB     | Grayscale 512×512 (3ch) | Lab `ab` 512×512 (2ch) | 2-bit palette              |
| `DDColor_modelscope_512_pal4_kmeans.mlpackage`        | 112 MB    | Grayscale 512×512 (3ch) | Lab `ab` 512×512 (2ch) | 4-bit palette              |
| `DDColor_modelscope_512_pal6_kmeans.mlpackage`        | 168 MB    | Grayscale 512×512 (3ch) | Lab `ab` 512×512 (2ch) | 6-bit palette              |
| `DDColor_modelscope_512_pal8_kmeans.mlpackage`        | 223 MB    | Grayscale 512×512 (3ch) | Lab `ab` 512×512 (2ch) | 8-bit palette              |
| `DDColor_modelscope_512_pal*_uniform.mlpackage`       | 29–223 MB | Grayscale 512×512 (3ch) | Lab `ab` 512×512 (2ch) | Same bits, uniform palette |
| `DDColor_modelscope_512_pal_unique.mlpackage`         | 446 MB    | Grayscale 512×512 (3ch) | Lab `ab` 512×512 (2ch) | Unique palette variant     |


---

## Image2Image (Anime2Sketch)

Anime/style artwork to sketch conversion. Original: [Mukosame/Anime2Sketch](https://github.com/Mukosame/Anime2Sketch) (MIT).

Models live in `anime2sketch/`.


| Model                                           | Size   | Input         | Output                 | Notes            |
| ----------------------------------------------- | ------ | ------------- | ---------------------- | ---------------- |
| `anime2sketch.mlpackage`                        | 208 MB | Image 512×512 | Image 512×512 (sketch) | Base             |
| `anime2sketch_xcode.mlpackage`                  | 208 MB | Image 512×512 | Image 512×512 (sketch) | Xcode-optimized  |
| `anime2sketch_xcode_fp16.mlpackage`             | 104 MB | Image 512×512 | Image 512×512 (sketch) | FP16             |
| `anime2sketch_xcode_quant8.mlpackage`           | 52 MB  | Image 512×512 | Image 512×512 (sketch) | INT8             |
| `anime2sketch_xcode_archsame_quant4.mlpackage`  | 26 MB  | Image 512×512 | Image 512×512 (sketch) | Same arch, 4-bit |
| `anime2sketch_xcode_archsame_quant8.mlpackage`  | 52 MB  | Image 512×512 | Image 512×512 (sketch) | Same arch, 8-bit |
| `anime2sketch_xcode_archsame_pal4.mlpackage`    | 26 MB  | Image 512×512 | Image 512×512 (sketch) | Same arch, pal4  |
| `anime2sketch_xcode_lut4.mlpackage`             | 26 MB  | Image 512×512 | Image 512×512 (sketch) | LUT 4-bit        |
| `anime2sketch_xcode_lut6.mlpackage`             | 39 MB  | Image 512×512 | Image 512×512 (sketch) | LUT 6-bit        |
| `anime2sketch_xcode_linear4.mlpackage`          | 26 MB  | Image 512×512 | Image 512×512 (sketch) | Linear 4-bit     |
| `anime2sketch_xcode_hybrid_q4lut4_50.mlpackage` | 26 MB  | Image 512×512 | Image 512×512 (sketch) | Hybrid quant     |


---

## Thanks

Thanks to the authors of Real-ESRGAN, NAFNet, DDColor, and Anime2Sketch for the original models and code.

---

## Author

[Your Name]  
[Your Title / Role]  
Contact: [your@email.com](mailto:your@email.com)  
[GitHub](https://github.com/[your-username])
