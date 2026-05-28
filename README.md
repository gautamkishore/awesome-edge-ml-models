# Awesome Edge ML Models

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](#contributing)

A curated list of machine learning models that can run locally on edge devices: phones, tablets, laptops, browsers, Raspberry Pi-class boards, Jetson/Coral/Arm devices, wearables, and microcontrollers.

This list prioritizes models with public weights, reproducible deployment paths, practical edge runtimes, and clear licensing.

## Contents

- [What counts as edge-ready?](#what-counts-as-edge-ready)
- [Legend](#legend)
- [Language Models](#language-models)
- [Vision-Language Models](#vision-language-models)
- [Computer Vision Backbones](#computer-vision-backbones)
- [Detection, Segmentation, Pose, and Tracking](#detection-segmentation-pose-and-tracking)
- [Speech and Audio](#speech-and-audio)
- [Embeddings and Retrieval](#embeddings-and-retrieval)
- [TinyML and Microcontroller Models](#tinyml-and-microcontroller-models)
- [Model Zoos and Collections](#model-zoos-and-collections)
- [Runtimes and Deployment Formats](#runtimes-and-deployment-formats)
- [Benchmarks](#benchmarks)
- [Contributing](#contributing)

## What counts as edge-ready?

A model can be added if it meets at least one of these criteria:

- Runs offline on a phone, tablet, laptop, browser, SBC, embedded GPU/NPU, or microcontroller.
- Has an official or community deployment path for LiteRT/TFLite, Core ML, ONNX, GGUF, ExecuTorch, MLC, WebGPU/WASM, MediaPipe, NCNN, MNN, TensorRT, Edge TPU, or TensorFlow Lite Micro.
- Has small/quantized variants designed for low memory, low latency, or battery-constrained use.
- Has benchmark evidence on real edge hardware or realistic CPU/NPU/GPU constraints.

Non-goals:

- Cloud-only APIs.
- Large server models with no credible edge path.
- Repos with no license or unclear weights.
- Marketing claims without weights, conversion path, or reproducible benchmark.

## Legend

| Tag | Meaning |
|---|---|
| `phone` | Practical for modern phones or tablets after quantization. |
| `high-end-phone` | Needs flagship mobile hardware, NPU/GPU, or aggressive quantization. |
| `laptop` | Practical on laptops, local desktops, or Apple Silicon-class devices. |
| `browser` | Runs through WebGPU, WebNN, WASM, or TensorFlow.js/ONNX Runtime Web. |
| `sbc` | Raspberry Pi, Jetson Nano/Orin Nano, Coral, Orange Pi, Arm boards. |
| `mcu` | Microcontrollers / TinyML-class devices. |
| `npu` | Has a deployment path for mobile/embedded NPUs. |
| `gguf` | Commonly usable with llama.cpp-compatible runtimes. |
| `tflite` | TensorFlow Lite / LiteRT / MediaPipe-compatible path. |
| `coreml` | Core ML-compatible path for Apple platforms. |
| `onnx` | ONNX / ONNX Runtime-compatible path. |

## Language Models

Small language models for on-device chat, summarization, rewriting, classification, tool calling, and local agents.

| Model | Size / family | Best for | Edge tags | Links |
|---|---:|---|---|---|
| Gemma 4 E2B / E4B | E2B, E4B | General text, reasoning, multimodal-adjacent apps on higher-end local hardware | `high-end-phone`, `laptop`, `npu` | [Overview](https://ai.google.dev/gemma/docs/core), [HF collection](https://huggingface.co/google) |
| Gemma 3n | E2B, E4B effective sizes | Offline mobile multimodal apps; text generation from text/image/audio/video inputs | `phone`, `high-end-phone`, `tflite`, `npu` | [Docs](https://ai.google.dev/gemma/docs/gemma-3n), [E2B model](https://huggingface.co/google/gemma-3n-E2B) |
| Gemma 3 1B IT | 1B | Small in-app text generation on Android/web | `phone`, `browser`, `tflite` | [Google AI Edge blog](https://developers.googleblog.com/gemma-3-on-mobile-and-web-with-google-ai-edge/), [LiteRT variant](https://huggingface.co/litert-community/Gemma3-1B-IT) |
| Llama 3.2 1B / 3B | 1B, 3B | Local summarization, rewriting, instruction following | `phone`, `high-end-phone`, `gguf`, `npu` | [Meta blog](https://ai.meta.com/blog/llama-3-2-connect-2024-vision-edge-mobile-devices/), [1B model](https://huggingface.co/meta-llama/Llama-3.2-1B) |
| SmolLM2 | 135M, 360M, 1.7B | Very small local assistants, classification, short-form generation | `phone`, `browser`, `gguf` | [Collection](https://huggingface.co/collections/HuggingFaceTB/smollm2), [135M](https://huggingface.co/HuggingFaceTB/SmolLM2-135M) |
| Qwen3 small dense models | 0.6B, 1.7B, 4B | Multilingual text generation, reasoning, local assistants | `phone`, `high-end-phone`, `gguf`, `onnx` | [Qwen3 blog](https://qwenlm.github.io/blog/qwen3/), [0.6B](https://huggingface.co/Qwen/Qwen3-0.6B) |
| Qwen2.5 small instruct | 0.5B, 1.5B | Efficient multilingual chat and agent-style tasks | `phone`, `gguf`, `onnx` | [0.5B Instruct](https://huggingface.co/Qwen/Qwen2.5-0.5B-Instruct), [1.5B Instruct](https://huggingface.co/Qwen/Qwen2.5-1.5B-Instruct) |
| MobileLLM | 125M, 350M, 600M, 1B, 1.5B | Research-grade sub-billion on-device LLMs | `phone`, `laptop` | [GitHub](https://github.com/facebookresearch/MobileLLM), [HF collection](https://huggingface.co/collections/facebook/mobilellm) |
| MobileLLM-Pro | 1B | Long-context local language modeling research | `phone`, `laptop` | [Model](https://huggingface.co/facebook/MobileLLM-Pro), [Paper](https://arxiv.org/abs/2511.06719) |
| MobileLLM-R1 | 950M | Small reasoning and coding research | `phone`, `laptop` | [Model](https://huggingface.co/facebook/MobileLLM-R1-950M) |
| LFM2 / LFM2.5 | 350M, 700M, 1.2B, larger | Fast local LLMs designed around edge constraints | `phone`, `laptop`, `npu` | [Models](https://www.liquid.ai/models), [LFM2-1.2B](https://huggingface.co/LiquidAI/LFM2-1.2B) |
| Phi-3 Mini | 3.8B | Local reasoning, coding, summarization on higher-end devices | `high-end-phone`, `laptop`, `gguf`, `onnx` | [Model](https://huggingface.co/microsoft/Phi-3-mini-4k-instruct), [Microsoft announcement](https://news.microsoft.com/source/features/ai/the-phi-3-small-language-models-with-big-potential/) |
| TinyLlama | 1.1B | Lightweight Llama-compatible experiments | `phone`, `gguf`, `tflite` | [Model](https://huggingface.co/TinyLlama/TinyLlama-1.1B-Chat-v1.0), [LiteRT variant](https://huggingface.co/litert-community/TinyLlama-1.1B-Chat-v1.0) |

## Vision-Language Models

Small multimodal models for image captioning, VQA, screen understanding, OCR-like tasks, pointing, and visual grounding.

| Model | Size / family | Best for | Edge tags | Links |
|---|---:|---|---|---|
| SmolVLM / SmolVLM2 | 256M, 500M, 2B/2.2B | Tiny VLMs for image/video understanding | `phone`, `browser`, `high-end-phone` | [SmolVLM blog](https://huggingface.co/blog/smolvlm), [SmolVLM2 blog](https://huggingface.co/blog/smolvlm2), [256M model](https://huggingface.co/HuggingFaceTB/SmolVLM-256M-Instruct) |
| Moondream | 2B dense, 9B MoE preview | Image captioning, VQA, detection/pointing on local devices | `phone`, `laptop`, `gguf` | [Website](https://moondream.ai/), [Moondream2 model](https://huggingface.co/vikhyatk/moondream2), [GitHub](https://github.com/m87-labs/moondream) |
| MobileVLM / MobileVLM V2 | 1.4B, 1.7B, 2.7B, 3B | Mobile-oriented VLM research and deployment | `phone`, `laptop`, `gguf` | [GitHub](https://github.com/Meituan-AutoML/MobileVLM), [Paper](https://arxiv.org/abs/2312.16886) |
| InternVL small variants | 1B+ | Lightweight multimodal understanding | `high-end-phone`, `laptop` | [InternVL2-1B](https://huggingface.co/OpenGVLab/InternVL2-1B), [InternVL3-1B](https://huggingface.co/OpenGVLab/InternVL3-1B) |
| FastVLM | multiple | Efficient vision encoder for VLM latency reduction | `phone`, `laptop`, `coreml` | [GitHub](https://github.com/apple/ml-fastvlm) |
| MobileCLIP | S0, S1, S2, B variants | Efficient image-text retrieval and zero-shot classification | `phone`, `coreml`, `onnx` | [Apple research](https://machinelearning.apple.com/research/mobileclip), [GitHub](https://github.com/apple/ml-mobileclip) |

## Computer Vision Backbones

Efficient feature extractors for classification, detection, segmentation, tracking, embedding, and transfer learning.

| Model | Task | Why it is useful on edge | Edge tags | Links |
|---|---|---|---|---|
| MobileNetV2 / MobileNetV3 | Classification backbone | Standard mobile CNN backbone; widely available in TFLite/Core ML/ONNX ecosystems | `phone`, `sbc`, `tflite`, `coreml`, `onnx` | [Keras apps](https://keras.io/api/applications/), [Apple MobileNet sample](https://developer.apple.com/documentation/CoreML/classifying-images-with-vision-and-core-ml) |
| EfficientNet-Lite | Classification backbone | Accuracy/latency tradeoff for TFLite deployments | `phone`, `sbc`, `tflite` | [TensorFlow Lite models](https://ai.google.dev/edge/litert/conversion/tensorflow/pretrained_models) |
| MobileViT | Classification / backbone | Hybrid CNN-transformer designed for mobile vision | `phone`, `coreml`, `onnx` | [Paper](https://arxiv.org/abs/2110.02178), [Apple CVNets](https://github.com/apple/ml-cvnets) |
| EfficientViT | Classification / dense prediction | Hardware-efficient vision transformer family | `phone`, `sbc`, `onnx` | [GitHub](https://github.com/mit-han-lab/efficientvit), [Paper](https://han-cai.github.io/selected_projects/efficientvit_iccv.pdf) |
| ShuffleNetV2 | Classification backbone | Very small CNN backbone for CPU-bound devices | `phone`, `sbc`, `onnx` | [Paper](https://arxiv.org/abs/1807.11164) |
| SqueezeNet | Classification backbone | Very small CNN baseline for constrained inference | `phone`, `sbc`, `onnx`, `coreml` | [Paper](https://arxiv.org/abs/1602.07360), [ONNX model zoo](https://github.com/onnx/models) |

## Detection, Segmentation, Pose, and Tracking

| Model | Task | Why it is useful on edge | Edge tags | Links |
|---|---|---|---|---|
| Ultralytics YOLO nano variants | Detection, segmentation, pose, OBB, classification | Popular real-time models with export paths to ONNX, Core ML, TFLite, TensorRT, and Edge TPU | `phone`, `sbc`, `coreml`, `tflite`, `onnx`, `npu` | [YOLO11 docs](https://docs.ultralytics.com/models/yolo11/), [Export docs](https://docs.ultralytics.com/modes/export/) |
| YOLOv5n / YOLOv8n | Object detection | Mature nano detectors with wide community deployment support | `phone`, `sbc`, `coreml`, `tflite`, `onnx` | [Ultralytics GitHub](https://github.com/ultralytics/ultralytics) |
| MobileNet SSD / SSDLite | Object detection | Classic mobile detection baseline; good for TFLite/Core ML examples | `phone`, `sbc`, `tflite`, `coreml` | [TF2 detection zoo](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/tf2_detection_zoo.md) |
| EfficientDet-Lite | Object detection | Edge-friendly detector family used in TFLite examples | `phone`, `sbc`, `tflite` | [TensorFlow Lite models](https://ai.google.dev/edge/litert/conversion/tensorflow/pretrained_models) |
| MediaPipe Face Detection / BlazeFace | Face detection | Real-time on-device face detection | `phone`, `browser`, `tflite`, `mediapipe` | [MediaPipe guide](https://ai.google.dev/edge/mediapipe/solutions/guide) |
| MediaPipe Face Landmarker | Face landmarks | Face mesh / landmarks for AR and camera effects | `phone`, `browser`, `tflite`, `mediapipe` | [MediaPipe tasks](https://ai.google.dev/edge/mediapipe/solutions/guide) |
| MediaPipe Hand Landmarker | Hand tracking | Real-time hand landmarks for gesture and AR apps | `phone`, `browser`, `tflite`, `mediapipe` | [MediaPipe Hands paper](https://arxiv.org/abs/2006.10214) |
| MediaPipe Pose Landmarker | Pose estimation | Real-time human pose and fitness/motion features | `phone`, `browser`, `tflite`, `mediapipe` | [MediaPipe guide](https://ai.google.dev/edge/mediapipe/solutions/guide) |
| MediaPipe Gesture Recognizer | Gesture recognition | Camera-based gesture UX on device | `phone`, `browser`, `tflite`, `mediapipe` | [MediaPipe guide](https://ai.google.dev/edge/mediapipe/solutions/guide) |
| MediaPipe Image Segmenter | Segmentation | On-device semantic/selfie segmentation pipelines | `phone`, `browser`, `tflite`, `mediapipe` | [MediaPipe guide](https://ai.google.dev/edge/mediapipe/solutions/guide) |
| MobileSAM / MobileSAMv2 | Promptable segmentation | Lightweight Segment Anything variant for mobile/edge use | `phone`, `laptop`, `onnx` | [GitHub](https://github.com/chaoningzhang/MobileSAM), [Ultralytics docs](https://docs.ultralytics.com/models/mobile-sam/) |
| EdgeSAM | Promptable segmentation | SAM-style segmentation optimized for on-device deployment | `phone`, `laptop`, `onnx` | [Paper](https://arxiv.org/abs/2312.06660) |
| NanoDet | Object detection | Lightweight anchor-free detector for mobile CPU/GPU | `phone`, `sbc`, `ncnn`, `onnx` | [GitHub](https://github.com/RangiLyu/nanodet) |
| PicoDet | Object detection | Lightweight detector from PaddleDetection | `phone`, `sbc`, `onnx` | [PaddleDetection](https://github.com/PaddlePaddle/PaddleDetection) |

## Speech and Audio

| Model | Task | Why it is useful on edge | Edge tags | Links |
|---|---|---|---|---|
| Whisper tiny/base/small | ASR, translation, language ID | Strong multilingual ASR; tiny/base variants are popular for local transcription | `phone`, `laptop`, `coreml`, `ggml` | [OpenAI Whisper](https://github.com/openai/whisper), [whisper.cpp](https://github.com/ggerganov/whisper.cpp) |
| Vosk small models | Offline ASR | Small offline ASR models for Android, iOS, Raspberry Pi | `phone`, `sbc` | [Vosk](https://alphacephei.com/vosk/), [Models](https://alphacephei.com/vosk/models) |
| Silero VAD | Voice activity detection | Lightweight speech/silence detection; useful before ASR | `phone`, `sbc`, `onnx` | [GitHub](https://github.com/snakers4/silero-vad) |
| Porcupine | Wake word detection | Always-on on-device keyword spotting | `phone`, `mcu`, `sbc` | [Product](https://picovoice.ai/products/voice/wake-word/), [GitHub](https://github.com/Picovoice/porcupine) |
| YAMNet | Audio event classification | Lightweight environmental audio classification | `phone`, `browser`, `tflite`, `tfjs` | [TF Hub](https://tfhub.dev/google/yamnet/1), [TensorFlow.js models](https://www.tensorflow.org/js/models) |
| RNNoise | Noise suppression | Small recurrent denoising model for real-time audio | `phone`, `sbc` | [GitHub](https://github.com/xiph/rnnoise) |
| DeepFilterNet | Noise suppression | Neural real-time speech enhancement | `phone`, `laptop`, `sbc` | [GitHub](https://github.com/Rikorose/DeepFilterNet) |

## Embeddings and Retrieval

Compact embedding models for local semantic search, RAG indexes, clustering, recommendations, and private search.

| Model | Size / dim | Best for | Edge tags | Links |
|---|---:|---|---|---|
| all-MiniLM-L6-v2 | 384-dim | General semantic search and clustering | `phone`, `browser`, `onnx` | [Model](https://huggingface.co/sentence-transformers/all-MiniLM-L6-v2) |
| BAAI/bge-small-en-v1.5 | 384-dim | English retrieval with small memory footprint | `phone`, `laptop`, `onnx` | [Model](https://huggingface.co/BAAI/bge-small-en-v1.5), [FastEmbed support](https://qdrant.github.io/fastembed/examples/Supported_Models/) |
| jina-embeddings-v2-small-en | 512-dim | Long-context English retrieval in a smaller model | `phone`, `laptop`, `onnx` | [Model](https://huggingface.co/jinaai/jina-embeddings-v2-small-en), [FastEmbed support](https://qdrant.github.io/fastembed/examples/Supported_Models/) |
| snowflake-arctic-embed-s | 384-dim | Lightweight English retrieval | `phone`, `laptop`, `onnx` | [Model](https://huggingface.co/Snowflake/snowflake-arctic-embed-s), [FastEmbed support](https://qdrant.github.io/fastembed/examples/Supported_Models/) |
| Universal Sentence Encoder Lite | 512-dim | Browser/mobile sentence similarity | `browser`, `phone`, `tfjs`, `tflite` | [TF Hub tutorial](https://www.tensorflow.org/hub/tutorials/semantic_similarity_with_tf_hub_universal_encoder_lite), [Kaggle model](https://www.kaggle.com/models/tensorflow/universal-sentence-encoder) |
| Qwen3 Embedding 0.6B | 0.6B | Multilingual retrieval when a larger local model is acceptable | `high-end-phone`, `laptop` | [Paper](https://arxiv.org/abs/2506.05176), [Qwen HF](https://huggingface.co/Qwen) |

## TinyML and Microcontroller Models

Models and model families for extremely constrained devices.

| Model / family | Task | Why it is useful on edge | Edge tags | Links |
|---|---|---|---|---|
| TensorFlow Lite Micro `micro_speech` | Keyword spotting | Canonical TinyML speech example | `mcu`, `tflite` | [TFLite Micro](https://github.com/tensorflow/tflite-micro), [Arm example](https://github.com/ARM-software/AVH-TFLmicrospeech) |
| TensorFlow Lite Micro `person_detection` | Visual wake word / person detection | Tiny camera model for MCU-class demos | `mcu`, `tflite` | [TFLite Micro](https://github.com/tensorflow/tflite-micro) |
| MLPerf Tiny reference models | KWS, visual wake words, image classification, anomaly detection | Reproducible benchmark models for ultra-low-power systems | `mcu`, `tflite` | [MLPerf Tiny](https://github.com/mlcommons/tiny), [Paper](https://arxiv.org/abs/2106.07597) |
| Arm ML Zoo | KWS, image classification, object detection, speech, super-resolution, anomaly detection | INT8 models for Cortex-A, Cortex-M, Mali GPU, and Ethos-U | `mcu`, `sbc`, `npu`, `tflite` | [GitHub](https://github.com/Arm-Examples/ML-zoo), [Docs](https://developer.arm.com/documentation/109267/) |
| Edge Impulse FOMO | Object detection | Real-time object detection/tracking/counting for constrained devices | `mcu`, `sbc`, `tflite` | [Docs](https://docs.edgeimpulse.com/studio/projects/learning-blocks/blocks/object-detection/fomo), [Tutorial](https://docs.edgeimpulse.com/tutorials/end-to-end/object-detection-centroids) |

## Model Zoos and Collections

| Collection | What it contains | Links |
|---|---|---|
| Google AI Edge / LiteRT models | Pretrained and converted models for mobile/edge deployment | [LiteRT pretrained models](https://ai.google.dev/edge/litert/conversion/tensorflow/pretrained_models), [Google AI Edge](https://ai.google.dev/edge) |
| MediaPipe Models | Ready-to-run on-device models for common vision/audio/text tasks | [Solutions guide](https://ai.google.dev/edge/mediapipe/solutions/guide) |
| Apple Core ML Models | Core ML-ready models for Apple platforms | [Core ML Models](https://developer.apple.com/machine-learning/models/) |
| TensorFlow.js models | Browser-side pretrained models | [TF.js models](https://www.tensorflow.org/js/models) |
| Arm ML Zoo | Embedded/TinyML models for Arm targets | [Arm ML Zoo](https://github.com/Arm-Examples/ML-zoo) |
| ONNX Model Zoo | ONNX-format model examples and baselines | [ONNX models](https://github.com/onnx/models) |
| Hugging Face LiteRT community | Android-ready LiteRT variants of selected LLMs | [litert-community](https://huggingface.co/litert-community) |
| Awesome TFLite | Community collection of TensorFlow Lite models, apps, and tools | [awesome-tflite](https://github.com/iglaweb/awesome-tflite) |
| Awesome Mobile LLM | Papers and resources for mobile/on-device LLMs | [awesome-mobile-llm](https://github.com/stevelaskaridis/awesome-mobile-llm) |

## Runtimes and Deployment Formats

This section is for deploying the models above, not for adding every runtime in the ecosystem.

| Runtime / format | Good for | Links |
|---|---|---|
| LiteRT / TensorFlow Lite | Android, embedded Linux, microcontrollers, MediaPipe | [LiteRT](https://ai.google.dev/edge/litert), [TFLite Micro](https://github.com/tensorflow/tflite-micro) |
| MediaPipe | Cross-platform on-device pipelines | [MediaPipe](https://ai.google.dev/edge/mediapipe/solutions/guide) |
| Core ML | iOS, macOS, iPadOS, visionOS, watchOS | [Core ML](https://developer.apple.com/machine-learning/core-ml/) |
| ExecuTorch | PyTorch-native mobile/edge deployment | [ExecuTorch](https://pytorch.org/executorch/) |
| ONNX Runtime | CPU/GPU/NPU inference across platforms | [ONNX Runtime](https://onnxruntime.ai/) |
| llama.cpp / GGUF | Local LLMs and VLMs on CPU/GPU/mobile | [llama.cpp](https://github.com/ggerganov/llama.cpp) |
| whisper.cpp | Local Whisper ASR on CPU/GPU/Core ML | [whisper.cpp](https://github.com/ggerganov/whisper.cpp) |
| MLC LLM | Mobile, desktop, and browser LLM deployment | [MLC LLM](https://llm.mlc.ai/) |
| TensorFlow.js | Browser and Node.js inference | [TensorFlow.js](https://www.tensorflow.org/js) |
| Transformers.js | Browser-side transformer inference | [Transformers.js](https://github.com/huggingface/transformers.js) |
| NCNN | Mobile CPU/GPU inference, common on Android | [NCNN](https://github.com/Tencent/ncnn) |
| MNN | Mobile and embedded inference | [MNN](https://github.com/alibaba/MNN) |
| TensorRT / TensorRT-LLM | Jetson and NVIDIA edge GPUs | [TensorRT](https://developer.nvidia.com/tensorrt), [TensorRT-LLM](https://github.com/NVIDIA/TensorRT-LLM) |
| Edge TPU | Coral accelerators | [Coral models](https://coral.ai/models/) |

## Benchmarks

Use these to validate that a model is actually edge-friendly.

| Benchmark / tool | Measures | Links |
|---|---|---|
| MLPerf Tiny | Accuracy, latency, energy for ultra-low-power tasks | [MLPerf Tiny](https://github.com/mlcommons/tiny), [v1.3 post](https://mlcommons.org/2025/09/mlperf-tiny-v1-3-tech/) |
| Android Benchmark / MediaPipe demos | On-device latency and UX for Android | [MediaPipe](https://ai.google.dev/edge/mediapipe/solutions/guide) |
| Core ML performance reports | Apple Neural Engine / CPU / GPU behavior | [Core ML optimization WWDC](https://developer.apple.com/videos/play/wwdc2024/10161/) |
| ONNX Runtime profiling | CPU/GPU/NPU operator performance | [ONNX Runtime profiling](https://onnxruntime.ai/docs/performance/tune-performance/profiling-tools.html) |
| llama.cpp benchmarks | Local LLM prefill/decode throughput | [llama.cpp](https://github.com/ggerganov/llama.cpp) |
| whisper.cpp benchmarks | Local ASR throughput | [whisper.cpp](https://github.com/ggerganov/whisper.cpp) |

## Contributing

Pull requests are welcome.

### Entry checklist

Each model entry should include:

- Model name and upstream link.
- Task: classification, detection, segmentation, ASR, VAD, embedding, LLM, VLM, etc.
- Size: parameters, file size, memory use, or quantized size when available.
- Edge target: phone, browser, SBC, Jetson, Edge TPU, NPU, MCU, Apple Neural Engine, etc.
- Runtime or format: LiteRT/TFLite, Core ML, ONNX, GGUF, ExecuTorch, MLC, WebGPU/WASM, NCNN, MNN, TensorRT, MediaPipe.
- License link.
- Evidence: benchmark, demo, paper, model card, hardware test, or conversion guide.

### Suggested entry format

```md
| Model Name | Size / family | One-line use case | `phone`, `onnx` | [Model](https://example.com), [Benchmark](https://example.com) |
```

### Curation rules

- Prefer official repos/model cards over mirrors.
- Prefer models with weights and a real deployment path.
- Do not add a model just because it is “small”; add it because it is useful and deployable.
- Mark research-only models clearly when production deployment is not mature.
- Avoid duplicate forks unless the fork adds a meaningful edge runtime, quantization, or benchmark.
- Check licenses before recommending production use.

