# AItaca Tech-Test-ML-Hand

## About the Project
This project started on `26/09/2023` and was completed within 2 weeks on `05/10/2023` for AItaca Tech-Test-ML-Hand.

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
   * Created two new folders; original and no_bg with each hand image + [:10] original folder name as unique ID.
   * Checked Images Sizes and Ratios, selected [1.87, 1.85] ratios to resize as size = (2160, 4000) and use it for the model.
   * Also checked no_bg hands manually, deleting the ones that were not showing true masks (other parts of the body, or the background)
   * Final Dataset length: 79 unique original and no_bg images. No bg_images were converted to true masks for predictions.
* Data Split:
   * Originally, it was a 80/10/10 split between training, validation and testing, using Data Augmentation to create 3 unique new images for training.
   * For the next models after the [MPV](https://github.com/isi-mube/Tech-Test-ML-Hand/blob/main/02_py/01_mvp.ipynb) I did a 65/15/10 split, using Data Augmentation to have 5 unique new images for training, and more images for validation. 
* Data Augmentation parameters:
  * **Brightness Range:** 0.5, 1.5
  * **Zoom Range:** 0.2
  * **Rotation Range:** 30
  * **Width & Height shift Range:** 0.1
  * **Horizontal Flip:** True
  * **Shear Range:** 0.1
* Image Pre-Processing: For some models, I tried all image-preprocessing I could to check if it improved performance. The best image pre-processing techniques to detect edges were Bilateral Filtering, CLAHE, Canny Edges and Dilatation. It did not improve performance so I ended up feeding the model with unprocessed images.
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

#@# Model: Eva X: 
<img width="928" alt="Screenshot 2023-10-04 at 19 54 09" src="https://github.com/isi-mube/Tech-Test-ML-Hand/assets/90038586/7dd521cd-d455-4b44-bbeb-e05c37ea60ed">

* Minimum Viable Product: [MPV](https://github.com/isi-mube/Tech-Test-ML-Hand/blob/main/02_py/01_mvp.ipynb)
* New Prototype (cleaning the code and explaining all the steps): [Prototype](https://github.com/isi-mube/Tech-Test-ML-Hand/blob/main/02_py/02_prototype.ipynb)
* [Final model Eva X](https://github.com/isi-mube/Tech-Test-ML-Hand/blob/main/02_py/12_eva_X.ipynb)


## Conclusions:
* The MPV was done and finished in the first week, on `29/09/2023`, showing some promising results.
* Image-preporcessing was not improving performance.
* The next models had more complex architecture, the maximum filters I could use was 128 without loosing performance. Using dropout and residual layers helped to create the prediction masks.
* I wanted to try different transfer learning models but hadn't time for that. Also, I thought about using object detection first to later on apply the segmentation.

## Toolkit:

* **JupyterLab**: Enviorment for Python scripts and managing files. AKA, as if VSCode and JupyterNotebook had a kid.

**Libraries**

📚 Basic Libraries
* **Pandas**: Data manipulation and analysis.
* **Numpy**: Arrays and mathematical functions, allowing it to read images.
* **Os**: File managment.
* **Matplotlib**: 2D Data visualization.
* **Seaborn**: Runs on top of matplotlib, HD data visualization.
* **PIL:** Python Imaging Library to manipulate images.

🛠️ Tools
* **Warnings**: Roses are red, violets are blue --> Warnings are annoying.
* **Shutil**: File operations (copying, deleting...).
* **Random:** To generate random subsets of data.

🌐 Computer Vision
* **TensorFlow:** Machine Learning for Computer Vision.
* **Keras:** High-level neural networks API for Deep Learning, running on top of TensorFlow.
* **ImageDataGenerator:** To generate random data augmentation (flips, zoom...).

📈 Metrics and Reports
* **Sklearn:** Machine Learning metrics.
* **Confusion Matrix:** To evaluate true and false positives and negatives.
* **Confusion Matrix Display:** To easily display the matrix.
* **Classification Report:** For a more accurate detail of each metrics (precision, recall, f1-score, support).


## Bibliography:
* Keras Team. Oxford Pets Image Segmentation. Keras. Retrieved from https://keras.io/examples/vision/oxford_pets_image_segmentation
* GeeksforGeeks Team. How to Normalize, Center, and Standardize Image Pixels in Keras. GeeksforGeeks. Retrieved from https://www.geeksforgeeks.org/how-to-normalize-center-and-standardize-image-pixels-in-keras
* Stack Overflow Community. Image and Mask Normalization in Semantic Segmentation for Cancer. Stack Overflow. Retrieved from https://stackoverflow.com/questions/67699174/image-and-mask-normalization-in-semantic-segmentation-for-cancer
* Analytics Vidhya Team. Getting Started with Image Processing using OpenCV. Analytics Vidhya. Retrieved from https://www.analyticsvidhya.com/blog/2023/03/getting-started-with-image-processing-using-opencv
* https://docs.opencv.org/4.x/d4/d13/tutorial_py_filtering.html
* https://www.sabrepc.com/blog/Deep-Learning-and-AI/Epochs-Batch-Size-Iterations
* https://machinelearningmastery.com/difference-between-a-batch-and-an-epoch/
