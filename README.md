# MKEL1123-G1-MILESTONE5
Milestone 5

Groups Member

1.  Muhaimin bin Mohd Hashim (MKE211014)
2.  Muhammad Salehuddin bin Bakarudin (MKE211021)
3.  Ooi Tze Kian (MKE191085)

Before proceeding with the steps, here are some prerequisite needed:
1.  Edge Impulse Account (https://www.edgeimpulse.com) - Do sign up for free so can use their API for our image recognition training.
2.  STM32CubeIDE (https://www.st.com/en/development-tools/stm32cubeide.html) - Do download the IDE from here and install to our local computer. Use to deploy our trained model and coding into STM32Board
3.  puTTY (https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) - This is to display our output
4.  Image pack (https://www.kaggle.com/paultimothymooney/chest-xray-pneumonia) - This is for our image training input

Steps for image recognition can be divided into 2 parts:

1.  Image recognition training from Edge Impulse
2.  Deploy training model into STM32 board

Part 1: Image recognition training from Edge Impulse

1.  Download the image dataset from the given link above.
2.  Go to Edge Impulse, and on "Dashboard" choose "LETS'S COLLECT SOME DATA". THen Choose "Upload data" and "Go to the uploader"

![image](https://user-images.githubusercontent.com/73817919/150857197-fc26eb52-ebfc-4a69-a09c-f63d96e8d5af.png)

3.  Keep "Upload into category" into default and for the label part, make sure using 2 set of label which are "Normal" and "Pneumonia". Then upload the image you downloaded before. Ensure the image upload are according to their label respectively. Normal for Normal Lung Image, and Pneumonia for Pneumonia Lung Image.

![image](https://user-images.githubusercontent.com/73817919/150857924-9b8a828b-bde2-40e0-85d1-468d419699eb.png)

4. After the upload image process is done, we need to create impulse for the image training. Impulse here mean, it will process the image, to extract the feature for the image training later. Create the impulse setting according the image below. Then save the impulse setting

![image](https://user-images.githubusercontent.com/73817919/150861172-a6d434ab-cd14-4852-a205-3fe277ecf83a.png)

5.  Go to "Image" on the right side. Choose the setting according to image below. Choose "Grayscale" as the parameters as our image mostly composed of black and white image. This give us more accurate data set compare to "RGB" parameters. Then save the parameters. After that, click on the "Generate features" and wait until the process done.

![image](https://user-images.githubusercontent.com/73817919/150862004-49198875-c1f9-4d6c-aa9d-d527c75ce8f9.png)

![image](https://user-images.githubusercontent.com/73817919/150862620-39f988de-c259-4502-ab0c-3eb37bf11aa7.png)

6.  After the process is done, go to "NN Classifier" to train our model using Edge Impulse API. Set the number of training cycles to 100, Learning rate to 0.0005 and Validation set size to 20. Then start the training process. After the training process is done, do take a look at the accurancy of the training process. If satisfied go to "Model testing" at the right side. Notes: If the validation accurancy is lower than expected, can retrain the model by clicking "Retrain model" on the right side.

![image](https://user-images.githubusercontent.com/73817919/150865540-a07f4012-5ce2-4ed8-ab62-1bb660e30eea.png)

![image](https://user-images.githubusercontent.com/73817919/150865703-6ec06866-7d74-4b6f-a24b-b93f5ba9a5ef.png)


7. At the "Model testing" windows, click "Classify all" to do some preliminary validation and testing on the image training to see whether the data extracted from the training process can be used to classify the image upload before acccording to their label respectively. 

![image](https://user-images.githubusercontent.com/73817919/150866224-cece3de8-f79c-4319-a97a-0ac313381bc3.png)

8. To deploy the data to be upload into STM32 board, go to "Deployement" on the left side and choose "Cube.MX CMSIS-PACK" and make sure "Enable EON™ Compiler" is enabled. Select "Quantized (int8) and click "Build". Later the pack that will be used to upload the data into the STM32 board will be automatically downloaded.

![image](https://user-images.githubusercontent.com/73817919/150866994-970007c2-95a9-43d6-b982-58507dcc4f63.png)

![image](https://user-images.githubusercontent.com/73817919/150867025-93575ed9-2462-4394-ac29-024a7bd5bc29.png)

