# ISDN 3150 Week 2 Assignment: From Image to Text — Understanding Visual Content with Language Models

## 🎯 Overview

This assignment explores the intersection of **computer vision** and **natural language processing** by converting personal images into **ASCII art representations** and analyzing them using **Large Language Models (LLMs)**. 

The central research question: *Can a language model understand and describe visual content from a text-based image representation alone?*

## 📁 Project Structure

```
Week2/
├── ISDN3150_Week2_Assignment.ipynb           # 🔴 Main assignment notebook (START HERE)
├── ISDN3150_Week2_Assignment-Updated.ipynb   # Updated version with all improvements
├── ISDN3150_Week2_Section1.ipynb             # Supplementary material - Section 1
├── ISDN3150_Week2_Section2.ipynb             # Supplementary material - Section 2
├── ISDN3150_Week2_Section3.ipynb             # Supplementary material - Section 3
├── imgs/                                      # Sample images for testing
├── README.md                                  # This file
```

## 📋 What You'll Learn

- **Image Processing**: Resize, normalize, and enhance images using OpenCV
- **ASCII Art Generation**: Map pixel brightness to character representations
- **Histogram Equalization**: Improve image contrast for better ASCII output
- **API Integration**: Connect to Azure OpenAI for LLM analysis
- **Prompt Engineering**: Craft effective prompts for visual understanding

## 🔧 Technical Implementation

### Cell 1: Image Processing Setup
**Imports and Configuration**
- NumPy, OpenCV, PIL, Requests libraries
- Character mapping set: `@W#$OEXC[(/?=^~_.`` ` (19 characters, ordered by visual density)
- Three image URLs configured for batch processing

### Cell 2: Image-to-Text Conversion
**The `mono()` Function** - Converts grayscale images to ASCII art
- **Input**: Grayscale NumPy array + target dimensions
- **Processing Pipeline**:
  1. **Aspect Ratio Preservation**: Calculates dimensions to maintain proportions
  2. **Resizing**: Uses OpenCV to resize image efficiently
  3. **Histogram Equalization**: Applies `cv2.equalizeHist()` to enhance contrast and clarity
  4. **Normalization**: Scales pixel values to 0-255 range
  5. **Character Mapping**: Maps brightness levels to ASCII characters
- **Output**: String representation suitable for LLM analysis

**Image Processing Loop** - Handles multiple images
- Downloads images from URLs (supports GitHub raw links)
- Converts RGB/RGBA to grayscale automatically
- Generates ASCII art for each image (50x100 dimensions)
- Stores all results in `ascii_arts` list for batch LLM analysis

### Cell 3: Language Model Analysis
**Multi-Image LLM Processing**
- Iterates through all 3 ASCII art representations
- For each image, requests the model to:
  - Describe observations in the text representation
  - Infer object type (face, person, landscape, etc.)
  - Identify visible features and characteristics
- Displays formatted output with clear separation between analyses

## 📦 Installation & Setup

### Required Libraries
numpy
opencv-python (cv2)
Pillow (PIL)
requests
openai (Azure OpenAI SDK)
python-dotenv
```

### Install Dependencies
```bash
pip install numpy opencv-python pillow requests openai python-dotenv
```

### Azure OpenAI Configuration
1. **Get API Key**: Obtain from your Azure portal
2. **Create `.env` file** in the project directory:
   ```
   AZURE_OPENAI_API_KEY=your_api_key_here
   AZURE_OPENAI_ENDPOINT=https://your-resource.openai.azure.com/
   ```
3. **Update Notebook**: Code automatically loads from `.env` using `load_dotenv()`

## 🚀 How to Run

### Step 1: Prepare Environment
```bash
# Install dependencies
pip install -r requirements.txt

# Create .env file with your Azure OpenAI credentials
echo AZURE_OPENAI_API_KEY=your_key_here > .env
```

### Step 2: Run the Notebook
- Open `ISDN3150_Week2_Assignment.ipynb` in Jupyter/VS Code
- **Cell 1**: Loads libraries, defines `mono()` function, sets up URLs
- **Cell 2**: Downloads 3 images, generates ASCII art for each
- **Cell 3**: Analyzes all 3 ASCII representations with GPT-4o-mini

### Step 3: Customize (Optional)
```python
# Change image URLs
urls = [
    "your_image_url_1.jpg",
    "your_image_url_2.jpg",
    "your_image_url_3.jpg"
]

# Adjust ASCII art dimensions
ascii_art = mono(im, target_h=75, target_w=150)  # Larger output

# Modify LLM prompt
prompt_content = f"""Custom prompt here: {ascii_art}"""
```

## 🎨 Key Algorithm: Image to ASCII

### Character Set Density
```
Darkest (most pixels per character):    @  W  #  $  O  E  X  C  (
Middle (medium density):                 [  /  ?  =  ^  ~  _  .
Lightest (fewest pixels per character):   ` (space)
```

### Processing Steps
1. **Resize**: Maintain aspect ratio with target dimensions (50×100)
2. **Equalize**: `cv2.equalizeHist()` boosts contrast for clearer features
3. **Normalize**: Scale pixel values evenly across character set
4. **Map**: Brightness level → character index
5. **Output**: Text grid for LLM analysis

## 💡 Key Features

### Histogram Equalization
- **What it does**: Spreads pixel intensity distribution for better contrast
- **When to use**: Low-contrast images or when ASCII art lacks detail
- **Effect**: Makes edges sharper, improves feature visibility in ASCII output

### Multi-Image Processing
- Process 3 images in a single notebook run
- Batch analysis with Azure OpenAI's GPT-4o-mini
- Organized output with clear separation between results
- Reduces API call overhead vs. single-image approach

### Flexible Input Handling
- Supports GitHub raw image links
- Handles RGB, RGBA, and grayscale formats
- Automatic format conversion to grayscale
- Array-based processing for efficiency

## 📊 Expected Output Example

**ASCII Art Sample:**
```
@@@@WWWW####$$$$OOOOEEEEXXXX
@@WW##$$OOEEXXCC((((????====
@W##$OEX[[[[//////????====^^
...
```

**LLM Analysis Sample:**
```
Based on this ASCII art representation, I can observe:

1. **Visual Observations**: The pattern shows a concentrated area of darker characters 
   (@, W, #) in the upper left, transitioning to lighter characters towards the right...

2. **Object Inferred**: This appears to be a human face or portrait, with the darker 
   areas representing facial features like eyes and the face structure...

3. **Identified Features**: 
   - Distinct facial contours
   - Two concentrated areas suggesting eyes
   - Overall symmetry typical of face images
```

## 🔍 Troubleshooting

| Issue | Solution |
|-------|----------|
| **"No module named 'openai'"** | Run `pip install openai` |
| **"Connection refused" error** | Check internet connection and Azure endpoint |
| **Low ASCII art quality** | Increase `target_h` and `target_w` values |
| **API Key errors** | Verify `.env` file is in correct location with valid API key |
| **Image won't download** | Check URL is valid and publicly accessible |

## 📈 Performance Tips

- **Faster Processing**: Reduce dimensions (`target_h=40, target_w=80`)
- **Better Quality**: Increase dimensions (`target_h=80, target_w=160`)
- **Cost Optimization**: Process multiple images per API call using batch mode
- **Clarity**: Use contrast-rich images (portraits, high-contrast scenes)

## 🎓 Learning Objectives

By completing this assignment, you will:
- ✅ Understand image-to-text transformation techniques
- ✅ Apply histogram equalization for image enhancement
- ✅ Integrate external APIs into Python workflows
- ✅ Design prompts for effective LLM visual understanding
- ✅ Analyze AI model capabilities and limitations
- ✅ Work with multi-step processing pipelines

## 📝 Notes

- **Aspect Ratio**: The algorithm automatically calculates and preserves image proportions
- **Character Order**: From darkest (@) to lightest (space) for intuitive brightness mapping
- **LLM Limitations**: ASCII interpretation depends on image clarity and model capability
- **Target Dimensions**: 50×100 provides good balance between clarity and readability

## 📚 References

- OpenCV Documentation: https://docs.opencv.org/
- Azure OpenAI: https://learn.microsoft.com/en-us/azure/ai-services/openai/
- ASCII Art History: https://en.wikipedia.org/wiki/ASCII_art

## ✍️ Author

ISDN 3150 - Information Systems and Design Network  
Week 2 Assignment - Spring 2026

---

**Questions or Issues?** Contact your course instructor or check Azure OpenAI documentation.