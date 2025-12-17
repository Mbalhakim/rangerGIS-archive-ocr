# RangerGIS-Archive

**AI-Powered Document Linking System for Staatsbosbeheer**

Automated tool to link historical archival documents with location and species data, making 125 years of forestry information accessible to forest rangers.

---

## Project Overview

### Problem Statement
Staatsbosbeheer (Dutch Forestry Commission) has thousands of scanned paper documents stored in SharePoint. These documents reference locations (PlaatsCodes) and species that are also registered in the Adlib database, but there's no automated way to link them together.

### Solution
An AI-powered tool that:
- Extracts text from scanned PDFs using OCR (Optical Character Recognition)
- Detects location codes and species names
- Matches extracted data with Adlib database records using fuzzy matching
- Provides confidence scores for automatic linking

---

## Features

**OCR Pipeline** - Extracts text from handwritten and printed documents  
**Document Segmentation** - Identifies paragraphs, lines, and words  
**Fuzzy Matching** - Handles OCR errors and variations in text  
**PDF Processing** - Batch processes multi-page documents  
**Smart Filtering** - Saves only pages with matches  
**Visualization** - Displays similarity scores and results  
**CRNN Model Training** - Deep learning for handwritten text recognition  

---

## Project Structure

```
RangerGIS-Archive/
├── notebooks/                          # Jupyter notebooks
│   ├── Updated_OCR_with_Segmentation.ipynb  # Main working pipeline 
│   ├── CRNN_training.ipynb            # Deep learning model training
│   ├── OCR-Train-With-VOC.ipynb       # Object detection training
│   └── experimental/                   # Experimental notebooks
│       ├── opencv.ipynb
│       ├── PIL_with_OCR.ipynb
│       ├── image_with_boxes.ipynb
│       ├── test.ipynb
│       └── OCR_with_Segmentation.ipynb
│
├── scripts/                            # Python scripts
│   ├── main.py                        # PDF text extraction
│   ├── main2.py                       # Tesseract OCR implementation
│   ├── main3.py                       # EasyOCR implementation
│   └── train.py                       # Model training utilities
│
├── dataset/                            # Training and reference data
│   ├── annotations.csv                # Labeled bounding boxes (28 images)
│   ├── labels.txt                     # Location code labels
│   ├── PlaatsCodes.json              # 2,075 location records
│   ├── ObjectenLijst.json            # 7,202 object records
│   ├── ImageTrainVoc/                 # VOC format training data
│   ├── ImgTrainCrop/                  # Cropped training images
│   └── PlaatsCodes/                   # Sample images by location
│
├── data/                               # Input data
│   └── raw/mix/                       # Raw PDF files (27 files)
│
├── outputs/                            # Generated outputs
│   ├── temp/                          # Temporary processing files
│   └── matched_pages/                 # Pages with successful matches
│
├── docs/                               # Documentation
├── extracted_text.txt                 # Sample OCR output
├── README.md                          # This file
├── requirements.txt                   # Python dependencies
└── .gitignore                         # Git ignore rules
```

---

## Getting Started

### Prerequisites
- Python 3.8+
- Tesseract OCR installed ([Installation Guide](https://github.com/tesseract-ocr/tesseract))
- 4GB+ RAM recommended

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
  
   ```

2. **Install Python dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Configure Tesseract path** (Windows)
   ```python
   pytesseract.pytesseract.tesseract_cmd = r'C:\Program Files\Tesseract-OCR\tesseract.exe'
   ```

### Quick Start

**Option 1: Run the main pipeline (Jupyter Notebook)**
```bash
jupyter notebook notebooks/Updated_OCR_with_Segmentation.ipynb
```

**Option 2: Run scripts directly**
```bash
python scripts/main3.py  # EasyOCR implementation
```

---

## Usage

### Processing a PDF Document

1. Place your PDF in the `data/raw/mix/` folder
2. Open `notebooks/Updated_OCR_with_Segmentation.ipynb`
3. Update the PDF path in the last cell:
   ```python
   pdf_path = 'data/raw/mix/your_document.pdf'
   ```
4. Run all cells
5. Check results in `outputs/matched_pages/`

### Training the CRNN Model

1. Open `notebooks/CRNN_training.ipynb`
2. Ensure training data is in `dataset/ImgTrainCrop/`
3. Run training cells
4. Model will be saved for inference

---

## Dataset

### Location Codes (PlaatsCodes)
Currently trained on 13 location codes:
- `AAGOALGC781`, `DWINAL`, `GUISFLO`, `Imblo`, `pemaflo`
- `SMBBFLO`, `Tersavi`, `Tersego`, `TERSHYD`

### Training Data
- **28 annotated images** with bounding boxes
- **2,075 location records** from Adlib
- **7,202 object records** with metadata

---

## Technical Details

### OCR Engines Used
1. **Tesseract OCR** - Fast, works well with printed text
2. **EasyOCR** - Better for handwritten text
3. **CRNN (in development)** - Custom deep learning model

### Matching Algorithm
- **Fuzzy Matching** using RapidFuzz
- Default threshold: 75% similarity
- Handles OCR errors and variations

### Current Accuracy
- Location code detection: ~75-85% (fuzzy matching)
- Handwriting recognition: In development (CRNN)

---

## Project Status

| Phase | Status | Description |
|-------|--------|-------------|
| 1. Needs Analysis | Complete | Requirements gathered |
| 2. Technical Planning | Complete | Architecture defined |
| 3. Data Collection | Complete | Training data prepared |
| 4. POC Development | Complete | Working pipeline built |
| 5. Evaluation | In Progress | Testing with real documents |
| 6. Model Training | In Progress | CRNN training underway |
| 7. Integration | Pending | SharePoint/Adlib integration |

---

## Next Steps

1. Complete project cleanup and organization
2. Finish CRNN model training
3. Evaluate accuracy on test dataset
4. Expand to species name recognition
5. Build feedback loop with archive manager (Finn)
6. Integrate with SharePoint and Adlib APIs

---

## Key Dependencies

- `opencv-python` - Image processing
- `pytesseract` - OCR engine wrapper
- `easyocr` - Deep learning OCR
- `tensorflow` - CRNN model training
- `rapidfuzz` - Fuzzy string matching
- `pdf2image` - PDF to image conversion
- `pandas` - Data manipulation
- `matplotlib` - Visualization

See `requirements.txt` for full list.

---

## Team & Contact

**Project**: Staatsbosbeheer Archive Digitization  
**Client**: Finn van der Ent (Archive Manager)  
**Duration**: 6 weeks  

---

## License

[Add appropriate license]

---

## Acknowledgments

- Staatsbosbeheer for providing access to historical documents
- Archive manager Finn for domain expertise and feedback

---

**Last Updated**: December 17, 2025
