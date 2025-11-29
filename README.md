# Damascus Dialect Data Gathering Pipeline

## 1. Project Purpose

This project provides a complete end-to-end pipeline for processing
Damascene (Syrian) dialect audio data.\
It transforms raw audio recordings into clean, structured linguistic
datasets suitable for:

-   Training ASR (speech-to-text) models\
-   NLP model training\
-   Dialect and linguistic research\
-   Building lexicons for Syrian dialects

The final output includes transcripts, normalized texts, tokens, POS
tags, and database-ready metadata.

## 2. Technologies and Tools Used

### 1) Audio Collection

All Damascene audio recordings are stored in a single directory.\
Supported formats include: **wav, mp3, m4a, flac, mpeg**.

### 2) Automatic Transcription (Speech-to-Text)

**Tools Used:** - OpenAI **Whisper (large-v3)** - torch, librosa,
soundfile, pydub

**Outputs:** - Full transcription - Language detection - Audio
duration - Error logs - Timestamp for each processed file

### 3) Text Cleaning and Normalization

Cleaning operations include: - Unicode normalization\
- Removing diacritics\
- Removing tatweel and invisible characters\
- Standardizing alef forms\
- Removing emojis and non-Arabic symbols\
- Reducing repeated characters\
- Collapsing multiple spaces

### 4) Tokenization

Tokenization using CAMeL Tools: - Extract tokens\
- Clean tokens\
- Link tokens to filenames and IDs

### 5) Duplicate & Similar Word Detection

Detects: - Exact duplicates\
- Near-duplicate words using fuzzy matching (RapidFuzz)

### 6) POS Tagging

Uses **Stanza** to assign POS tags to each word.

### 7) Dataset Preparation

Final dataset fields:

    dialect_region  
    word_or_phrase  
    gloss_ar  
    pos  
    source  
    filename  
    source_url

### 8) Upload to Supabase PostgreSQL

-   Batch upload (100 rows per batch)\
-   Supabase Python client\
-   PostgreSQL backend

## 3. Pipeline Workflow

    [ Audio Files ]
            ↓
    Whisper Transcription
            ↓
    Text Normalization
            ↓
    Tokenization
            ↓
    Duplicate & Fuzzy Matching
            ↓
    POS Tagging (Stanza)
            ↓
    Dataset Formatting
            ↓
    Supabase / PostgreSQL Upload

## 4. Final Output

This pipeline produces a complete Damascene dialect dataset: -
Transcripts\
- Normalized text\
- Tokens\
- Unique vocabulary\
- Fuzzy duplicate detection\
- POS tags\
- Database-ready CSV
