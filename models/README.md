# Self-hosted demo models

These ONNX models are served directly from tathastha.com for the Playground demos — no third-party
model host is queried at runtime, consistent with the site's edge-first approach.

## ppe-detection/

- **Architecture**: DETR (ResNet-50 backbone)
- **Fine-tuned checkpoint**: [`devonho/detr-resnet-50_finetuned_cppe5`](https://huggingface.co/devonho/detr-resnet-50_finetuned_cppe5) on Hugging Face
- **Training dataset**: [CPPE-5](https://huggingface.co/datasets/rishitdagli/cppe-5) (Coverall, Face_Shield, Gloves, Goggles, Mask)
- **Conversion**: exported to ONNX via Hugging Face Optimum, dynamically quantized to `QUInt8` via ONNX Runtime (166MB → 42.8MB)
- **License**: dataset and base DETR model are both openly licensed for research/demo use; see the Hugging Face model card for full terms

## hardhat-detection/

- **Architecture**: YOLOv8n (2 classes: `Hardhat`, `NO-Hardhat`)
- **Pretrained checkpoint**: [`keremberke/yolov8n-hard-hat-detection`](https://huggingface.co/keremberke/yolov8n-hard-hat-detection) on Hugging Face
- **Conversion**: exported to ONNX directly via Ultralytics' built-in exporter (opset 17, simplified)
- **License**: Ultralytics YOLOv8 weights are distributed under **AGPL-3.0** by Ultralytics. Since this model is served publicly from this repository (a form of "hosting a product built with it"), the complete corresponding source for this integration is the public `Tathastha-Labs/website` repository itself, satisfying AGPL-3.0's source-availability requirement. Do not extract and redistribute `model.onnx` on its own without equivalent source-availability.

## Face detection & recognition (Worker ID demo)

The worker-identification demo does not use a self-hosted model — it loads [`@vladmandic/face-api`](https://github.com/vladmandic/face-api) (MIT licensed) and its bundled TensorFlow.js face-detection/recognition weights directly from its CDN distribution. See that demo's page for details.
