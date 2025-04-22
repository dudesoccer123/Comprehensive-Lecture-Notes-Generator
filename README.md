# Comprehensive-Lecture-Notes-Generator

A powerful tool that automates the generation of comprehensive lecture notes by combining transcribed audio from university lectures with content from lecture slides. The system uses OpenAI's Whisper model for transcription, vector embeddings for semantic search, and LLaMa 70B for content generation.

## Overview

This project streamlines the note-taking process by:

1. Transcribing lecture videos using OpenAI's Whisper model
2. Processing lecture slides (PowerPoint) to extract content
3. Storing transcriptions in a vector database for semantic search
4. Generating comprehensive notes by combining relevant transcripts with slide content
5. Outputting professional-quality PDF notes

## Technical Architecture

┌───────────────┐    ┌───────────────┐    ┌───────────────┐
│  Video Input  │    │  PPT Slides   │    │     Groq      │
│    (.mp4)     │    │    (.pptx)    │    │    API Key    │
└───────┬───────┘    └───────┬───────┘    └───────┬───────┘
        │                    │                    │
┌───────▼───────┐    ┌───────▼───────┐    ┌───────▼───────┐
│ Audio         │    │ Slide Content │    │  LLM Access   │
│ Extraction    │    │ Extraction    │    │               │
└───────┬───────┘    └───────┬───────┘    └───────┬───────┘
        │                    │                    │
┌───────▼───────┐    ┌───────▼───────┐            │
│ Audio         │    │ Topic-Content │            │
│ Chunking      │    │ Mapping       │            │
└───────┬───────┘    └───────┬───────┘            │
        │                    │                    │
┌───────▼───────┐            │                    │
│ Whisper       │            │                    │
│ Transcription │            │                    │
└───────┬───────┘            │                    │
        │                    │                    │
┌───────▼───────┐            │                    │
│ ChromaDB      │◄───────────┘                    │
│ Vector Store  │                                 │
└───────┬───────┘                                 │
        │                                         │
┌───────▼─────────────────────────────────────────▼───────┐
│                   LangChain Pipeline                     │
│     (Combines transcript chunks with slide content)      │
└───────────────────────────────┬─────────────────────────┘
                                │
                        ┌───────▼───────┐
                        │  PDF Output   │
                        │ (Final Notes) │
                        └───────────────┘


## Requirements

- Python 3.10+
- Groq API key (for LLM access)
- Required Python libraries:
  - `groq`
  - `moviepy`
  - `pydub`
  - `langchain`
  - `langchain_groq`
  - `pptx`
  - `markdown2`
  - `xhtml2pdf`
  - `Pillow`
  - `sentence-transformers`

## Installation and Setup

1. Clone the repository
2. Install required dependencies:
   ```bash
   pip install groq moviepy pydub langchain langchain_groq python-pptx markdown2 xhtml2pdf pillow sentence-transformers

3. Create a key.txt file with your groq API key.

## Note Generation Pipeline
LangChain is used to create a processing pipeline that:

Takes a topic from the lecture slides
Finds relevant transcription chunks from the vector database
Uses LLaMa 70B model (via Groq) to generate comprehensive notes

The prompt template is defined as: 
```
prompt_temp = PromptTemplate.from_template('''
    ### UNIVERSITY LECTURE TRANSCRIPT:
    {lecture_transcript}

    ### LECTURE SLIDE CONTENT:
    {slides_content}

    ###TOPIC:
    {unique_topic}

    ###INSTRUCTIONS:
    You are John, An expert at making comprehensive academic notes. 
    You are required do exactly what you are good at. Given the lecture transcripts and the lecture slide content for a particular topic, generate
    comprehensive lecture notes for the same covering all important details, merging the information from the slides and the transcripts.
    ensure the text is correctly formatted.

    DO NOT provide a preamble.
    ### ANSWER (NO PREAMBLE):
''')
```

Usage

Place your lecture video file in the project directory
Place your lecture PowerPoint slides in the project directory
Update file paths in the notebook
Run the notebook cells sequentially
Retrieve generated PDF notes

Benefits

Time Efficiency: Automates the tedious process of manual note-taking
Comprehensive Coverage: Combines visual slide content with spoken explanations
Semantic Relevance: Uses vector search to match transcripts with relevant slide topics
High Quality Output: Leverages state-of-the-art LLMs for coherent, well-structured notes

Limitations

Requires high-quality audio for accurate transcription
Slide content extraction works best with text-based slides (vs. image-heavy slides)
Processing large videos may require substantial computational resources

Future Improvements

Support for additional slide formats (Google Slides, PDF)
Multi-language support
Improved image extraction and processing
Interactive web interface
Real-time processing capabilities

License
MIT License
