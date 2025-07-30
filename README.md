# Auto-Ethnography VLM

**Automated video ethnography tool using Google Gemini VLM for social interaction analysis**

A research tool that automatically annotates human-robot interactions and social behaviors in video footage, reducing manual annotation time from hours to minutes while maintaining research-grade accuracy.

## Overview

This tool leverages Google's Gemini Vision Language Model (VLM) to automatically detect, categorize, and annotate social interactions in video data. Originally developed for human-robot interaction (HRI) research, it can be adapted for various ethnographic studies including public space dynamics, accessibility research, and behavioral analysis.

### Key Features

- **Automated interaction detection** with detailed behavioral observations
- **Dialogue capture** from audio with sentiment analysis  
- **Configurable event categories** for different research domains
- **Structured output** compatible with statistical analysis software
- **Multi-modal analysis** combining visual and audio cues
- **Research-grade annotations** with confidence scoring

## Quick Start

### Prerequisites

- Google Cloud account with billing enabled
- Gemini API access
- Python 3.7+ environment (Google Colab recommended)

### Installation

1. **Set up Google Cloud billing** and create budget alerts
2. **Enable Gemini API** in Google Cloud Console
3. **Install dependencies**:
   ```bash
   pip install google-generativeai pandas openpyxl
   ```

### Basic Usage

```python
import google.generativeai as genai
from auto_ethnography_vlm import EnhancedVideoAnalyzer

# Configure API
genai.configure(api_key="your-gemini-api-key")

# Initialize analyzer
analyzer = EnhancedVideoAnalyzer()

# Process video
video_path = "path/to/your/video.mp4"
output_path = "annotations_output.xlsx"

df, annotations = analyzer.process_video(video_path, output_path)
print(f"Found {len(annotations)} interactions")
```

## Validation Results

**Tested on 5-minute HRI video segments:**
- **Human annotator**: 12 interactions identified
- **Auto-Ethnography VLM**: 10 interactions identified  
- **Precision**: 90% (9/10 auto-detected were valid)
- **Recall**: 75% (9/12 human-detected were found)
- **Agreement on interaction types**: 89%

The tool consistently identifies major social interactions with high confidence, occasionally missing very brief or ambiguous behaviors that human annotators catch.

## Research Applications

### Current Use Cases
- **Human-Robot Interaction Studies**: Analyze public reactions to autonomous robots
- **Public Space Ethnography**: Study social dynamics in urban environments  
- **Accessibility Research**: Identify barriers and accommodations in public spaces
- **Customer Behavior Analysis**: Understand shopping and service interactions

### Output Data Structure

| Field | Description | Example |
|-------|-------------|---------|
| `Start Time` | Interaction start timestamp | "02:15" |
| `End Time` | Interaction end timestamp | "02:34" |
| `Event` | Interaction category | "photographing" |
| `Observations` | Detailed behavioral description | "Woman takes photo of robot while laughing with friend" |
| `Dialogue Captured` | Direct quotes from audio | "What is this thing? It's so cool!" |
| `Emotional Reaction` | Sentiment classification | "positive" |
| `Confidence` | Model confidence score (0-1) | 0.89 |

## Configuration for Different Research Domains

### Custom Study Configuration

Create a YAML configuration file for your research domain:

```yaml
# public_space_study.yaml
study_name: "Public Space Social Dynamics"
interaction_types:
  - "conversation"
  - "personal_space_negotiation" 
  - "device_usage"
  - "environmental_interaction"
analysis_focus: "spontaneous social behaviors and spatial dynamics"
custom_fields:
  group_size: "number of people in interaction"
  space_type: "type of public space (plaza, park, etc.)"
```

### Adapting for Your Research

1. **Define interaction categories** relevant to your study
2. **Customize observation prompts** for your research questions
3. **Modify output fields** to capture domain-specific data
4. **Adjust confidence thresholds** based on your accuracy requirements

## Limitations

### Technical Constraints
- **File size limit**: 2GB maximum per video file (Gemini API constraint)
- **Processing time**: ~2-3 minutes per minute of video footage
- **API costs**: ~$0.10-0.20 per hour of video processed

### Methodological Considerations
- **Optimized for clear interactions**: May miss very subtle or brief behaviors
- **Audio-dependent dialogue capture**: Requires clear speech for accurate quotes
- **Context interpretation**: Better with direct interactions than inferential behaviors
- **Reproducibility**: Small variations in output between runs (inherent to LLMs)

### Recommended Practices
- **Validate on sample data** before large-scale processing
- **Review low-confidence annotations** manually
- **Use consistent video quality** and audio settings across datasets
- **Document any prompt modifications** for research reproducibility

## Cost Estimation

**Gemini 1.5 Flash pricing (recommended model):**
- Input: $0.075 per 1M tokens
- Typical cost: **~$0.04 per 26-minute video**
- Large study (20 hours): **~$2-5 total**

**Budget recommendations:**
- Set up $10 monthly budget alerts in Google Cloud
- Monitor usage in early processing phases
- Consider Gemini 1.5 Pro ($1.25/1M tokens) for higher accuracy needs


