Learning spatiotemporal features with 3d convolutional networks
===================================================================

:paper: 

See :cite:`tran2015learning`. 

Ideas
-----------------

.. rubric:: Requirements of effective video descriptors:

* **Generic**: Can represent different types of videos well while being discriminative.
* **Compact**: Should be small in size to build databases of millions of videos. Storage
  and retrieval tasks should be scalable.
* **Efficient** to compute: Need to process thousands of videos every minute
* **Simple** to implement: Avoid complicated feature encoding methods and classifiers. 


Examples of different types of videos: Landscapes, Natural scenes,
Sports, TV shows, Movies, Pets, Food


.. rubric:: Prior work

* Spatio-temporal interest points (STIP)
* SIFT-3D for action recognition
* HOG-3D for action recognition
* Cuboids features for behavior recognition
* Improved Dense Trajectories  (iDT)


.. rubric:: Remarks on prior work

* Image based deep features are not directly suitable for video due to lack of
  motion modeling.
* iDT has good performance but it is computationally intensive and intractable on large scale datasets.


.. rubric:: 3D ConvNets

* :math:`3 \times 3 \times 3` convolution kernels for all layers work best.
* Encapsulate information related to objects, scenes and actions in a video.
* No need to fine-tune the model for specific task.
* Model appearance and motion simultaneously.
* Outperform existing results on 4 different tasks and 6 different benchmarks.
* Are compact and efficient to compute.


Results
-----------------------------


.. rubric:: Benchmarks used

* Sports1M for action recognition
* UCF101 for action recognition
* ASLAN for action similarity labeling
* YUPENN for scene classification
* UMD for scene classification
* Object for object recognition



.. bibliography:: ../../sksrrcs.bib
