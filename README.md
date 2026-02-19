# CoreML-Model-Zoo

A curated collection of CoreML (`.mlpackage`) models
All models can be added directly to Xcode projects targeting iOS, iPadOS, macOS, and visionOS.

## Quick start

1. You can find each model linked to its realease direct link or navigate to "Releases" and select your wanted Model

Each model’s license follows its original upstream project (linked in the Footnotes).

<a id="contents"></a>
<details>
<summary><strong>Contents</strong></summary>

- [Super Resolution (Real-ESRGAN)](#super-resolution-real-esrgan)
- [Image Denoising (NAFNet)](#image-denoising-nafnet)
- [Image Colorization (DDColor)](#image-colorization-ddcolor)
- [Image2Image (Anime2Sketch)](#image2image-anime2sketch)

</details>

# Super Resolution

## Real-ESRGAN

Models live in `Models-List/RealESRGAN_x2/` and `Models-List/RealESRGAN_x4/`.

### RealESRGAN x2

<details>
<summary><strong>Model contract</strong></summary>

- **Nominal I/O:** <code>1x3x256x256 -> 1x3x512x512</code>
- **Runtime behavior:** arbitrary image sizes are supported in app/runtime via tiling/resizing
- **Minimum target:** <code>iOS16+</code>
- **Filename mapping:** <code>&lt;model_id&gt;.mlpackage</code>

</details>

| Model ID | Size | Input | Output | Profile |
| --------------------------------------- | ------- | ----- | ------ | ------- |
| <code>RealESRGAN_<wbr>x2plus</code> | 32.5 MB | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x2/RealESRGAN_x2_model_outputs/input_images/RealESRGAN_x2_model_Input1.png?raw=true" width="120" /> | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x2/RealESRGAN_x2_model_outputs/output_images/output_images1/RealESRGAN_x2plus.png?raw=true" width="120" /> | base |
| <code>RealESRGAN_<wbr>x2plus_<wbr>pal4</code> | 8.7 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x2/RealESRGAN_x2_model_outputs/output_images/output_images1/RealESRGAN_x2plus_pal4.png?raw=true" width="120" /> | pal4 |
| <code>RealESRGAN_<wbr>x2plus_<wbr>pal6</code> | 12.7 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x2/RealESRGAN_x2_model_outputs/output_images/output_images1/RealESRGAN_x2plus_pal6.png?raw=true" width="120" /> | pal6 |
| <code>RealESRGAN_<wbr>x2plus_<wbr>pal-8</code> | 16.9 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x2/RealESRGAN_x2_model_outputs/output_images/output_images1/RealESRGAN_x2plus_pal-8.png?raw=true" width="120" /> | pal-8 |
| <code>RealESRGAN_<wbr>x2plus_<wbr>Q-4</code> | 16.8 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x2/RealESRGAN_x2_model_outputs/output_images/output_images1/RealESRGAN_x2plus_Q-4.png?raw=true" width="120" /> | Q-4 |

### RealESRGAN x4

<details>
<summary><strong>Model contract</strong></summary>

- **Nominal I/O:** <code>1x3x256x256 -> 1x3x1024x1024</code>
- **Minimum target:** base model <code>iOS15+</code> (<code>spec6</code>), compressed variants <code>iOS16+</code> (<code>spec7</code>)
- **Filename mapping:** <code>&lt;model_id&gt;.mlpackage</code>

</details>

| Model ID | Size | Input | Output | Profile |
| ----------------------------------- | ------- | ----- | ------ | ------- |
| <code>RealESRGAN_<wbr>x4</code> | 32.5 MB | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/input_images/RealESRGAN_x4_model_Input1.png?raw=true" width="120" /> | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/output_images/output_images1/RealESRGAN_x4.png?raw=true" width="120" /> | base |
| <code>RealESRGAN_<wbr>x4_<wbr>pal4</code> | 8.8 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/output_images/output_images1/RealESRGAN_x4_pal4.png?raw=true" width="120" /> | pal4 |
| <code>RealESRGAN_<wbr>x4_<wbr>Q-4</code> | 16.8 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/output_images/output_images1/RealESRGAN_x4_Q-4.png?raw=true" width="120" /> | Q-4 |

---

# Image Denoising

## NAFNet

Image denoising with NAFNet (SIDD-trained, width 64). Original: [megvii-research/NAFNet](https://github.com/megvii-research/NAFNet).

Models live in `Models-List/NAFNet_SIDD_width64/`.

<details>
<summary><strong>Model contract</strong></summary>

- **Nominal I/O:** `1x3x512x512 -> 1x3x512x512`
- **CoreML type:** `mlProgram`
- **Filename mapping:** `<model_id>.mlpackage`

</details>


| Model ID | Size | Input | Output | Profile |
| ------------------------------------------------ | -------- | ----- | ------ | ------------- |
| <code>NAFNet_<wbr>SIDD_<wbr>width64_<wbr>512</code> | 221.7 MB | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/NAFNet_SIDD_width64/NAFNet_SIDD_width64_model_outputs/input_images/NAFNet_SIDD_width64_model_Input1.png?raw=true" width="120" /> | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/NAFNet_SIDD_width64/NAFNet_SIDD_width64_model_outputs/output_images/output_images1/NAFNet_SIDD_width64_512.png?raw=true" width="120" /> | base |
| <code>NAFNet_<wbr>SIDD_<wbr>width64_<wbr>512_<wbr>ios18_<wbr>Q-4</code> | 56.7 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/NAFNet_SIDD_width64/NAFNet_SIDD_width64_model_outputs/output_images/output_images1/NAFNet_SIDD_width64_512_ios18_Q-4.png?raw=true" width="120" /> | ios18 Q-4 |
| <code>NAFNet_<wbr>SIDD_<wbr>width64_<wbr>512_<wbr>pal6_<wbr>kmeans</code> | 83.9 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/NAFNet_SIDD_width64/NAFNet_SIDD_width64_model_outputs/output_images/output_images1/NAFNet_SIDD_width64_512_pal6_kmeans.png?raw=true" width="120" /> | pal6 kmeans |
| <code>NAFNet_<wbr>SIDD_<wbr>width64_<wbr>512_<wbr>pal-8_<wbr>kmeans</code> | 111.6 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/NAFNet_SIDD_width64/NAFNet_SIDD_width64_model_outputs/output_images/output_images1/NAFNet_SIDD_width64_512_pal-8_kmeans.png?raw=true" width="120" /> | pal-8 kmeans |
| <code>NAFNet_<wbr>SIDD_<wbr>width64_<wbr>512_<wbr>pal-8_<wbr>uniform</code> | 111.6 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/NAFNet_SIDD_width64/NAFNet_SIDD_width64_model_outputs/output_images/output_images1/NAFNet_SIDD_width64_512_pal-8_uniform.png?raw=true" width="120" /> | pal-8 uniform |
| <code>NAFNet_<wbr>SIDD_<wbr>width64_<wbr>512_<wbr>Q-4</code> | 111.8 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/NAFNet_SIDD_width64/NAFNet_SIDD_width64_model_outputs/output_images/output_images1/NAFNet_SIDD_width64_512_Q-4.png?raw=true" width="120" /> | Q-4 |

---

# Image Colorization

## DDColor

Models live in `Models-List/DDColor/`.

<details>
<summary><strong>Model contract</strong></summary>

- **Nominal I/O:** <code>gray_rgb:1x3x512x512 -> ab:1x2x512x512</code>
- **Filename mapping:** <code>&lt;model_id&gt;.mlpackage</code>

</details>


| Model ID | Size | Input | Output | Profile |
| --------------------------------------------------- | -------- | ----- | ------ | ------------- |
| <code>DDColor_<wbr>modelscope_<wbr>512</code> | 445.5 MB | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/DDColor/DDColor_Model_outputs/input_images/DDColor_model_Input1.png?raw=true" width="120" /> | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/DDColor/DDColor_Model_outputs/output_images/output_images1/DDColor_modelscope_512.png?raw=true" width="120" /> | base |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>ios18_<wbr>pal3_<wbr>kmeans</code> | 84.4 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/DDColor/DDColor_Model_outputs/output_images/output_images1/DDColor_modelscope_512_ios18_pal3_kmeans.png?raw=true" width="120" /> | ios18 pal3 kmeans |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>ios18_<wbr>Q-4</code> | 112.7 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/DDColor/DDColor_Model_outputs/output_images/output_images1/DDColor_modelscope_512_ios18_Q-4.png?raw=true" width="120" /> | ios18 Q-4 |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>pal4_<wbr>kmeans</code> | 112.2 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/DDColor/DDColor_Model_outputs/output_images/output_images1/DDColor_modelscope_512_pal4_kmeans.png?raw=true" width="120" /> | pal4 kmeans |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>pal6_<wbr>kmeans</code> | 167.8 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/DDColor/DDColor_Model_outputs/output_images/output_images1/DDColor_modelscope_512_pal6_kmeans.png?raw=true" width="120" /> | pal6 kmeans |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>pal6_<wbr>uniform</code> | 167.8 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/DDColor/DDColor_Model_outputs/output_images/output_images1/DDColor_modelscope_512_pal6_uniform.png?raw=true" width="120" /> | pal6 uniform |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>pal-8_<wbr>kmeans</code> | 223.4 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/DDColor/DDColor_Model_outputs/output_images/output_images1/DDColor_modelscope_512_pal-8_kmeans.png?raw=true" width="120" /> | pal-8 kmeans |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>pal-8_<wbr>uniform</code> | 223.4 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/DDColor/DDColor_Model_outputs/output_images/output_images1/DDColor_modelscope_512_pal-8_uniform.png?raw=true" width="120" /> | pal-8 uniform |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>Q-4</code> | 223.8 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/DDColor/DDColor_Model_outputs/output_images/output_images1/DDColor_modelscope_512_Q-4.png?raw=true" width="120" /> | Q-4 |


---

## Image2Image (Anime2Sketch)

Models live in `Models-List/anime2sketch/`.
<details>
<summary><strong>Model contract</strong></summary>

- **Nominal I/O:** `512x512 -> 512x512`
- **Minimum target:** `iOS13+` (`spec4`)
- **Filename mapping:** `<model_id>.mlpackage`

</details>


| Model ID | Size | Input | Output | Profile |
| --------------------------------------------------------- | -------- | ----- | ------ | ------- |
| <code>anime2sketch</code> | 207.6 MB | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/anime2sketch/Anime2Sketch_x4_model_outputs/input_images/Anime2Sketch_model_Input1.png?raw=true" width="120" /> | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/anime2sketch/Anime2Sketch_x4_model_outputs/output_images/output_images1/anime2sketch.png?raw=true" width="120" /> | base |
| <code>anime2sketch_<wbr>xcode_<wbr>LUT-4</code> | 26.0 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/anime2sketch/Anime2Sketch_x4_model_outputs/output_images/output_images1/anime2sketch_xcode_LUT-4.png?raw=true" width="120" /> | LUT-4 |
| <code>anime2sketch_<wbr>xcode_<wbr>LUT-6</code> | 38.9 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/anime2sketch/Anime2Sketch_x4_model_outputs/output_images/output_images1/anime2sketch_xcode_LUT-6.png?raw=true" width="120" /> | LUT-6 |
| <code>anime2sketch_<wbr>xcode_<wbr>Q-4</code> | 51.9 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/anime2sketch/Anime2Sketch_x4_model_outputs/output_images/output_images1/anime2sketch_xcode_Q-4.png?raw=true" width="120" /> | Q-4 |


---

## Thanks

Thanks to the authors of Real-ESRGAN, NAFNet, DDColor, and Anime2Sketch for the original models and code.

---

## Author

Arshiya Rahgozar  
[GitHub](https://github.com/marshiyar)
[LinkedIn](https://www.linkedin.com/in/marshiyar/)

### Footnotes

Real-world image super-resolution. Original project: [xinntao/Real-ESRGAN](https://github.com/xinntao/Real-ESRGAN) (BSD-3-Clause).
Anime/style artwork to sketch conversion. Original: [Mukosame/Anime2Sketch](https://github.com/Mukosame/Anime2Sketch) (MIT).
Grayscale image colorization. ModelScope variant. Original: [piddnad/DDColor](https://github.com/piddnad/DDColor).