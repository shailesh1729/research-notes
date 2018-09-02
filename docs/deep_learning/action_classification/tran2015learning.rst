Learning spatiotemporal features with 3d convolutional networks
===================================================================

In this note, we discuss :cite:`tran2015learning`. 


Summary
--------------

An approach for learning spatiotemporal features
using deep 3D convolutional networks is presented.
The network is trained on large supervised dataset.

.. rubric:: Claims

* 3D convolutional networks are more suitable for spatiotemporal feature learning.
* A homogeneous architecture with :math:`3 \times 3 \times 3` kernels in all layers performs quite well.
* The learned C3D (convolutional 3D) features with a simple linear classifier outperform state of the art methods on many benchmarks.

Further: 

* Features are compact.
* Features are efficient to compute.
* Features are conceptually simple and easy to train.


Prior work
--------------

* Spatio-temporal interest points (STIP)
* SIFT-3D for action recognition
* HOG-3D for action recognition
* Cuboids features for behavior recognition
* Improved Dense Trajectories  (iDT)
* Two stream networks
* Human detector and head tracking
* Deep Video :cite:`karpathy2014large`

.. rubric:: Remarks on prior work

* Image based deep features are not directly suitable for video due to lack of
  motion modeling.
* iDT has good performance but it is computationally intensive and intractable on large scale datasets.


Major results
-----------------------------


.. rubric:: Benchmarks used

* Sports1M for action recognition
* UCF101 for action recognition
* ASLAN for action similarity labeling
* YUPENN for scene classification
* UMD for scene classification
* Object for object recognition






Proposals
-----------------

.. rubric:: Requirements of effective video descriptors:

* **Generic**: Can represent different types of videos well while being discriminative.
* **Compact**: Should be small in size to build databases of millions of videos. Storage
  and retrieval tasks should be scalable.
* **Efficient** to compute: Need to process thousands of videos every minute
* **Simple** to implement: Avoid complicated feature encoding methods and classifiers. 


Examples of different types of videos: Landscapes, Natural scenes,
Sports, TV shows, Movies, Pets, Food



.. rubric:: Proposed 3D convnets

* :math:`3 \times 3 \times 3` convolution kernels for all layers work best.
* Encapsulate information related to objects, scenes and actions in a video.
* No need to fine-tune the model for specific task.
* Model appearance and motion simultaneously.
* Outperform existing results on 4 different tasks and 6 different benchmarks.
* Are compact and efficient to compute.
* No preprocessing on the video. Full video frames as input.
* 3D pooling
* Gradual pooling of space and time information.
* In 3D nets, the input as well as output is an image volume.

.. rubric:: Comparison with 2D ConvNets

* 2D convolutional networks lose temporal information of input signal right after every
  convolution operation.
* Similarly, 3D pooling retains temporal information while 2D pooling loses it.
* 2D convolutional networks when applied on multiple images by treating them as different channels also result in an image only.
* Slow fusion model :cite:`karpathy2014large` uses 3D convolutions and average pooling in first 3 layers. Loses all the
  temporal information after this. The use of 3D convolutions in initial layers is probably the reason for its better 
  performance compared to other models.

.. rubric:: Notation

* :math:`c` : number of channels in image
* :math:`l` : number of frames in video clip
* :math:`h` : height of frame
* :math:`w` : width of frame
* :math:`c \times l \times h \times w` : size of the video clip
* :math:`k` : kernel spatial size
* :math:`d` : kernel temporal depth
* :math:`d \times k \times k` : size of convolutional kernel and pooling kernel


Basic study of 3D convolution and learning
---------------------------------------------

Here our goal is to find out the right parameters for kernel temporal depth.


.. rubric:: Network architecture

* Video frame size : :math:`128 \times 171`.
* Non overlapped 16 frame clips.
* Jittering using random crop for training clips size: :math:`3 \times 16 \times 112 \times 112`.
* 5 convolutional layers, 5 pooling layers.
* 2 FC layers.
* Final softmax layer.
* Number of filters in each layer: 64, 128, 256, 256, 256.
* Kernel temporal depth is variable.
* Appropriate padding is used [both spatially and temporally].
* Stride = 1
* Same convolution used. No change in image volume size in convolution layers.
* First max pooling layer of size :math:`1 \times 2 \times 2`.
* Remaining max pooling layers of size :math:`2 \times 2 \times 2`.
* Clip length changes as follows from layer to layer: :math:`16 \to 16 \to 8 \to 4 \to 2 \to 1`.
* Two 2048 (output size) FC layers 
* Mini batches of 30 clips.
* Initial learning rate 0.003.
* Learning rate divided by 4 after 10 epochs.
* Training stopped after 16 epochs.


.. rubric:: Temporal depth of convolutional kernel

Following options

* Homogeneous temporal depth (same in each layer)
* Varying temporal depth (different in each layer)


Setups

* depth-d homogeneous networks.
* depth-1 network is same as using 2D net on each frame.
* Increasing depth nets: 3-3-5-5-7.
* Decreasing depth nets: 7-5-5-3-3.


.. rubric:: Results

* Clip accuracy is the main metric on UCF 101 dataset.
* Depth 3 network performs best among homogeneous nets.
* Depth 1 (2D net) is significantly worse than others.
* Depth 3 performs better than varying depth networks (gap is not much).
* Increasing depth net performs slightly better than decreasing depth net.


Spatiotemporal feature learning
---------------------------------------


.. rubric:: Network architecture

* Only :math:`3 \times 3 \times 3` nets are used.
* 8 convolution layers, 5 pooling layers, two FC layers and then softmax layer.
* C - P - C - P - C - C - P - C - C - P - C - C - P - FC - FC - SF.


.. rubric:: Training setup

* Sports 1M
* Five random clips each 2 second long from each video
* Frame size to :math:`128 \times 171`.
* Random cropping (both spatial and temporal) to :math:`16 \times 112 \times 112` size.
* Horizontal flipping with 0.5 probability.
* SGD with mini batch of 30 clips.
* Initial learning rate: 0.003.
* Divided by 2 every 150K iterations.
* Optimization stopped after 1.9M iterations (13 epochs).


.. rubric:: Results

* Accuracy of 84.4% at top-5 accuracy.


.. rubric:: C3D video descriptor

* Break video into 16 frame clips with overlap of 8 frames.
* Compute the output activation of final FC layer for each clip.
* Average these activations over all clips.
* L2-Normalize the resultant vector 


.. rubric:: What C3D learns?


* Focuses on appearance in first few frames of a clip.
* Tracks the salient motion in remaining frames.
* Selectively attends to both motion and appearance.




Action recognition
------------------------------




Bibliography
-------------------


.. bibliography:: ../../sksrrcs.bib
