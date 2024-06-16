# Face Recognition with Occlusion and Orientation

## Overview

This project, guided by Dr. Mrinal Kanti Das and conducted by Abhishek S. Mayya (142302014) and Shreyansh Acharya (142302013), aims to investigate and enhance the robustness of face recognition systems under challenging conditions, specifically occlusion and orientation variations. The primary focus is on improving the performance of existing face recognition models in real-world scenarios where faces may be partially covered and captured from different angles.

## Problem Statement

The goal is to evaluate and improve the performance of face recognition systems when faces are occluded or oriented differently. This involves:
- Investigating the effects of occlusion and orientation on face recognition accuracy.
- Enhancing the robustness of face recognition models to handle these variations effectively.

 ![image](https://github.com/ShreyanshAcharya/Face-Recognition/assets/59439172/9622c133-a07f-48de-8b01-34d47473ee22)


## Dataset

- **Brazilian Face Dataset**: Contains 2800 images, 14 images for each of the 200 individuals, including 2 separate frontal images for each individual. Each image is labeled with a consistent FaceID for the same individual.
  
 ![image](https://github.com/ShreyanshAcharya/Face-Recognition/assets/59439172/f56417b0-3d08-4b9f-a1ae-b193be369887)


## Project Description

The project aims to enhance face recognition systems by:
1. Using existing face detection and recognition models.
2. Optimizing these models to handle occlusions and orientation variations.

### Starting Point

- **Face Detection**: Multi-task Cascaded Convolutional Networks (MTCNN)
- **Face Recognition**: VGG-Face model from the Visual Geometry Group

For more details on VGG-Face, visit the [GitHub repository](https://github.com/rcmalli/keras-vggface?tab=readme-ov-file).

## Face Extraction Using MTCNN

MTCNN is utilized for extracting faces from images due to its superior performance.

![image](https://github.com/ShreyanshAcharya/Face-Recognition/assets/59439172/01ee119c-3b41-4ef0-9247-5ed82deb0643)


## Applying Occlusion

Two types of occlusions are introduced:
1. **Central Occlusion**
2. **Peripheral Occlusion** (Left and Right)

![image](https://github.com/ShreyanshAcharya/Face-Recognition/assets/59439172/4d17afbb-b85a-4229-a441-66e6797d74d4)


Occlusions are applied by setting pixels to zero in rectangular shapes on the images, with occlusion levels of 5% and 15%.

## Applying Occlusion with Orientation

Occlusions of 15% are applied to images with different face orientations.

## Face Register

### Register1

- 200 frontal faces are extracted using MTCNN and passed through the pretrained VGG-Face model to obtain 512-dimensional embeddings.
- These embeddings are stored in a dictionary with FaceID as the key.

### Register2

- Includes 200 frontal faces, along with central, left, and right occlusion faces (4 images per individual).
- Embeddings for these faces are obtained using the VGG-Face model and averaged for each individual.

## Face Recognition Model

1. Faces are extracted from images using MTCNN.
2. Face registers (Register1 and Register2) are created.
3. Test images with occlusions and orientations are compared with the face registers.
4. The face ID of the most similar face from the register is assigned to the test image.

## Results – Pretrained Model with Register1

| Type of Data                  | Accuracy (%) | Type of Data                  | Accuracy (%) |
|-------------------------------|--------------|-------------------------------|--------------|
| Orientation                   | 94.5         | 5% Central Occlusion          | 95.0         |
| 15% Central Occlusion         | 78.5         | 5% Right Occlusion            | 98.5         |
| 15% Right Occlusion           | 80.5         | 5% Left Occlusion             | 99.0         |
| 15% Left Occlusion            | 91.0         |                               |              |

## Comparison – Pretrained Model

| Type of Data                   | Register1 (%) | Register2 (%) |
|--------------------------------|---------------|---------------|
| Orientation                    | 94.5          | 94.3          |
| 15% Central Occlusion          | 78.5          | 97.5          |
| 15% Right Occlusion            | 80.5          | 98.5          |
| 15% Left Occlusion             | 91.0          | 99.0          |
| 15% Central Occlusion + Orientation | 59.5          | 74.0          |
| 15% Right Occlusion + Orientation   | 71.0          | 78.0          |
| 15% Left Occlusion + Orientation    | 63.5          | 74.0          |

## Comparison – Trained Model

One convolution layer of the VGG-Face model is trained with 400 images. Predictions are made as follows:

| Type of Data                   | Register1 (%) | Register2 (%) |
|--------------------------------|---------------|---------------|
| Orientation                    | 92.0          | 93.0          |
| 15% Central Occlusion          | 85.5          | 98.5          |
| 15% Right Occlusion            | 85.0          | 100           |
| 15% Left Occlusion             | 92.0          | 99.5          |
| 15% Central Occlusion + Orientation | 56.0          | 72.5          |
| 15% Right Occlusion + Orientation   | 69.0          | 77.0          |
| 15% Left Occlusion + Orientation    | 58.5          | 70.5          |

## Heatmaps

Deeper convolution layers focus more on crucial facial features such as eyes and nose.

![image](https://github.com/ShreyanshAcharya/Face-Recognition/assets/59439172/121b4a98-3e2e-48e7-9d27-673eda04ed56)


## Observations

Using Register2, which includes both regular and occluded faces, consistently results in better accuracy. This highlights the importance of incorporating diverse data in training.

## Challenges

1. **Dependency Issues**: Encountered various library compatibility and version conflicts when installing VGG-Face.
2. **GPU Limitations**: Training models with large images was challenging due to GPU capacity limitations, affecting processing speed and scalability.
3. **Quality vs. Size**: Reducing image size to address GPU constraints led to a trade-off between quality and preserving crucial facial details.

## Conclusion

- MTCNN is effective for face extraction.
- VGG-Face accurately identifies crucial facial characteristics, enhancing accuracy in face recognition tasks with occlusions.
- Notable accuracy improvements were achieved, particularly with occluded and varied orientation images when using Register2.
- Due to higher training time, the model was only trained for 7 epochs. Training for more epochs could yield better results.

## Acknowledgements

Thank you for your attention and interest in this project.

---
