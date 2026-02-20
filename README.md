# CoreML-Model-Zoo

<p align="center">
  <a href="https://huggingface.co/marshiyar">
    <img alt="HF" src="https://img.shields.io/badge/HF-My_Hugging_Face-yellow?logo=huggingface&logoColor=yellow">
  </a>
</p>

A curated collection of CoreML (`.mlpackage`) models
All models can be added directly to Xcode projects targeting iOS, iPadOS, macOS, and visionOS.

# Quick start

You can find each model linked to its release direct link, or navigate to [Releases](https://github.com/marshiyar/CoreML-Model-Zoo/releases) and select your desired model.

Each model’s license follows its original upstream project (linked in the [Footnotes](#footnotes)).

<a id="contents"></a>

<details>
  
<summary><strong>Contents</strong></summary>

- [Super Resolution](#super-resolution)
  - [RealESRGAN x2](#realesrgan-x2)
  - [RealESRGAN x4](#realesrgan-x4)
- [Image Denoising](#image-denoising)
  - [NAFNet](#nafnet)
- [Image Colorization](#image-colorization)
  - [DDColor](#ddcolor)
- [Image2Image](#image2image)
  - [Anime2Sketch](#anime2sketch)
- [Footnotes](#footnotes)

</details>

<a id="super-resolution"></a>
# Super Resolution

<a id="realesrgan-x2"></a>
## RealESRGAN x2 [^1]

<p align="leading">
  <a href="https://huggingface.co/marshiyar/RealESRGAN_x2_CoreML">
    <img alt="HF" src="https://img.shields.io/badge/HF-RealESRGAN_x2_CoreML-yellow?logo=huggingface&logoColor=yellow">
  </a>
</p>

<details>
<summary><strong>Model contract</strong></summary>

- **Predictions:** <code>1x3x256x256 -> 1x3x512x512</code>

</details>

| Model ID | Size | Input | Output | Profile |
| --------------------------------------- | ------- | ----- | ------ | ------- |
| [RealESRGAN_x2plus&nbsp;<sup>⬇️</sup>](https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/RealESRGAN_x2_CoreML/RealESRGAN_x2plus.mlpackage.zip) | 32.5 MB | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/readme-assets/RealESRGAN_x2_model_Input1.png" width="120" /> | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/readme-assets/RealESRGAN_x2plus.png" width="120" /> | base |
| [RealESRGAN_x2plus_pal-4&nbsp;<sup>⬇️</sup>](https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/RealESRGAN_x2_CoreML/RealESRGAN_x2plus_pal-4.mlpackage.zip) | 8.7 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/readme-assets/RealESRGAN_x2plus_pal-4.png" width="120" /> | pal-4 |
| [RealESRGAN_x2plus_pal-6&nbsp;<sup>⬇️</sup>](https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/RealESRGAN_x2_CoreML/RealESRGAN_x2plus_pal-6.mlpackage.zip) | 12.7 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/readme-assets/RealESRGAN_x2plus_pal-6.png" width="120" /> | pal-6 |
| [RealESRGAN_x2plus_pal-8&nbsp;<sup>⬇️</sup>](https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/RealESRGAN_x2_CoreML/RealESRGAN_x2plus_pal-8.mlpackage.zip) | 16.9 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/readme-assets/RealESRGAN_x2plus_pal-8.png" width="120" /> | pal-8 |
| [RealESRGAN_x2plus_Q-8&nbsp;<sup>⬇️</sup>](https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/RealESRGAN_x2_CoreML/RealESRGAN_x2plus_Q-8.mlpackage.zip) | 16.8 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/readme-assets/RealESRGAN_x2plus_Q-8.png" width="120" /> | Q-8 |

<a id="realesrgan-x4"></a>
### RealESRGAN x4

<p align="leading">
  <a href="https://huggingface.co/marshiyar/RealESRGAN_x4_CoreML">
    <img alt="HF" src="https://img.shields.io/badge/HF-RealESRGAN_x4_CoreML-yellow?logo=huggingface&logoColor=yellow">
  </a>
</p>

<details>
<summary><strong>Model contract</strong></summary>

- **Predictions:** <code>1x3x256x256 -> 1x3x1024x1024</code>

</details>

| Model ID | Size | Input | Output | Profile |
| ----------------------------------- | ------- | ----- | ------ | ------- |
| [RealESRGAN_x4&nbsp;<sup>⬇️</sup>](https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/RealESRGAN_x4_CoreLM/RealESRGAN_x4.mlpackage.zip) | 32.5 MB | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/readme-assets/RealESRGAN_x4_model_Input1.png" width="120" /> | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/readme-assets/RealESRGAN_x4.png" width="120" /> | base |
| [RealESRGAN_x4_pal-4&nbsp;<sup>⬇️</sup>](https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/RealESRGAN_x4_CoreLM/RealESRGAN_x4_pal-4.mlpackage.zip) | 8.8 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/readme-assets/RealESRGAN_x4_pal-4.png" width="120" /> | pal-4 |
| [RealESRGAN_x4_Q-8&nbsp;<sup>⬇️</sup>](https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/RealESRGAN_x4_CoreLM/RealESRGAN_x4_Q-8.mlpackage.zip) | 16.8 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/readme-assets/RealESRGAN_x4_Q-8.png" width="120" /> | Q-8 |


### Performance Benchmarks (RealESRGAN x4)

Tested on MacBook Pro (Apple Silicon M4 Max, 36 GB) running macOS 15.7.2 using Xcode Performance tab with Compute Units: All.

  <details>
  <summary><strong>Part 1 — Model + device info</strong></summary>
    
| Model File Name     | Model Type   | Model Size   | Device Type   | Software Version   |  Compute Units                |
|:--------------------|:-------------|:-------------|:--------------|:-------------------|:------------------------------|
| RealESRGAN_x4       | ML Program   | 34.1 MB      | MacBook Pro   | macOS 15.7.2       | All (CPU, GPU, Neural Engine) |
| RealESRGAN_x4_Q-8   | ML Program   | 17.6 MB      | MacBook Pro   | macOS 15.7.2       | All (CPU, GPU, Neural Engine) |
| RealESRGAN_x4_pal-4 | ML Program   | 9.2 MB       | MacBook Pro   | macOS 15.7.2       | All (CPU, GPU, Neural Engine) |

  </details>

  <details>
  <summary><strong>Part 2 — Operations</strong></summary>

| Model File Name     |   Neural Engine Operations |   CPU Operations |   GPU Operations | Total Operations   |
|:--------------------|---------------------------:|-----------------:|-----------------:|:-------------------|
| RealESRGAN_x4       |                        955 |                0 |               71 | 1,026              |
| RealESRGAN_x4_Q-8   |                        955 |                0 |               71 | 1,026              |
| RealESRGAN_x4_pal-4 |                        955 |                0 |               71 | 1,026              |

</details>

<details>
  <summary><strong>Part 3 — Performance (Prediction / Load / Compile)</strong></summary>
  
| Model File Name     | Metric     | Average   | Median   | Minimum   | Maximum   | Uncached   |
|:--------------------|:-----------|:----------|:---------|:----------|:----------|:-----------|
| RealESRGAN_x4       | Prediction | 198.62    | 196.61   | 191.82    | 251.10    | 251.10     |
| RealESRGAN_x4       | Load       | 82.63     | 83.41    | 78.56     | 84.40     | 1,946.85   |
| RealESRGAN_x4       | Compile    | 199.57    | 197.59   | 195.36    | 205.77    | 195.36     |
| RealESRGAN_x4_Q-8   | Prediction | 201.30    | 199.74   | 192.94    | 236.59    | 236.59     |
| RealESRGAN_x4_Q-8   | Load       | 94.53     | 94.92    | 90.93     | 96.17     | 2,399.90   |
| RealESRGAN_x4_Q-8   | Compile    | 222.40    | 222.53   | 220.22    | 224.45    | 220.22     |
| RealESRGAN_x4_pal-4 | Prediction | 200.81    | 199.31   | 193.33    | 259.98    | 259.98     |
| RealESRGAN_x4_pal-4 | Load       | 90.99     | 91.74    | 85.77     | 93.65     | 2,103.96   |
| RealESRGAN_x4_pal-4 | Compile    | 211.95    | 211.87   | 211.81    | 212.18    | 212.18     |

</details>


---

<a id="image-denoising"></a>
# Image Denoising

<a id="nafnet"></a>
## NAFNet [^2]

<details>
<summary><strong>Model contract</strong></summary>

- **Predictions:** `1x3x512x512 -> 1x3x512x512`

</details>


| Model ID | Size | Input | Output | Profile |
| ------------------------------------------------ | -------- | ----- | ------ | ------------- |
| [NAFNet_SIDD_width64_512&nbsp;<sup>⬇️</sup>](https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/NAFNet_SIDD_width64_CoreML/NAFNet_SIDD_width64_512.mlpackage.zip) | 221.7 MB | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/readme-assets/NAFNet_SIDD_width64_model_Input1.png" width="120" /> | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/readme-assets/NAFNet_SIDD_width64_512.png" width="120" /> | base |
| [NAFNet_SIDD_width64_512_ios18_quant4&nbsp;<sup>⬇️</sup>](https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/NAFNet_SIDD_width64_CoreML/NAFNet_SIDD_width64_512_ios18_quant4.mlpackage.zip) | 56.7 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/readme-assets/NAFNet_SIDD_width64_512_ios18_quant4.png" width="120" /> | ios18 quant4 |
| [NAFNet_SIDD_width64_512_pal6_kmeans&nbsp;<sup>⬇️</sup>](https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/NAFNet_SIDD_width64_CoreML/NAFNet_SIDD_width64_512_pal6_kmeans.mlpackage.zip) | 83.9 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/readme-assets/NAFNet_SIDD_width64_512_pal6_kmeans.png" width="120" /> | pal6 kmeans |
| [NAFNet_SIDD_width64_512_pal8_kmeans&nbsp;<sup>⬇️</sup>](https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/NAFNet_SIDD_width64_CoreML/NAFNet_SIDD_width64_512_pal8_kmeans.mlpackage.zip) | 111.6 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/readme-assets/NAFNet_SIDD_width64_512_pal8_kmeans.png" width="120" /> | pal8 kmeans |
| [NAFNet_SIDD_width64_512_pal8_uniform&nbsp;<sup>⬇️</sup>](https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/NAFNet_SIDD_width64_CoreML/NAFNet_SIDD_width64_512_pal8_uniform.mlpackage.zip) | 111.6 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/readme-assets/NAFNet_SIDD_width64_512_pal8_uniform.png" width="120" /> | pal8 uniform |
| [NAFNet_SIDD_width64_512_quant8&nbsp;<sup>⬇️</sup>](https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/NAFNet_SIDD_width64_CoreML/NAFNet_SIDD_width64_512_quant8.mlpackage.zip) | 111.8 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/readme-assets/NAFNet_SIDD_width64_512_quant8.png" width="120" /> | quant8 |

---

<a id="image-colorization"></a>
# Image Colorization

<a id="ddcolor"></a>
## DDColor [^4]

<details>
<summary><strong>Model contract</strong></summary>

- **Predictions:** <code>gray_rgb:1x3x512x512 -> ab:1x2x512x512</code>
- **Filename mapping:** <code>&lt;model_id&gt;.mlpackage</code>

</details>


| Model ID | Size | Input | Output | Profile |
| --------------------------------------------------- | -------- | ----- | ------ | ------------- |
| [DDColor_modelscope_512&nbsp;<sup>⬇️</sup>](https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/DDColor_CoreML/DDColor_modelscope_512.mlpackage.zip) | 445.5 MB | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/readme-assets/DDColor_model_Input1.png" width="120" /> | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/readme-assets/DDColor_modelscope_512.png" width="120" /> | base |
| [DDColor_modelscope_512_ios18_pal-3_kmeans&nbsp;<sup>⬇️</sup>](https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/DDColor_CoreML/DDColor_modelscope_512_ios18_pal-3_kmeans.mlpackage.zip) | 84.4 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/readme-assets/DDColor_modelscope_512_ios18_pal-3_kmeans.png" width="120" /> | ios18 pal-3 kmeans |
| [DDColor_modelscope_512_ios18_quant4&nbsp;<sup>⬇️</sup>](https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/DDColor_CoreML/DDColor_modelscope_512_ios18_quant4.mlpackage.zip) | 112.7 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/readme-assets/DDColor_modelscope_512_ios18_quant4.png" width="120" /> | ios18 quant4 |
| [DDColor_modelscope_512_pal-4_kmeans&nbsp;<sup>⬇️</sup>](https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/DDColor_CoreML/DDColor_modelscope_512_pal-4_kmeans.mlpackage.zip) | 112.2 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/readme-assets/DDColor_modelscope_512_pal-4_kmeans.png" width="120" /> | pal-4 kmeans |
| [DDColor_modelscope_512_pal-6_kmeans&nbsp;<sup>⬇️</sup>](https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/DDColor_CoreML/DDColor_modelscope_512_pal-6_kmeans.mlpackage.zip) | 167.8 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/readme-assets/DDColor_modelscope_512_pal-6_kmeans.png" width="120" /> | pal-6 kmeans |
| [DDColor_modelscope_512_pal-6_uniform&nbsp;<sup>⬇️</sup>](https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/DDColor_CoreML/DDColor_modelscope_512_pal-6_uniform.mlpackage.zip) | 167.8 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/readme-assets/DDColor_modelscope_512_pal-6_uniform.png" width="120" /> | pal-6 uniform |
| [DDColor_modelscope_512_pal-8_kmeans&nbsp;<sup>⬇️</sup>](https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/DDColor_CoreML/DDColor_modelscope_512_pal-8_kmeans.mlpackage.zip) | 223.4 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/readme-assets/DDColor_modelscope_512_pal-8_kmeans.png" width="120" /> | pal-8 kmeans |
| [DDColor_modelscope_512_pal-8_uniform&nbsp;<sup>⬇️</sup>](https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/DDColor_CoreML/DDColor_modelscope_512_pal-8_uniform.mlpackage.zip) | 223.4 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/readme-assets/DDColor_modelscope_512_pal-8_uniform.png" width="120" /> | pal-8 uniform |
| [DDColor_modelscope_512_Q-8&nbsp;<sup>⬇️</sup>](https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/DDColor_CoreML/DDColor_modelscope_512_Q-8.mlpackage.zip) | 223.8 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/readme-assets/DDColor_modelscope_512_Q-8.png" width="120" /> | Q-8 |

---

<a id="image2image"></a>
<a id="anime2sketch"></a>
## Image2Image (Anime2Sketch) [^3]


<details>
<summary><strong>Model contract</strong></summary>

- **Predictions:** `512x512 -> 512x512`

</details>

| Model ID | Size | Input | Output | Profile |
| ------------------------------- | -------- | ----- | ------ | ------- |
| [anime2sketch&nbsp;<sup>⬇️</sup>](https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/anime2sketch_CoreML/anime2sketch.mlpackage.zip) | 207.6 MB | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/readme-assets/Anime2Sketch_model_Input1.png" width="120" /> | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/readme-assets/anime2sketch.png" width="120" /> | base |
| [anime2sketch_xcode_LUT-4&nbsp;<sup>⬇️</sup>](https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/anime2sketch_CoreML/anime2sketch_xcode_LUT-4.mlpackage.zip) | 26.0 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/readme-assets/anime2sketch_xcode_LUT-4.png" width="120" /> | LUT-4 |
| [anime2sketch_xcode_LUT-6&nbsp;<sup>⬇️</sup>](https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/anime2sketch_CoreML/anime2sketch_xcode_LUT-6.mlpackage.zip) | 38.9 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/readme-assets/anime2sketch_xcode_LUT-6.png" width="120" /> | LUT-6 |
| [anime2sketch_xcode_Q-8&nbsp;<sup>⬇️</sup>](https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/anime2sketch_CoreML/anime2sketch_xcode_Q-8.mlpackage.zip) | 51.9 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/releases/download/readme-assets/anime2sketch_xcode_Q-8.png" width="120" /> | Q-8 |

## Author

Arshiya Rahgozar  
[GitHub](https://github.com/marshiyar)
[LinkedIn](https://www.linkedin.com/in/marshiyar/)

## Attributions

Thanks to the authors of Real-ESRGAN, NAFNet, DDColor, and Anime2Sketch for the original models and code.

<a id="footnotes"></a>
## Footnotes

[^1]: Real-world image super-resolution. Original project: [xinntao/Real-ESRGAN](https://github.com/xinntao/Real-ESRGAN) (BSD-3-Clause).

[^2]: Image denoising with NAFNet (SIDD-trained, width 64). Original: [megvii-research/NAFNet](https://github.com/megvii-research/NAFNet).

[^3]: Anime/style artwork to sketch conversion. Original: [Mukosame/Anime2Sketch](https://github.com/Mukosame/Anime2Sketch) (MIT).

[^4]: Grayscale image colorization. ModelScope variant. Original: [piddnad/DDColor](https://github.com/piddnad/DDColor).
