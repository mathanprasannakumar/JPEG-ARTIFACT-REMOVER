# JPEG-ARTIFACT-REMOVER


<h5>JPEG artifact remover using GAN architecture</h5>


Model is trained based on NoGan approach , initally both generator and discriminator is trained separately.After that , Normal Gan method is followed for both generator and discriminator.

<h4><b>Model Architecture</b></h4>

In this work, i followed the approach proposed in this paper ,

<b>A NoGAN approach for image and video
restoration and compression artifact removal</b>

<a href = "https://dl.acm.org/doi/10.1145/3394171.3414451">link</a>

I did lot of modifications as per my requirement, the intuition behind patchbased training,NoGan method is taken from the paper.

<ul>
  <li>Generator model will have double Residual in Residual Dense Block (RRDB) followed convolution layers</li>
  <li> Discriptor model will have 6 Convolution layer having leaky Relu as an activation function</li>
</ul>

<h4><b>Data Preparation</b></h4>

<ul>
  <h5><b>Generator Training</b></h5>
  <li>900 images is take from the <a href= "https://www.kaggle.com/datasets/joe1995/div2k-dataset">Div2k</a>dataset</li>
  <li> train_data = 700 , test_data = 100 , val_data = 100 </li>
  <li> Initially patches or cropping is done on the images by using albumentations library</li>
  <li> JPEG compression is done with a Quality Factor = 10 </li>

  <h5><b>Discriminator Training</b></h5>
  <li>Two input image is being passed, real high resolution image and reconstructed image from jpeg.</li>
  <li>train_data = 300 , test_data = 50 , val_data = 50</li>

  <h5><b>Gan Traning</b></h5>
  <li>Same data used for the generator is used</li>
  <li>Model was able to produce 0.67 SSIM and 24 PSNR on the test dataset and able to generalize well across all the images</li>
</ul>

Here as of resource constraints,  batchsize = 1.


<h4><b>Losses</b></h4>
<ul>
  <li>Intially for the generator, there will be two losses, pixel loss (mse) and perceptual loss(VGG feature mse)</li>
  <li>For the Discriptor, Binary cross entropy is used</li>
  <li>During GanTraining, for generator ,in addition to above losses binary cross entroy is added as generator want the fake to be classified as real.
</ul>

