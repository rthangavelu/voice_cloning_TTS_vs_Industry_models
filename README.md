# Voice Cloning Benchmark

Data from: [Kaggle TensorFlow Speaker Verification](https://www.kaggle.com/code/beastlyprime/tensorflow-speaker-verification)  

This project benchmarks **open-source** and **industry** Text-to-Speech (TTS) / Voice Cloning models.

It uses **multi-sample per speaker** (multiple reference recordings for each speaker) and generates **one audio per text page per model**.

---

## Features

- Compare **Open Source Models**  
  - SpeechBrain Tacotron2 + HiFiGAN  
  - Coqui TTS, etc.  

- Compare **Industry Models**  
  - OpenAI GPT-4o-mini-TTS
  - ElevenLabs TTS (with pre-created `voice_id`)  

- Generate **page-wise audio outputs** for audiobook workflows  
- Measure **inference time**, **cost**, and **similarity** (cosine similarity for open-source models)  
- Visualize results with **bar plots** and **box plots**

---

## Project Structure
data/
Sample_voice1/
sample1.wav
sample2.wav
results/ # Auto-generated audio outputs
Sample_voice2/


---

## API Keys Setup

Set your API keys as environment variables:

```bash
export OPENAI_API_KEY="your_openai_key"
export ELEVENLABS_API_KEY="your_elevenlabs_key"


**For ElevenLabs:**
Create a custom cloned voice in your dashboard and note its voice_id.
Update the script:
ELEVENLABS_VOICE_ID = "your_precreated_voice_id_here"

#### Usage

Place sample voices in data/Sample_voice*/ folders
Example: data/Sample_voice1/sample1.wav, sample2.wav

#### Run the benchmark:
python benchmark_notebook.py

#### Results:
Audio outputs saved in each speaker’s results/ folder
Metrics stored in benchmark_results_multisample.csv
Visualization plots displayed inline


### Metrics Collected

Inference Time (s) per page per model
Cost (USD) for industry APIs
Cosine Similarity for open-source speaker embeddings (using SpeechBrain ECAPA)

## Conclusion & Analysis
**Strengths**
   _Open Source (SpeechBrain Tacotron2)_
      Free to run, no API costs
      Decent similarity with reference voices
      Slower inference than industry APIs

   _OpenAI GPT-4o-mini-TTS_
      Very fast inference
      High naturalness
      Cost-efficient ($0.15/min)
   _ElevenLabs_
      Best voice cloning quality across multiple samples
      Natural prosody and emotional variation
      Easy API usage with pre-created voice_id

### Limitations
**Open Source**: Struggles with prosody, requires GPU for speed
**Industry Models**: Require API keys; costs scale with usage

ElevenLabs: Needs manual pre-creation of voices (cannot auto-create due to API limits)

## Winner (Overall)
For voice cloning realism → ElevenLabs
For speed and cost-efficiency → OpenAI GPT-4o-mini-TTS
For open research & free usage → SpeechBrain (Tacotron2 + HiFiGAN)

## Recommendation

Use ElevenLabs for final audiobook / production pipelines
Use OpenAI TTS for rapid prototyping & cost-effective narration
Explore open-source for custom training and research



### Conclusion

##### The voice cloning benchmark revealed several key insights about the performance and usability of different models:

#### Open-Source Models (Your_TTS, VITS):

These models provide good voice cloning quality when multiple sample files per speaker are used.
They are cost-effective and allow flexible multi-speaker cloning.
The inference time is slightly higher compared to industry APIs, but they are fully under our control and can be scaled locally.

#### Industry Models (ElevenLabs, OpenAI TTS, Azure TTS):

ElevenLabs demonstrates very high-quality voice cloning and naturalness, producing near-human results.
OpenAI and Azure TTS also deliver reliable output with consistent quality.

However, when cloning multiple voices and generating a full audiobook with conversational details, the cost rises significantly, especially for models like ElevenLabs.Despite their efficiency and speed, scaling up to multiple voices or long-form content can become expensive, making open-source models preferable for projects requiring many speakers or extended audio.

#### Overall Recommendation:

For high-quality single-voice cloning, industry models like ElevenLabs are ideal.

For multi-speaker audiobooks or budget-conscious scenarios, open-source TTS models like Your_TTS and VITS offer a practical balance between quality, flexibility, and cost.

Combining open-source models for bulk content and industry models for premium segments could be a hybrid strategy for audiobook production.

