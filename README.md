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
  - [Network kernel modifications](#network-kernel-modifications)
  - [WAYMO cars dataset categorization and adaptation](#waymo-cars-dataset-categorization-and-adaptation)
  - [Video-based road scene analysis (Temporal domain)](#video-based-road-scene-analysis-temporal-domain)
  - [Increasing network performance using transfer learning](#increasing-network-performance-using-transfer-learning)
  - [Estimating and localizing both vehicles and pedestrians (Multi-object)](#estimating-and-localizing-both-vehicles-and-pedestrians-multi-object)
  - [Reducing false-positives and localizing more than 2 objects](#reducing-false-positives-and-localizing-more-than-2-objects-current-research) (Current research)
- **Networks:** [5G network performance and QoE estimation using machine learning](#estimating-video-streaming-qoe-in-the-5g-networks1)

## Road scene analysis using deep learning and computer vision

Understanding the location, distribution pattern, and characteristics of crowds, along
with the number of objects within a specific space, constitutes a critical subject known
as crowd analysis. In the case of research done by us, we substuted "People" by "Vehicles" as the target objects, hence adapting this method to the area of vehicle crowd analysis and counting in frames captured from roads and streets. Details of our research can be found in the following sections.

### Single frame crowd counting and estimation (Spatial domain)

### Network kernel modifications

### WAYMO cars dataset categorization and adaptation

### Video-based road scene analysis (Temporal domain)

### Increasing network performance using transfer learning

### Estimating and localizing both vehicles and pedestrians (Multi-object)

### Reducing false-positives and localizing more than 2 objects (CURRENT RESEARCH)

## Estimating Video Streaming QoE in the 5G networks[1]

Estimating and evaluating the performance of the network for a mobile video streaming use case using 5G network’s analytics functionality implemented with OMNeT++ in combination with INET and SimuLTE frameworks. Analysis of the 5G NWDAF gathered network performance data such as Uplink and Downlink traffic, number of transmitted and retransmitted packets, and radio quality conditions per user equipment using machine learning techniques such as F-test, MIR and PCA. At the first phase, a network is defined and implemented in OMNeT++ and SimuLTE is used to generate user plane traffic in this mobile network. This network consists of a single access node (AN) connected to the gateway (PWG). The access node is connected to a video server which provides a video with the length of 300 seconds, split into segments of 5 seconds duration with three different quality levels having bitrates of 500 Kbps, 1500 Kbps, and 3000 Kbps, corresponding to 560p (SD), 720p (HD) and 1080p (FULL HD) video qualities, respectively. 

In this simulation number of active video clients (UEs) increases from initial number of 20 UEs to 200 UEs, randomly placed around the access node. Each UE initially receives the SD video quality, with a buffer length of 30 seconds, each user is able to reach to the highest possible video streaming quality within a very short time, however, as the number of UEs increases, the required time for each UE to be able to switch to a higher streaming quality increase, also increase in number of UEs, decreases the received video bitrate.  Figures below show the schematic of the network implemented in OMNeT++ and a graph showing the comparison between received video bitrate for a network with 40 UEs compared to a another one with 200 UEs.

![network](/assets/network1.PNG)

![graphs](/assets/network2.PNG)


[1] *This is an implementation of the network proposed in the paper by Schwarzmann, S., Cassales Marquezan, C.,
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
