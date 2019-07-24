# Pattern-Recognition
This file contains the project of pattern recognition

Code:	the codes  for the training and testing. The patern_recognition.ipynb contains all the code
	and is generated using Google Colab. It can also be opened in jypiter notebook. Python 3.

dataset: contains the patches used for the training. The folders are divided in IMG14 and IMG32 and
	 inside of each are the different representations (local depth, normal azimuth and normal elevation)
	and all of them merged together in the "all" folder. Each of them is divided in 3 folders :train, test, val
	and these ones are also grouped in 3 subfolders : edge, non_texture and texture. 
	That depends on the label of the patch. 

Doc: The papers readed for this project and some useful links.

mesh grid generation: This folder contains mesh models, the related descriptors and the code to generate the patches

models: contains the trained models which have the best accuracy on validation. Used for the testing.
	_model_azimuth_32_13.pt : azimuth : the representation
				  32 : the dimension of the patch
				  13 : the number of the epoch 

train_test_results: contains the results of the testing. Each folder has the results depending on 
			the dimension of the patch and the representation. 
			Each file consists of 2 parts:
			  - The first are the results of the training and validation of each epoch.
			   In the end there is the best accuracy of the validation and the model is saved for the testing.
			  - The second are the results of the testing. In the end is the average testing result
 
