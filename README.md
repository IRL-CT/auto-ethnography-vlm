# Video Annotation Tool 

**Automated video annotation and analysis tool using Google Gemini Vision Language Model for behavioral research**

Transform hours of manual video annotation into minutes of automated analysis while maintaining research-grade accuracy. Originally developed at Cornell's Interaction Research Lab for human-robot interaction studies.

## How It Works

```
📁 Box Video → 🤖 Gemini VLM → 📊 Excel Annotations
```

The tool automatically:
1. **Downloads** videos from Box (with OAuth authentication)
2. **Chunks** large files (>2GB) into processable segments
3. **Analyzes** each segment with Gemini's vision capabilities
4. **Extracts** interactions, dialogue, emotions, and behaviors
5. **Combines** results into structured Excel output

## Quick Start

### Prerequisites
- Google Cloud account with Gemini API access
- Box account with videos to analyze
- Google Colab (highly recommended so you can link with Google Drive) 

### One-Command Setup
```python
# In Google Colab - run this cell:
!pip install google-generativeai boxsdk pandas openpyxl

# Configure your credentials
GEMINI_API_KEY = "your-gemini-api-key"
BOX_CLIENT_ID = "your-box-client-id" 
BOX_CLIENT_SECRET = "your-box-client-secret"
```

### Run Analysis
```python
# Get Box file ID from URL: box.com/file/123456789 → use "123456789"
BOX_FILE_ID = "123456789"
OUTPUT_PATH = "annotations.xlsx"

df, annotations = complete_box_to_annotations_pipeline(BOX_FILE_ID, OUTPUT_PATH)
```

## What You Get

### Structured Output
Each interaction includes:
- **Timestamps** (start/end times)
- **Interaction type** (approaching, talking, photographing, etc.)
- **Detailed observations** (behavior, body language, context)
- **Direct quotes** from audio
- **Emotional classification** (positive, negative, neutral, mixed)
- **Confidence scores** (0.0-1.0)

### Sample Results
| Time | Event | Observations | Dialogue | Emotion |
|------|--------|-------------|----------|----------|
| 02:15-02:34 | talking | Woman approaches robot hesitantly, takes photo while laughing with friend | "What is this thing? It's so cool!" | positive |
| 05:42-06:01 | avoiding | Man deliberately walks wide path around robot, shakes head | "I don't trust those things" | negative |

## Performance Validation

**Tested on 5-minute HRI video segments:**
- **Precision**: 90% (9/10 auto-detected were valid!)
- **Recall**: 75% (9/12 human-detected were found)
- **Agreement on interaction types**: 89%
- **Time savings**: ~95% reduction in annotation time

The system consistently identifies major social interactions while occasionally missing very brief or ambiguous behaviors.

## Technical Features

### Smart File Handling
- **Small files** (<2GB): Direct processing
- **Large files** (>2GB): Automatic chunking with timestamp coordination
- **Any length**: From minutes to hours of footage

### Cost Efficiency
- **~$0.04 per 26-minute video** (Gemini Flash)
- **~$2-5 for 20 hours** of video analysis
- Automatic cleanup of temporary files

### Research Integration
- Excel output compatible with statistical software
- Confidence scoring for quality control
- Maintains original video timestamps across chunks

## Use Cases

- **Human-Robot Interaction**: Public reactions to autonomous systems
- **Public Space Studies**: Social dynamics in urban environments
- **Accessibility Research**: Barrier identification and accommodation analysis
- **Customer Behavior**: Shopping and service interaction patterns
- **Educational Research**: Classroom interaction analysis

## Setup Guide

### 1. Google Cloud Setup
1. Create Google Cloud account
2. Enable Gemini API
3. Create API key
4. Set billing alerts ($10/month recommended)

### 2. Box Integration
1. Create Box developer app
2. Get Client ID and Secret
3. Set redirect URL to: `https://irl.tech.cornell.edu/video-annotator/box-oauth-redirect.html`

### 3. Run in Colab
1. Open the notebook in Google Colab
2. Add your credentials
3. Run the complete pipeline function

## Limitations & Best Practices

### What Works Best
- Clear video quality with audible speech
- Direct human interactions and behaviors
- Videos with obvious social dynamics

### Current Limitations
- **File size**: 2GB max per chunk (handled automatically)
- **Subtle behaviors**: May miss very brief or ambiguous actions
- **Audio dependent**: Requires clear speech for dialogue capture
- **Processing time**: ~2-3 minutes per video minute

### Recommended Workflow
1. Test on a sample video first
2. Review low-confidence annotations manually
3. Validate results against manual coding subset
4. Document any prompt modifications for reproducibility

## Research Applications

Originally developed for human-robot interaction studies at Cornell's Interaction Research Lab under Dr. Wendy Ju. The tool addresses the common research challenge of vast amounts of unanalyzed video data sitting in storage.

### Citation
*If you use this tool in your research, please cite the Interaction Research Lab at Cornell University.*

## Contributing

This tool is actively developed for research use. Suggestions and improvements welcome for:
- Additional interaction categories
- Domain-specific prompt templates  
- Integration with other video platforms
- Statistical analysis extensions

---

**Cornell Interaction Research Lab** | *Making video analysis easier for researchers!*