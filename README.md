# License Plate Extraction with YOLOv10 and PaddleOCR & Save Data to SQL Database


* Data
  
Get dummy data from roboflow

What is the use of Roboflow?

Roboflow empowers developers to build their own computer vision applications, no matter their skillset or experience. We streamline the process between labeling your data and training your model. After building our own applications, we learned firsthand how tedious it can be to train and deploy a computer vision model.

Link for dataset:-https://roboflow.com/universe

<a href="URL_REDIRECT" target="blank"><img align="center" src="https://github.com/khamkaradinath/Numberplate_detection_using_YOLOv10_and_PaddleOCR/blob/main/image_for_readme/Screenshot%202024-11-26%20114434.png" height="300" /></a>

* Model selection
  #### YOLOv10: Real-Time End-to-End Object Detection
  Comparisons with others in terms of latency-accuracy (left) and size-accuracy (right) trade-offs.
  
  <table>
  <tr>
    <td><img src="https://github.com/khamkaradinath/Numberplate_detection_using_YOLOv10_and_PaddleOCR/blob/main/image_for_readme/latency.svg" alt="Detection 1" width="400"></td>
    <td><img src="https://github.com/khamkaradinath/Numberplate_detection_using_YOLOv10_and_PaddleOCR/blob/main/image_for_readme/params.svg" alt="Detection 2" width="400"></td>
  </tr>
</table>

## How It Works
#### 1.YOLOv10 Model
* YOLOv10 (You Only Look Once) is used for detecting license plates in each video frame.
* It provides
    * Bounding box coordinates for detected plates.
    * Confidence scores for the detections.

<h3>Precison,recall and f1-score</h3>

<table>
  <tr>
    <td><img src="https://github.com/khamkaradinath/Numberplate_detection_using_YOLOv10_and_PaddleOCR/blob/main/image_for_readme/download%20(9).png" alt="Detection 1" width="300"></td>
    <td><img src="https://github.com/khamkaradinath/Numberplate_detection_using_YOLOv10_and_PaddleOCR/blob/main/image_for_readme/download%20(10).png" alt="Detection 2" width="300"></td>
  </tr>
  <tr>
    <td><img src="https://github.com/khamkaradinath/Numberplate_detection_using_YOLOv10_and_PaddleOCR/blob/main/image_for_readme/download%20(11).png" alt="Detection 3" width="300"></td>
    <td><img src="https://github.com/khamkaradinath/Numberplate_detection_using_YOLOv10_and_PaddleOCR/blob/main/image_for_readme/f1.png" alt="Detection 4" width="300"></td>
  </tr>
</table>

<h3>confugion Matrix</h3>
  <table>
  <tr>
    <td><img src="https://github.com/khamkaradinath/Numberplate_detection_using_YOLOv10_and_PaddleOCR/blob/main/image_for_readme/confusion_matrix.png" width="400"></td>
  </tr>
</table>

<h3>Here it is How Yolov10 detected numberplates</h3>
  <table>
  <tr>
    <td><img src="https://github.com/khamkaradinath/Numberplate_detection_using_YOLOv10_and_PaddleOCR/blob/main/image_for_readme/numbeplatebox.jpeg" width="500"></td>
  </tr>
</table>

## 2.PaddleOCR

Leveraging deep learning techniques, including CNNs and recurrent neural networks, Paddle OCR excels in accurate text recognition. It comprises two key components: the detector and the extractor. The detector is tasked with pinpointing text within an image or document.

* PaddleOCR takes the bounding box regions as input to extract the text on license plates
* Handles low-quality images and rotated text.
* Confidence filtering ensures only high-confidence text is stored.

  
<h3>workflow image for paddleOCR</h3>
  <table>
  <tr>
    <td><img src="https://github.com/khamkaradinath/Numberplate_detection_using_YOLOv10_and_PaddleOCR/blob/main/image_for_readme/ocr_image.webp" width="500"></td>
  </tr>
</table>
Documentation for PaddleOCR: [PaddleOCR Documentation](https://blog.roboflow.com/what-is-optical-character-recognition-ocr/#:~:text=Leveraging%20deep%20learning%20techniques%2C%20including,within%20an%20image%20or%20document.).

## 3. Data Storage

* JSON: Outputs license plate numbers for each 20-second interval
* example
  ```json
  {
  "Start Time": "2024-11-25T10:00:00",
  "End Time": "2024-11-25T10:00:20",
  "License Plate": ["MH12AB1234", "DL5C6789"]
   }

 * SQLite: A database table (LicensePlates) stores
     * Start and end times.
     * Detected license plate text.
  
 
## 3.Customization
You can modify the following in the main.py or Notebook:
* Detection Interval: Change the 20-second interval for saving outputs.
* Model Weights: Replace weights/best.pt with a custom YOLOv10 weight file
* Confidence Thresholds: Adjust the detection confidence (default: 0.45).

## 4.Limitations
 * Environmental Factors: Performance may degrade under poor lighting or weather conditions.
 * Regional Variations: The model might need fine-tuning for region-specific license plates.
 
## 5. Future Enhancements
  * Integrate more advanced OCR techniques for improved accuracy.
  * Add support for real-time video streaming.
  * Provide multi-language OCR capabilities.
    
  






  
