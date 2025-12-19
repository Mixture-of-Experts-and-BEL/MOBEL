# EmoCRNet: Cross-Modal Emotion Analysis: Leveraging Audio and Video Fusion with CRNN

# INTRODUCTION
  Emotion recognition from Multimodal input, particularly in speech and facial expressions has garnered significant interest in the recent times. Emotional recognition is complex because human emotions are expressed across various modalities. To Tackle these challenges we have introduced an innovative approach through a fusion model combining deep learning features of audio and video emotions using a convolutional recurrent neutral network. This model adresses the spatial-temporal correlation between Audio and Video and aims to recognize the pattern between the same. The RAVDESS dataset has been used to train the models. The model detects 6 basic emotion with an accuracy of 92.851% and tries to detect other emotions like frustration, sarcasm etc.

# METHODOLOGY
  The proposed model works as follow:
  ![EmoCRNet](https://github.com/user-attachments/assets/b618251e-2aaf-426c-9447-a2528c145756) 
  Initially, the audio and video streams are extracted from the input file.

# AUDIO Preprocessing
  The extracted audio signal after noise removal and other tuning process is converted into small segments of duration 1000ms and 500ms overlapping. These segments are converted into Normalized and scaled Mel-spectograms and passed to a CRNN for feature extraction. 96 Mel-filter banks were adopted with a frequency range of 20 to 8000 Hz and a context window of 32 frames for a audio file. The features extracted are stored in csv file along with other features from the video stream.

# VIDEO Preprocessing
  The visual stream consists only of the video without any audio. 12 keyframes are generated from a video file based on a specific frame rate with an interval of 8ms. After extracting keyframes, each video had 12 key images. These images were then passed into a SSD generator, a pre-trained model trained on the CAFFEE dataset. The output of the SSD model is a coordinate of face bounding boxes. Using these bounding boxes, RGB key images are cropped to knock off the background, focus on the face, and resize each image to a fixed size.
    
# FEATURE EXTRACTION and FUSION
  The generated  SSD frames for each visual stream are fed into a separate CRNN network for training, which directly learns the spatial-temporal features from the video. The model learns the spatial-temporal features from the visual data, and 256 features are extracted from the feature-level fusion. Then, the generated Mel-spectrogram is passed into another CRNN model for audio as an image of size. The CRNN consists of a 3D-CNN and LSTM network. The CNN architecture is the same as visual stream emotion recognition. In the LSTM part, there are layers with 256 cells. The last FC layer, 256, is extracted as a speech emotion representation. Then audio and video features are combined and given to BEL network model to train spatial-temporal information of different modalities jointly. The output of the softmax layer is passed to the feature fusion model.10-fold cross-validation was implemented to improve test accuracy.The features extracted from the Softmax layer of Audio and Visual networks  are fused to get 12 features for a single input file. These features are probabilities of the input file belonging to a particular emotion class out of the 6 classes. These are passed into the BEL (Brain Emotional Learning) model, which is a mixture of expert architectures.RESNET was used to generate SSD results and the extracted features were averaged .The BEL model consists of two components: how the brain’s amygdala (AMG) and orbitofrontal cortex (OFC) interact to learn and adapt. The BEL model’s parameters are trained using a Gradient descent algorithm, which provides supervised training. In feature-level fusion, features are extracted from the fully connected layer of the audio network (256D) and visual network (256D). The features are fused to get 512 high-level features, which are passed to the network. The architecture consists of BEL experts and one BEL gating network. 

# RESULT
The model analyses the result  to further recognize complex cognitive emotions like Depresssion,Frustration,Anxiety etc.

<img width="504" height="259" alt="image" src="https://github.com/user-attachments/assets/65a542d6-7f5c-4782-9c70-76010008961c" />

  

  
  
  

  

 


