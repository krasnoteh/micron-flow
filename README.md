# Micron-Flow: Real-Time Optical Flow Model

## Model Overview
**Micron-Flow** is a lightweight optical flow model optimized for real-time inference at **80+ FPS** on high-end GPUs. By leveraging knowledge distillation from RAFT-Large, this model achieves **high accuracy** while maintaining an extremely small size of **522K parameters**.

## Model Details
- **Architecture**: Modified U-Net with MobileNetV2-based Siamese encoder, residual blocks, and a flow refinement module.
- **Parameters**: 522K
- **Input Resolution**: (152, 240)
- **Training Dataset**: 200K video frame pairs generated from the **Moments of Time** dataset using RAFT-Large.
- **Distillation Approach**: 
  - Mean squared error (MSE) loss in tanh-space
  - Edge-aware smoothness loss
- **Optimization**: Trained with **CosineAnnealing** scheduler and progressive encoder unfreezing.

## Performance
| Device       | Inference Time | FPS  |
|-------------|---------------|------|
| **RTX 4090** | 0.012 sec     | 83   |
| **GTX 1650** | 0.013 sec       | 76 |
| **CPU-Only** | 0.07 sec      | 14   |

## Key Features
- **Real-time processing**: 80+ FPS on RTX 4090
- **Small model size**: Only 2.1MB on disk
- **Efficient architecture**: 
  - Depthwise convolutions for reduced parameters
  - Inverted residual blocks for better efficiency
  - Flow refiner for enhanced motion consistency
- **Optimized training pipeline**: GPU caching and JPEG decoding acceleration

## Limitations
- Trained on synthetic optical flow from RAFT-Large, which may introduce biases.
- Resolution fixed to (152, 240) – requires up/downscaling for different input sizes.


## Model Weights
The trained weights are available on [Hugging Face](https://huggingface.co/krasnoteh/micron-flow).
