# pet_emotion_detector_cnn

Pet emotion classifier using convolutional neural networks.

## Data Preparation
### Database
For the training of the classifier, the [Dog Emotions Prediction](https://www.kaggle.com/datasets/devzohaib/dog-emotions-prediction?resource=download) database was used as a starting point.
As a first step, the face of each animal was cropped using the dlib library with a [model](https://github.com/kairess/dog_face_detector) trained to recognize animal faces provided by @kairess. After that, a manual curation was carried out in the classes, excluding noisy images and rearranging images that were in incorrect classes.

### Data augmentation
Data augmentation was performed on the training data at a ratio of 10 to 1, that is, for each image, another 10 derived images were generated using the ImageDataGenerator library. Each image was resized to be 250x250 in size.

## Model Training
Two main models were used, the Densenet121 and the Densenet201. For each of them, the following techniques were used:

- EarlyStopping: Based on validation accuracy, a patience of 15 epochs was set for the model to stop if there was no evolution in this metric.
- The base layers of the Dense were frozen to avoid retraining.
- The base layer, a flatten layer, a dense layer with 512 neurons, a 50% dropout for this layer, and an output layer with 4 neurons, one for each class, were used.
- A learning rate decay per epoch was used, starting at 1e-3 and ending at 1e-5.

## Model Application
Given an image to be classified in a format accepted by keras image, the classification code searches for animals, crops the face, and applies it to the previously trained model, classifying the animal's mood as "angry", "happy", "sad", or "relaxed".

## Results
In the best model, using Densenet201, an accuracy of 73% was achieved on the test data.

### Download Links for Models
Put the files in the cnn_models folder.
- [Densenet121](https://1drv.ms/u/s!Agbyu4vkkajhhoEEZDRzJ4Dpa0QZdQ?e=psHgI4)
- [Densenet201](https://1drv.ms/u/s!Agbyu4vkkajhhoEFmxO5TiOi2zmkdA?e=t8RrmM)