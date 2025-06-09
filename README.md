
# Medicine Strip Information Extraction

This repository provides an end-to-end pipeline to extract key information from medicine strip images, including the medicine name, manufacturing date (MFG), expiry date, and number of tablets. It uses a combination of YOLOv11 for object detection, EasyOCR for text recognition, and Gemini (LLM) for post-processing and result refinement.

## Repository Structure

```
MedicineStrip_information/
├── Medicine_Strip_content/               # Input data: test images and OCR result samples
│   ├── images_required.jpg
│   └── best.pt                           #saved YOLO model after training
│
├── Paddleocr_change_comparison/         # Visual comparison: PaddleOCR output snapshots
│   └── paddleocr_fail_case_comparison.jpg
│
├── previous_notebook_medicineStrip/     # Previous trials using different OCR engines
│   └── paddleocr_previous_tests.ipynb
│
├── Medicine_strip_easyocr.ipynb         # Main notebook: YOLOv11 + EasyOCR + Gemini pipeline
└── README.md                            # Project documentation
```

## Objective

The objective of this project is to automatically extract the following fields from medicine strip images:

* Medicine Name
* Manufacturing Date (MFG Date)
* Expiry Date
* Number of Tablets

## Pipeline Overview

1. **YOLOv11**: Detects regions of interest (text areas) in the medicine strip image.
2. **EasyOCR**: Extracts text from the detected regions.
3. **Gemini** (LLM): Refines and interprets the extracted text to identify structured information such as dates, tablet counts, and medicine names, even if noisy or partially missing.

## Notebooks Description

### `Medicine_strip_easyocr.ipynb`

* Implements the complete pipeline using YOLOv11 for detection, EasyOCR for recognition, and Gemini for refinement.
* Accepts user-provided images via the `Medicine_Strip_content/` directory.
* Outputs cleaned information such as MFG, EXP, and tablet count.

### `previous_notebook_medicineStrip/paddleocr_previous_tests.ipynb`

* Explores multiple OCR engines including PaddleOCR, EasyOCR, and others.
* Documents the accuracy and failures experienced with newer PaddleOCR versions.

## Observations and Comparison

* Earlier versions of **PaddleOCR** (up to 16.05) showed accurate results in extracting medicine strip content.
* Post-update versions of PaddleOCR demonstrated noticeable degradation in recognition quality, as shown in `Paddleocr_change_comparison/paddleocr_fail_case_comparison.jpg`.
* **EasyOCR**, when used with YOLOv11 for preprocessing, provided improved and consistent results, especially for mixed fonts and unclear layouts.

## Requirements

Install dependencies using pip:

```bash
pip install easyocr
pip install paddleocr
pip install ultralytics
```

Additional dependencies may include OpenCV, NumPy, and transformers if using Gemini or LLM-based post-processing.

## Usage Instructions

1. Clone or download the repository.
2. Upload your test image(s) into the `Medicine_Strip_content/` directory.
3. Open and execute `Medicine_strip_easyocr.ipynb` in Google Colab or a local Jupyter environment.
4. The notebook will output:

   * Cropped image segments
   * OCR text results
   * Cleaned structured information (Medicine name, MFG, EXP, tablet count)

## Contributor

Abir Mozito – Research, development, and experimentation with OCR and object detection methods.

## References

* EasyOCR: [https://github.com/JaidedAI/EasyOCR](https://github.com/JaidedAI/EasyOCR)
* PaddleOCR: [https://github.com/PaddlePaddle/PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR)
* Ultralytics YOLO: [https://github.com/ultralytics/ultralytics](https://github.com/ultralytics/ultralytics)

