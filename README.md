# Image Hand Segmentation
![Company Logo](https://aitaca.io/wp-content/uploads/2020/01/logo_loading.png)

## About the Project
This project started on `26/09/2023` and was completed within 2 weeks on `05/10/2023` for [AItaca Tech-Test-ML-Hand](https://aitaca.io/).

Primary Objective:
<ul>
  <li>Develop a segmentation model that removes hands from the background with high precision.</li>
</ul>

Secondary Objectives:
<ul>
  <li>Implement a web-based application using Streamlit, using user-input hand images and segmented images as the output.</li>
</ul>

## Challenges and Project Development
* Data Cleaning:
    * Created two folders named 'original' and 'no_bg'. Each hand image in these folders has a unique ID which is the original folder name appended with its index ([:10]).
    * Examined image sizes and ratios. Chose ratios [1.87, 1.85] to resize images to dimensions (2160, 4000) for the model.
    * Manually reviewed 'no_bg' images, discarding those that did not display accurate masks (like other body parts or the background).
    * The final dataset consisted of 79 unique original and 'no_bg' images. 'No_bg' images were transformed into true masks for predictions.
* Data Split:
    * Initially, the dataset was split in an 80/10/10 ratio for training, validation, and testing respectively. Used Data Augmentation to produce 3 unique new images for training.
    * For subsequent models post the MVP, adopted a 65/15/10 split. Enhanced Data Augmentation to generate 5 unique new images for training and allocated more images for validation.
* Data Augmentation:
Parameters used:
  * **Brightness Range:** 0.5, 1.5
  * **Zoom Range:** 0.2
  * **Rotation Range:** 30
  * **Width & Height shift Range:** 0.1
  * **Horizontal Flip:** True
  * **Shear Range:** 0.1
* Image Pre-Processing:
Tried multiple pre-processing techniques, unprocessed images were eventually used as they yielded better performance.
  * **Normalization:** Pixel Normalization
  * **Noise reduction:** Bilateral Filtering
  * **Histogram Equalization:** CLAHE
  * **Edge detection:** Canny Edges
  * **Morphological Operations:** Dilatation

## Results
### MVP (Minimum Viable Product):
![image](https://github.com/isi-mube/Tech-Test-ML-Hand/assets/90038586/350359ea-a197-475e-b67f-35132e11b055)
 
### Model: Eva VIII:
![image](https://github.com/isi-mube/Tech-Test-ML-Hand/assets/90038586/ad02f4b9-683e-474b-aec8-611bae660238)

## Model: Eva X: 
<img width="928" alt="Screenshot 2023-10-04 at 19 54 09" src="https://github.com/isi-mube/Tech-Test-ML-Hand/assets/90038586/7dd521cd-d455-4b44-bbeb-e05c37ea60ed">

## Notebooks
* Minimum Viable Product: [MPV](https://github.com/isi-mube/Tech-Test-ML-Hand/blob/main/02_py/01_mvp.ipynb)
* New Prototype (Explained all the Steps and cleaned MPV code): [Prototype](https://github.com/isi-mube/Tech-Test-ML-Hand/blob/main/02_py/02_prototype.ipynb)
* [Final model Eva X](https://github.com/isi-mube/Tech-Test-ML-Hand/blob/main/02_py/12_eva_X.ipynb)


## Conclusions:
* The MPV was done and finished in the first week, on `29/09/2023`, showing some promising results.
* Pre-processing the images did not improve performance.
* Succeeding models were architecturally more intricate, with a limit of 128 filters for optimum performance. Incorporating dropout and residual layers was beneficial for generating prediction masks.
* While there was an intent to experiment with various transfer learning models, time constraints prevented this. Another potential enhancement considered was using object detection before segmentation and fine-tuning some hyperparameters.

## Toolkit:

* **JupyterLab**: Enviorment for Python scripts and managing files.

**Libraries**

📚 Basic Libraries
* **Numpy**: Image numeric array manipulation
* **Os**: File access.
* **Matplotlib**: Visualization.
* **Shutil**: Folder operations (copying, deleting...).
* **Random:** To generate random subsets of data.
* **Warnings**: Roses are red, violets are blue --> Warnings are annoying.

🌐 Computer Vision
* **TensorFlow:** Machine Learning for Computer Vision.
* **Keras:** High-level neural networks API for Deep Learning, running on top of TensorFlow.
* **ImageDataGenerator:** To generate random data augmentation (flips, zoom...).

## Bibliography:
* Keras Team. Oxford Pets Image Segmentation. Keras. Retrieved from https://keras.io/examples/vision/oxford_pets_image_segmentation
* GeeksforGeeks Team. How to Normalize, Center, and Standardize Image Pixels in Keras. GeeksforGeeks. Retrieved from https://www.geeksforgeeks.org/how-to-normalize-center-and-standardize-image-pixels-in-keras
* Stack Overflow Community. Image and Mask Normalization in Semantic Segmentation for Cancer. Stack Overflow. Retrieved from https://stackoverflow.com/questions/67699174/image-and-mask-normalization-in-semantic-segmentation-for-cancer
* Analytics Vidhya Team. Getting Started with Image Processing using OpenCV. Analytics Vidhya. Retrieved from https://www.analyticsvidhya.com/blog/2023/03/getting-started-with-image-processing-using-opencv
* OpenCV Documentation (n.d.). Image Filtering. OpenCV Official Documentation. Retrieved from https://docs.opencv.org/4.x/d4/d13/tutorial_py_filtering.html
* SabrePC Blog (n.d.). Understanding the Difference Between Epochs, Batch Size and Iterations. SabrePC Blog. Retrieved from https://www.sabrepc.com/blog/Deep-Learning-and-AI/Epochs-Batch-Size-Iterations
* Brownlee, J. (n.d.). Difference Between a Batch and an Epoch. Machine Learning Mastery. Retrieved from https://machinelearningmastery.com/difference-between-a-batch-and-an-epoch/
