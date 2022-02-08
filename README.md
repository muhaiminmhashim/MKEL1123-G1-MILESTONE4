# MKEL1123-G1-MILESTONE4
Milestone 4

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

######################################################################################################

Part 2: Deploy training model into STM32 board

1.  To deploy the pack into STM32 board, open STM32Cube IDE and start a new STM32 project.
2.  A new window will pop out. At the top side, go to "Board Selector" and search for NUCLEO-F446RE Board as that is the board we are using. It depends on what board you are using at this part.
3.  Enter the project name, and choose "C++" as the targeted languang. Then click on "Finish". If there is a window pop out asking whether to "Initialize all peripherals with their default mode" click "Yes". Make sure you have <project_name>.ioc tab open after clicking "Finish" button.
4.  On the .ioc tab, go to "Pinout & Configuration" > "Computing" > "CRC". Click on "CRC" to enable it.

![image](https://user-images.githubusercontent.com/73817919/150868590-1531ede5-6f57-4859-bc0a-c3c7e311e542.png)

5. To upload the pack downloaded before from Edge Impulse, go to "Help" > "Manage Embedded Software Packages" > "From Local...". Then, search for the downloaded pack from your local computer and select it. A window pop out for license agreement will show. Read the "License and Agreement" and click "Yes" if you agree with it. The pack will be installed after you clicking "Yes".

![image](https://user-images.githubusercontent.com/73817919/150869139-fd253a15-e81d-43f6-a457-455b8a01bf87.png)

6.  After have the pack installed. Go back to .ioc tab and  go to "Pinout & Configuration" > "Software packs" > "Select components". Select the pack you previously installed and under selection, click on the checkbox to use the pack. Then go back to .ioc tab, go to "Pinout & Configuration" > "Software Packs". Select the pack you installed, and under "Mode" check the checkbox. 

![image](https://user-images.githubusercontent.com/73817919/150869565-3dc95512-b415-4bb2-b7dd-f013487dc777.png)

![image](https://user-images.githubusercontent.com/73817919/150870005-e280c2ad-d1cb-40d5-9d91-2f70e3a356db.png)

7. Done for the pack installed part. Next we will upload the pack into the board. To do so, we save the configuration we have done on .ioc tab then a window pop out will show to generate the code. Click "Yes". This is the important part, make sure "Middleware" folder is generated because this is where all your impulse and required libraries. Rename the main.c file under Core/Src to main.cpp as C++ languange is preferred.

![image](https://user-images.githubusercontent.com/73817919/150870974-8a0f9575-3109-441f-8ad0-1e1458d09c08.png)

8.  Edit main.cpp file by copy and paste this code from here: https://github.com/muhaiminmhashim/MKEL1123-G1-MILESTONE5/blob/main/Core/Src/main.cpp

9.  Click on the hammer icon on the top side to compile the project. If for errors, fix the error and re-run. Make sure the compile pass, free from errors

![image](https://user-images.githubusercontent.com/73817919/150871987-14fbc06b-b5cb-4921-9c85-8fb0c1a27864.png)

10. To upload the code into board, click on the play button icon. Leave all the setting to default and make sure you already connected your board prior clicking the play button icon. This message will shows if you have successfully uploaded your code into the board.

![image](https://user-images.githubusercontent.com/73817919/150872354-924a43ed-2b39-445a-ba1d-e44d077d7510.png)

11. To display the output, open puTTY. Then choose "Serial" as the connection type. Set the speed to "115200". For the serial line, to know which COMx to use, open "Device Manager" to check. Below is the setting we use.

![image](https://user-images.githubusercontent.com/73817919/150873176-a56c45fa-7e0a-4a01-96da-be0bf7e32d50.png)

12. The result will be shown on puTTy interface as shown below.

![image](https://user-images.githubusercontent.com/73817919/150873951-3463e320-f440-46c8-b696-7d9401ee8f9c.png)

13. To change the dataset, we can copy the raw features of each image. To do so, go back to Edge Impulse, at the left side, choose "Live Classification" and under "Classify existing test sample" choose which image you want to have its raw features. Then click the "Load sample" and wait for classification result comes out. Then, copy the raw features and paste it into this line of code in main.cpp file.

![image](https://user-images.githubusercontent.com/73817919/150874335-8f6f30fa-0f72-4327-afdb-e103e5ffde37.png)

![image](https://user-images.githubusercontent.com/73817919/150874369-a1e7ed0f-f9ba-4974-8e5a-e8646de3030f.png)

######################################################################################################

Reference:
1.  https://docs.edgeimpulse.com/docs/using-cubeai
2.  https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0256630
3.  https://www.hindawi.com/journals/cmmm/2021/8854892/
4.  https://pubmed.ncbi.nlm.nih.gov/34492046/




