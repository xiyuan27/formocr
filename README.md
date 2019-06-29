

# Formocr
Form parsing project(For Internship at IITB)

# Pipeline:
The pipeline for the project consists of the following steps:</br>
## 1)Faster RCNN based object detection:</br>
First we pass the input image through faster RCNN model to detect the date and A/C no fields.</br>
The model was trained on 10 Images from the validation set provided.</br>
The model was technicaly overfit onto the 10 Images because we only need to learn 1 template and do not have the requirement for generalization over differnent templates.</br>
Overfitting the model onto one template provides significant accuracy in detection on that particular template at the cost of generalization accross templates.</br>
The model was trained using the luminoth library ([Luminoth](https://github.com/tryolabs/luminoth)) which is an interface to train and use object detection models.</br>
The model was trained for 550 epochs.</br>

The Trained model is used to get Reigons of Intrest which are then extracted and then passed onto the next part of the pipeline.</br>
#### Reigons of Intrest extracted:</br>















## 2)Charater Segmentation:</br>
Characters are segmented from the Reigions of Intrest(ROI) using traditional Computer vision and Image processing techniques.
Each ROI image is first converted to grayscale.</br>
The Grayscale Image is then Blurred using gaussian blur which is used to remove noise and smooth around edges.</br>
The Blurred Image is later binirized using Otsu thresholding.</br>
The we find countours which are later sorted.</br>
After recieving the coordinates of all the countours we extract all the ones which satisfy predefined parameters.</br>
These extracted countours are then saved in their respective directories.

#### Segmented Characters:














## 3)Prediction:</br>
The segmented characters are then passed through the clasifier model to obtain predictions
#### Classifier Model:</br>
The Classifier model is a simple convolutional neural network with 2 convolutional layers  and 2 fully connected layers but,it also includes a [Spatial Transformer Network Module](https://arxiv.org/abs/1506.02025).</br>
The primary Advantage of spatial transformer networks is that they make the model invariant to transformations in the input image by learning the transformations to apply to the input image which normailizes them.</br>
They also dont need any special kind of training ,they just learn from normal training procedure.</br>
The model was trained on the MNIST dataset for 20 epochs.
The optimiser used is SGD with a batch size of 64.</br>

##### Training Plot:














The model trained on the above methods is used to predict the classes of the image which are then stored for further processing.


## 4)Output:
The predicted classes are then preproced as required and the results are then printed on the screen.</br>
The results are also stored onto a CSV file which is available on the output directory.





# SETUP AND RUNNING:
Clone the Repo into your local system:
```
git clone https://github.com/ghost2718/formocr.git
```

To install dependencies run:
```
pip install -r requirements.txt
```
The Download the checkpoints for the RCNN model from [Google Drive](https://drive.google.com/open?id=1E5qdlhBK471Bqp_iwDevIW2O7h4uc6Z1)

Now Move the Jobs.zip file inside the project and then unzip it.
You should have a jobs folder in your main project folder.

Now we have to install Luminoth
```
pip install luminoth
```
We Now have all the dependencies.</br>
To get the ouput run :
```
python3 main.py --impath PATH_TO_IMAGE
```
Here PATH_TO_IMAGE is the path to image file your using as an input
This command will run the project and then print the output onto the screen.</br>

If you wish you can also train the Classifier model again:</br>
To train the model:
```
python3 ./models/train.py --num_epoch NUMBER_oF_EPOCH
```
here NUMBER_OF_EPOCH is the number of epochs you wish to train the model for.

## Additional:
Once the code is run all the ROI and extracted characters are saved in segments directory and this will be cleaned once the code is run again.You can always view the segemented Images from the folder segments</br>
For any problem please email:</br>
[vaishnav160536@mechyd.ac.in](vaishnav160536@mechyd.ac.in)


