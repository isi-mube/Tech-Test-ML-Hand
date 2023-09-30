# Hand Segmentation in Images
## MVP (Minimum Viable Product):
![image](https://github.com/isi-mube/Tech-Test-ML-Hand/assets/90038586/350359ea-a197-475e-b67f-35132e11b055)

## New Prototype:
![image](https://github.com/isi-mube/Tech-Test-ML-Hand/assets/90038586/2efa3326-98d7-4ce4-91c8-38c71bd15a82)

### New Operations:
### Train-Validation-Test Split: 65% for Training (It'll be later on augmented), 25% for Validation, 10% for Testing.

### Data Augmentation (5 new images for Training Folder, instead of 3):
* **Brightness Range:** 0.5, 1.5
* **Zoom Range:** 0.2
* **Rotation Range:** 30
* **Width & Height shift Range:** 0.1
* **Horizontal Flip:** True
* **Shear Range:** 0.1


### Image Pre-Processing Chosen:
* **Normalization:** Pixel Normalization
* **Noise reduction:** Bilateral Filtering
* **Histogram Equalization:** CLAHE
* **Edge detection:** Canny Edges
* **Morphological Operations:** Dilatation

### Modeling:
* U-Net: Same architecture as the MVP

## Bibliography:
* Keras Team. Oxford Pets Image Segmentation. Keras. Retrieved from https://keras.io/examples/vision/oxford_pets_image_segmentation
* GeeksforGeeks Team. How to Normalize, Center, and Standardize Image Pixels in Keras. GeeksforGeeks. Retrieved from https://www.geeksforgeeks.org/how-to-normalize-center-and-standardize-image-pixels-in-keras
* Stack Overflow Community. Image and Mask Normalization in Semantic Segmentation for Cancer. Stack Overflow. Retrieved from https://stackoverflow.com/questions/67699174/image-and-mask-normalization-in-semantic-segmentation-for-cancer
* Analytics Vidhya Team. Getting Started with Image Processing using OpenCV. Analytics Vidhya. Retrieved from https://www.analyticsvidhya.com/blog/2023/03/getting-started-with-image-processing-using-opencv
* https://docs.opencv.org/4.x/d4/d13/tutorial_py_filtering.html
