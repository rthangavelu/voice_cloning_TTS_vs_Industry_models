
# Voice Cloning Benchmark

Data from https://www.kaggle.com/code/beastlyprime/tensorflow-speaker-verification


This project benchmarks **open-source** and **industry** Text-to-Speech (TTS) / Voice Cloning
models.
It uses **multi-sample per speaker** (multiple reference recordings for each speaker) and generates
**one audio per text page per model**.
---
## Features
- Compare **Open Source Models** (SpeechBrain Tacotron2 + HiFiGAN, Coqui TTS, etc.)
- Compare **Industry Models**:
- OpenAI GPT-4o-mini-TTS
- Microsoft Azure Cognitive Services TTS
- ElevenLabs TTS (with pre-created `voice_id`)
- Generate **page-wise audio outputs** for audiobook workflows.
- Measure **inference time**, **cost**, and **similarity (cosine for open-source)**.
- Visualize results with **bar plots and box plots**.
---
##  Project Structure
```
data/
    Sample_voice1/
       sample1.wav
       sample2.wav
    results/ (auto-generated audios)
      Sample_voice2/
```
---
## API Keys Setup
Set your keys as environment variables:
```bash
export OPENAI_API_KEY="your_openai_key"
export ELEVENLABS_API_KEY="your_elevenlabs_key"
```
For ElevenLabs, create a **custom cloned voice** in your dashboard and note its `voice_id`.
Then update the script:
```python
```
ELEVENLABS_VOICE_ID = "your_precreated_voice_id_here"
---
## Usage
1. Place sample voices in `data/Sample_voice*/` folders.
- Example: `data/Sample_voice1/sample1.wav`, `sample2.wav`
2. Run the benchmark:
```bash
python benchmark_notebook.py
```
3. Results:
- Audio outputs in each speaker’s `results/` folder.
- Metrics stored in `benchmark_results_multisample.csv`.
- Visualization plots shown inline.
---
##  Metrics Collected
- **Inference Time (s)** per page per model.
- **Cost (USD)** for industry APIs.
- **Cosine Similarity** for open-source speaker embeddings (using SpeechBrain ECAPA).
---
# Conclusion & Analysis
### Strengths
- **Open Source (SpeechBrain Tacotron2 + HiFiGAN)**:
- Free to run, no API costs.
- Decent similarity with reference voices.
- Slower inference than industry APIs.
- **OpenAI GPT-4o-mini-TTS**:
- Very fast inference.
- High naturalness.
- Cost-efficient ($0.15/min).
- **ElevenLabs**:
- Best **voice cloning quality** across multiple samples.
- Natural prosody and emotional variation.
- Easy API usage with pre-created `voice_id`.
###  Limitations
- **Open Source**: Struggles with prosody, requires GPU for speed.
- **Industry Models**: Require API keys, costs scale with usage.
- **ElevenLabs**: Needs manual pre-creation of voices (can’t auto-create each time due to API limits).
### Winner (Overall)
- For **voice cloning realism** → **ElevenLabs**.
- For **speed and cost-efficiency** → **OpenAI GPT-4o-mini-TTS**.
- For **open research & free usage** → **SpeechBrain (Tacotron2 + HiFiGAN)**.
---
 **Recommendation**:
- Use **ElevenLabs** for final audiobook / production pipelines.
- Use **OpenAI TTS** for rapid prototyping & cost-effective narration.
- Explore **open-source** for custom training and research.
