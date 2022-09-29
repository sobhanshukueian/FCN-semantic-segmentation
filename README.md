# FCN Semantic Segmentation
One of the Semantic segmentation algorithms is FCN that uses a Fully Convolutional Network (FCN) i.e. you stack a bunch of convolutional layers in a encoder-decoder fashion. The encoder downsamples the image using strided convolution giving a compressed feature representation of the image, and the decoder upsamples the image using methods like transpose convolution to give the segmented output

[Paper Link](https://arxiv.org/abs/1411.4038)

![image](https://user-images.githubusercontent.com/47561760/192777225-f54acba9-6c46-43a0-967a-2d117659efcb.png)

One major issue with in-network Downsampling in a FCN is that it reduces the resolution of the input by a large factor, thus during upsampling it becomes very difficult to reproduce the finer details even after using sophisticated techniques like Transpose Convolution. As a result we obtain a coarse output (refer the illustration below). One-way to deal with this is by adding ‘skip connections’ in the Upsampling stage from earlier layers and summing the two feature maps. These skip connections provide enough information to later layers to generate accurate segmentation boundaries. This combination of fine and coarse layers leads to local predictions with nearly accurate global (spatial) structure.

![image](https://user-images.githubusercontent.com/47561760/192777292-6c9e2f14-bc2f-4a23-a18a-9c15292a846d.png)

# CamVid Dataset
CamVid (Cambridge-driving Labeled Video Database) is a road/driving scene understanding database which was originally captured as five video sequences with a 960×720 resolution camera mounted on the dashboard of a car. Those sequences were sampled (four of them at 1 fps and one at 15 fps) adding up to 701 frames. You Can Dowload dataset from kaggle:

[Download Dataset from Kaggle](https://www.kaggle.com/datasets/carlolepelaars/camvid)

![image](https://user-images.githubusercontent.com/47561760/192777912-5930383d-8ae8-4df3-8a89-dcfa2c93a03c.png)

## Some Configs for downloading from kaggle :
1. Go to your account, Scroll to API section and Click Expire API Token to remove previous tokens
2. Click on Create New API Token - It will download kaggle.json file on your machine.


# Train
Trainer class Does the main part of code which is training model, plot the training process and save model each n epochs.

I Defined `Adam` Optimizer with learning rate 0.0002.

Does Each training step in `train_step` function and validation step in `val_step` function and whole trining process in 
`train` function.
 
## Some Configurations
 
*   You can set epoch size : `EPOCHS` and batch size : `BATCH_SIZE`.
*   Set `device` that you want to train model on it : `device`(default runs on cuda if it's available)
*   You can set one of three `verboses` that prints info you want => 0 == nothing || 1 == model architecture || 2 == print optimizer || 3 == model parameters size.
*   Each time you train model weights and plot(if `save_plots` == True) will be saved in `save_dir`.
*   You can find a `configs` file in `save_dir` that contains some information about run. 
