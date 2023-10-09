# 🐍 About Neural Networks, Deep Learning and Image Segmentation</h1>

The architecture I've implemented is a variant of the U-Net model, a popular architecture for semantic image segmentation:

<div style="padding:10px; background-color: #f5f5f5;">
<pre>
    # First Downsampling Block
    x = layers.Conv2D(32, (3, 3), activation='relu', padding='same')(inputs)
    x = layers.BatchNormalization()(x)
    x = layers.Conv2D(32, (3, 3), activation='relu', padding='same')(x)
    x = layers.BatchNormalization()(x)
    x = layers.Conv2D(32, (3, 3), activation='relu', padding='same')(x)
    x = layers.BatchNormalization()(x)
    x = layers.Dropout(0.2)(x)
    residual_1 = x
    x = layers.MaxPooling2D((2, 2))(x)

    # Second Downsampling Block
    x = layers.Conv2D(64, (3, 3), activation='relu', padding='same')(x)
    x = layers.BatchNormalization()(x)
    x = layers.Conv2D(64, (3, 3), activation='relu', padding='same')(x)
    x = layers.BatchNormalization()(x)
    x = layers.Conv2D(64, (3, 3), activation='relu', padding='same')(x)
    x = layers.BatchNormalization()(x)
    x = layers.Dropout(0.3)(x)
    residual_2 = x
    x = layers.MaxPooling2D((2, 2))(x)

    # Bottleneck
    x = layers.Conv2D(128, (3, 3), activation='relu', padding='same')(x)
    x = layers.BatchNormalization()(x)
    x = layers.Conv2D(128, (3, 3), activation='relu', padding='same')(x)
    x = layers.BatchNormalization()(x)
    x = layers.Conv2D(128, (3, 3), activation='relu', padding='same')(x)
    x = layers.BatchNormalization()(x)
    x = layers.Dropout(0.4)(x)

    # Upsampling
    x = layers.Conv2DTranspose(64, (2, 2), strides=(2, 2), padding='same')(x)
    x = layers.Conv2D(64, (3, 3), activation='relu', padding='same')(x)
    x = layers.BatchNormalization()(x)
    x = layers.Conv2D(64, (3, 3), activation='relu', padding='same')(x)
    x = layers.BatchNormalization()(x)
    x = layers.Conv2D(64, (3, 3), activation='relu', padding='same')(x)
    x = layers.BatchNormalization()(x)
    x = layers.Dropout(0.3)(x)
    x = layers.add([x, residual_2])

    x = layers.Conv2DTranspose(32, (2, 2), strides=(2, 2), padding='same')(x)
    x = layers.Conv2D(32, (3, 3), activation='relu', padding='same')(x)
    x = layers.BatchNormalization()(x)
    x = layers.Conv2D(32, (3, 3), activation='relu', padding='same')(x)
    x = layers.BatchNormalization()(x)
    x = layers.Conv2D(32, (3, 3), activation='relu', padding='same')(x)
    x = layers.BatchNormalization()(x)
    x = layers.Dropout(0.2)(x)
    x = layers.add([x, residual_1])
</pre>

![image](https://github.com/isi-mube/Tech-Test-ML-Hand/assets/90038586/3181e8ab-7697-46ab-94b9-6d1d3df0bce7)


* Conv2D Layer: Convolutional layer of the network, where the image pre-processing happens and the kernel filter the image on the whole image, detecting lines and edges. `32`, `64`, `128` refers to the umber of filters used, starting from a small number. `Relu` activation adds non-linearity to the model, to learn more complex patterns. `Padding='same` ensures that the output feature map has the same width and height as the input. `Batch normalization` is applied after each convolution to stabilize and speed up training.
* MaxPooling2D Layer:  It performs downsampling operations, and also spatial dimensions (width, height), reducing overfitting and the computional cost by decreasing the spatial dimensionality.
* Dropout Layer: Helps in preventing overfitting by randomly setting a fraction of input units to 0 at each update during training.
* Bottleneck: The central part of the U-Net which doesn't have a skip connection to capture the most abstract features of the image.
* Conv2DTranspose Layer & Residual Connections: The transpose layers, often referred to as deconvolutional layers, help in upsampling the features. `Residual connections` from the downsampling path are added to these upsampled features. This is crucial as these connections help in localizing and refining the segmented regions.
* Output Layer: Produces the segmented image. The `sigmoid` activation function ensures pixel values are in the [0,1] range.

    
