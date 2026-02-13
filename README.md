# ISDN3150 Week 2 Assignment: Image to Text — Understanding Visual Content with Language Models

## Overview

This assignment explores how visual information can be represented in textual form and how large language models (LLMs) can reason about such representations. The core objective is to convert a personal image into a text-based (ASCII-style) image and investigate whether a language model can understand and describe visual content from the textual representation alone.

## Project Structure

```
Week2/
├── ISDN3150_Week2_Assignment.ipynb      # Main assignment with image-to-text conversion and LLM analysis
├── ISDN3150_Week2_Section1.ipynb        # Supplementary learning material - Section 1
├── ISDN3150_Week2_Section2.ipynb        # Supplementary learning material - Section 2
├── ISDN3150_Week2_Section3.ipynb        # Supplementary learning material - Section 3
├── imgs/                                 # Directory containing sample images
├── README.md                             # This file
```

## Assignment Tasks

### Part 1: Image-to-Text Conversion (`mono` function)
- **Objective**: Convert a grayscale image into an ASCII art representation
- **Implementation**:
  - Resizes image while maintaining aspect ratio
  - Maps pixel brightness (0-255) to a character string: `@W#$OEXC[(/?=^~_.`` `
  - Normalizes pixel values for even distribution across character set
  - Returns a text representation suitable for LLM analysis

### Part 2: Image Acquisition & Processing
- **Objective**: Load and prepare an image for conversion
- **Implementation**:
  - Downloads image from a URL (or loads from local file)
  - Converts to NumPy array for processing
  - Converts RGB/RGBA images to grayscale
  - Calls the `mono()` function to generate ASCII art

### Part 3: Language Model Interpretation
- **Objective**: Analyze the ASCII art using Azure OpenAI's GPT-4 mini model
- **Implementation**:
  - Sends the ASCII art representation to the LLM
  - Requests the model to:
    1. Describe what it observes in the text-based image
    2. Infer the object type (face, person, landscape, etc.)
    3. Identify visible features or characteristics
  - Records and displays the model's response

## Prerequisites

### Required Libraries
```
numpy
opencv-python (cv2)
Pillow (PIL)
requests
openai (Azure OpenAI)
```

### Required Credentials
- **Azure OpenAI API Key**: Obtain from your Azure account
- Update the `api_key` variable in the LLM analysis cell with your actual credentials

## How to Use

1. **Configure API Key**: 
   - Open `ISDN3150_Week2_Assignment.ipynb`
   - Replace `"!!! put your api keys here"` with your Azure OpenAI API key

2. **Run the Notebook**:
   - Cell 1: Defines imports and the `mono()` conversion function
   - Cell 2: Downloads/loads image and generates ASCII art
   - Cell 3: Sends ASCII art to LLM for analysis

3. **Customize**:
   - Replace the image URL with your own image path
   - Adjust `target_h` and `target_w` parameters for different ASCII art sizes
   - Modify the prompt in Cell 3 for different LLM queries

## Key Features

- **Aspect Ratio Preservation**: Maintains proportions when resizing images
- **Character Mapping**: Uses a 19-character set with varying density to represent brightness levels
- **Flexible Input**: Supports both URL-based and local image files
- **LLM Integration**: Leverages Azure OpenAI GPT-4 mini for visual understanding

## Example Output

The ASCII art conversion produces a text representation like:
```
@@@@@@@@WWWW###$$$$OOOEEEXXX
@@WWWW####$$$$OOOEEECCC(((([
...
```

The LLM then analyzes this representation to identify objects, features, and characteristics.

## Notes

- ASCII art quality depends on image resolution and target dimensions
- Larger dimensions (e.g., 100x100) provide more detail but may be harder to read
- The character set `@W#$OEXC[(/?=^~_.`` ` is ordered by visual density
- LLM interpretation accuracy varies based on image complexity and ASCII art clarity

## Author

ISDN 3150 - Information Systems and Design Network