# About me...
I'm Pedram. I recently graduated with a Master's degree from Istanbul Technical University. This is my personal webpage, where you can find my education and **[research](#research)** details, as well as my CV, **[publications](#publications)** and **[contact](#contact)** information. I hold a Bachelor's degree in Electronics and a Master's degree in Telecommunications and I am a member of ITU Multimedia Signal Processing and Pattern Recognition (MSPR) research group Lab where I am currently conducting research even after finalizing my masters degree studies. I have experience working in two main research areas. My primary research areas include machine learning, computer vision, and pattern recognition. During my Master's studies, I focused on image and video processing, specifically working with CNN networks to detect and count target objects such as pedestrians, vehicles, or bicycles in input frames. My work involved estimating crowd numbers and distribution patterns through color-coded density maps in both spatial and temporal domains. I published an IEEE paper in this area, and the link to the publication can be found on this webpage. My second area of expertise is networking and telecommunications, specifically the use of machine learning techniques for network quality assessment and management. I detailed my work on 5G network quality of experience (QoE).



# Education
**MSc.** Telecommunications Engineering (ITU)

**BSc.** Electrical and Electronics Engineering (QIAU)


# Skills

Python - C - C++ - Java - MATLAB - OMNeT++ - Proteus - Verilog
          

# Research

- **Deep Learning & Computer Vision:** [Vehicle and pedestrian crowd analysis and density estimation](#road-scene-analysis-using-deep-learning-and-computer-vision)
  - [Single frame crowd counting and estimation (Spatial domain)](#single-frame-crowd-counting-and-estimation-spatial-domain)
  - [CNN Network kernel modifications](#cnn-network-kernel-modifications)
  - [WAYMO cars dataset categorization and adaptation](#waymo-cars-dataset-categorization-and-adaptation)
  - [Video-based road scene analysis (Temporal domain)](#video-based-road-scene-analysis-temporal-domain)
  - [Increasing network performance using transfer learning](#increasing-network-performance-using-transfer-learning)
  - [Estimating and localizing both vehicles and pedestrians (Multi-object)](#estimating-and-localizing-both-vehicles-and-pedestrians-multi-object)
  - [Reducing false-positives and localizing more than 2 objects](#reducing-false-positives-and-localizing-more-than-2-objects-current-research) (Current research)
- **Networks:** [5G network performance and QoE estimation using machine learning](#estimating-video-streaming-qoe-in-the-5g-networks)

## Road scene analysis using deep learning and computer vision

Understanding the location, distribution pattern, and characteristics of crowds, along
with the number of objects within a specific space, constitutes a critical subject known
as crowd analysis. In this process the network passes each input frame through convolutional layers and generates a color-coded map, called as the "Density Map" which is a representation of objects' location whithin each scene. An example of such a map can be seen below. In the case of research done by us, we substuted "People" by "Vehicles" as the target objects, hence adapting this method to the area of vehicle crowd analysis and counting within frames captured from roads and streets. Details of our research can be found in the following sections.

![perf](/assets/perf_example.PNG)

### Single frame crowd counting and estimation (Spatial domain)

My initial experience with CNN-based crowd counting networks relates to a term project I done for the statistical pattern recognition course during my masters’ degree. In that term project I worked with the famous CSRnet deep neural network which was state of the art at the time, after that due to my self interest in that area, I focused on the CANnet, which is a scale-aware neural net, to further familiarize myself with the workings of these networks, I trained multiple models using datasets such as ShanghaiTech, FDST, Venice, JHU-Crowds, UCSD and etc, which all are people crowd counting datasets. Understanding the abilities of CANnet, I implemented the [TRANCOS](https://gram.web.uah.es/data/datasets/trancos/index.html) cars dataset, which provides highway CCTV frames, using this dataset to count and estimate numbers of cars within each scene, reaching to a MAE error rate of 2.82. Image below shows the CANnet architecture, which depicts the VGG-16 layers at the front-end and the convolutional layers at the back-end, and the contextual scale-aware module in the middle. 

![can_arch](/assets/can_detail_1.PNG)

The contextual module is responsible for processing extracted VGG features at different scales and finding the saliency details in each input image. As can be seen in figure below, the feature goes through a process of pooling, upsampling and sigmoid operations.

![can_mods](/assets/can_detail_2.PNG)

The contextual features then are passed to the back-end of the network where the each feature is passed through convolutional layers which at the end a density map whith dots representing center point of each target object is generated. This process is shown in the image below.

![can_convs](/assets/can_detail_3.PNG)


### CNN Network kernel modifications

The MAE error rate showed by CANnet on TRANCOS test set showed that this network is not able to successfully locate and estimate the number of all vehicles present at the images, therefore a modification was applied to the network kernels, specifically kernels with different scales belonging to the contextual module. Image below demonstrates these changes.

![can_kernels](/assets/can_kernels.PNG)

After this modification, CANnet was once again tested on the TRANCOS data, this time however, with the new kernel sizes the network was able to demonstrate impressive MAE error rate of 2.1. Figure below shows the visual network performance after this modification.

![can_tranctest](/assets/can_trantest.PNG)

### WAYMO cars dataset categorization and adaptation

Due to limitations of the TRANCOS dataset such as image resolution and quality, camera point-of-view, limited number of training and test images, and due to the fact that this dataset was not originally developed for the usage in projects with the purpose of autonomous vehicles as the target domain, we turned our focus to the comprehensive [WAYMO](https://waymo.com/open/) cars dataset, which provides video sequences of onboard autonomous vehicle road images, captured using LiDAR equipment and provides 360 degree scene environment. In order to adapt the crowd counting networks to the domain of autonomous vehicles, we implemented the video-based counterpart of the CAnnet, CANnet2s, which is capable of estimating the flow of objects within frame pairs and is able to generate flow maps as well as scene density map and estimate the number of object within a scene. Samples of input frames from WAYMO dataset used by these neural networks are presented in figure below.

![waymo_frames](/assets/waymo_frames.PNG)

For this purpose we went through all the available WAYMO segments, and extracted "Front camera" frames. Totalling more thatn 140 segments and 28000 frames. One-third of this number of frames were used for the training and the remaining were used for testing of both CANnet and CANnet2s. Furthermore, to better understand the content of the WAYMO images and to better evaluate the performance of networks under various scenes we labeled each segment of the dataset in 7 different general categories, as "Bright", "Dark", "Occlusion", "Pose change", "Low density", "Blurry", and "Multi-scale". Examples of labled WAYMO input frames can be seen below.

![waymo_cat](/assets/waymo_cat.PNG)

### Video-based road scene analysis (Temporal domain)

The video-sequence-based counterpart of the CANnet is called the CANnet2s is used for the purpose of training a model for road scene analysis and density estimation using the WAYMO frames. This network has an architecture very similar to that of the CANnet, however, instead of processing single images, this network inputs a frame pair, and the network passes each frame to one of its two parallel covolutional layers, as can be seen in the figure below. It is evident that the network process each frame, and passes the extracted contextual features to the back-end; however, on contrast to the CANnet, this network generates intermediatory grid-based density maps and by detecting differences in objects' locations whithin frames, the network estimates the object flows, hence generating 10 different flow maps in each corresponding directions and by averaging all the flows, the network reaches to a single estimated density map, similar to those seen in the output of networks such as CSRnet or CANnet.

![can2_arch](/assets/can2_arch.PNG)

Supriority of CANnet2s compared to CANnet can be seen both in training and testing phases. Graph presented below shows the Epoch Vs Loss details for both networks, as it can be seen in this graph, CANnet2s converges faster thatn CANnet, requiring less training time compared to its image-based counterpart (CANnet) while showing better performance. 


To better compare the two networks' performance when tested on WAYMO test set, three different evaluation metrics, MAE, RMSE and PSNR are considered. Tables below show networks' evaluation comparison. First table shows total network performance, however, the second table shows attribute-based performance of each network corresponding to various scene categories.

|    Network   |   MAE  | RMSE  | PSNR    |
|:------------:|:------:|:-----:|:-------:|
| CANnet2s     | 5.46   | 6.13  | 32.4 dB |
| CANnet       | 7.74   | 8.45  | 29.5 dB |

![cans_tab](/assets/cans_tab.PNG)


### Increasing network performance using transfer learning

### Estimating and localizing both vehicles and pedestrians (Multi-object)

### Reducing false-positives and localizing more than 2 objects (CURRENT RESEARCH)

## Estimating Video Streaming QoE in the 5G networks\*

Estimating and evaluating the performance of the network for a mobile video streaming use case using 5G network’s analytics functionality implemented with OMNeT++ in combination with INET and SimuLTE frameworks. Analysis of the 5G NWDAF gathered network performance data such as Uplink and Downlink traffic, number of transmitted and retransmitted packets, and radio quality conditions per user equipment using machine learning techniques such as F-test, MIR and PCA. At the first phase, a network is defined and implemented in OMNeT++ and SimuLTE is used to generate user plane traffic in this mobile network. This network consists of a single access node (AN) connected to the gateway (PWG). The access node is connected to a video server which provides a video with the length of 300 seconds, split into segments of 5 seconds duration with three different quality levels having bitrates of 500 Kbps, 1500 Kbps, and 3000 Kbps, corresponding to 560p (SD), 720p (HD) and 1080p (FULL HD) video qualities, respectively. 

In this simulation number of active video clients (UEs) increases from initial number of 20 UEs to 200 UEs, randomly placed around the access node. Each UE initially receives the SD video quality, with a buffer length of 30 seconds, each user is able to reach to the highest possible video streaming quality within a very short time, however, as the number of UEs increases, the required time for each UE to be able to switch to a higher streaming quality increase, also increase in number of UEs, decreases the received video bitrate.  Figures below show the schematic of the network implemented in OMNeT++ and a graph showing the comparison between received video bitrate for a network with 40 UEs compared to a another one with 200 UEs.

![network](/assets/network1.PNG)

![graphs](/assets/network2.PNG)


\* *This is an implementation of the network proposed in the paper by Schwarzmann, S., Cassales Marquezan, C.,
Bosk, M., Liu, H., Trivisonno, R., & Zinner, T titled “Estimating Video Streaming QoE in the 5G
Architecture Using Machine Learning". This implementation was presented as a term project for the Network planning and
management course during my masters degree. Network presented in the figure and the results are mine and are different from results presented in the original paper.*




# Publications

* Yousefi, Pedram. **"Crowd Localization and Counting via Deep Flow Maps."** *M.S. thesis, Istanbul Technical University, July 2024*.

* Yousefi, Pedram, Bilge Gunsel, and Yusuf Kagan Hanoglu. **"Vehicle Crowd Density Estimation Enhanced by Video Flow Maps."** In *2023 14th International Conference on Electrical and Electronics Engineering (ELECO)*, 1–5. IEEE, 2023. [official link](http://www.eleco.org.tr/ELECO2023/eleco2023-papers/103.pdf)


# Test Score
Here you can see my TOEL iBT test score. 

Test Date: November 22nd, 2023

![Score](/assets/toefl_score.PNG)


# Contact

**Academic Email:** yousefi21@itu.edu.tr

**Personal Email:** pedramyousefi39@gmail.com

**[Linkedin](linkedin.com/in/pedram-yousefi-9b2139197/)**
