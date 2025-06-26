#  AI Talking Avatar Generator 🎥  
Generate a hyper-realistic talking avatar from a text topic using a pipeline of cutting-edge models including Stable Diffusion, TinyLLaMA, gTTS, and SadTalker – all deployed on **Kaggle** with GPU.

---

##  Overview

This project creates an AI tutor-like talking avatar video from a text topic using the following steps:

1. **Topic Input**
2. **Avatar Image Generation** using Stable Diffusion
3. **Script Generation** using TinyLLaMA
4. **Voice Synthesis** using Google Text-to-Speech (gTTS)
5. **Avatar Animation** using SadTalker
6. **Face Enhancement** using GFPGAN

---

##  Pipeline Architecture

```mermaid
graph TD
A[User Input: Topic] --> B[Stable Diffusion (Avatar Image)]
B --> C[TinyLLaMA (Script)]
C --> D[gTTS (Audio)]
D --> E[SadTalker (Animation)]
E --> F[GFPGAN (Face Enhancement)]
F --> G[Final MP4 Video]
```

---

##  Environment

- Platform: **Kaggle Notebooks**
- GPU:  Required
- Python: 3.11+
- Key Libraries: `diffusers`, `transformers`, `gTTS`, `torch`, `SadTalker`

---

##  Installation & Setup (in Kaggle)

###  STEP 0: Install Dependencies

```bash
!pip install -q diffusers transformers accelerate sentence-transformers gTTS faiss-cpu gradio
!pip install -q git+https://github.com/CompVis/taming-transformers.git
!pip install -q opencv-python==4.7.0.72 face_alignment imageio nest_asyncio
```

---

### ✅ STEP 1: Get Topic from User

```python
topic = input("📥 Enter the topic you want the avatar to explain: ").strip()
```

---

###  STEP 2: Generate Avatar Image

```python
from diffusers import StableDiffusionPipeline
# ... (see full notebook for full function)
```

---

###  STEP 3: Generate Script Using TinyLLaMA

```python
from transformers import AutoTokenizer, AutoModelForCausalLM
# ... (text generation using <|system|>, <|user|> format)
```

---

###  STEP 4: Text-to-Speech (gTTS)

```python
from gtts import gTTS
tts = gTTS(text=script, lang='en')
tts.save("audio.mp3")
```

---

### ✅ STEP 5: Set Up SadTalker

```bash
!git clone https://github.com/OpenTalker/SadTalker.git
%cd SadTalker
!bash scripts/download_models.sh
!pip install -r requirements.txt
```

---

### 🛠 FIX: Dependency Patching

```bash
!pip install numpy==1.23.5 --force-reinstall
# Restart the kernel manually in Kaggle here
```

Then:

```bash
!pip uninstall -y imageio
!pip install imageio==2.31.1
```

---

###  STEP 6: Run Inference

```python
import sys
sys.setrecursionlimit(20000)

!python inference.py \
  --driven_audio audio.mp3 \
  --source_image avatar.jpg \
  --result_dir results \
  --still \
  --enhancer gfpgan
```

---

##  Output

- Final video is saved at:
  ```
  SadTalker/results/<timestamp>/avatar##audio_enhanced.mp4
  ```

---

##  Sample Output

![Sample Avatar](https://via.placeholder.com/500x280.png?text=Generated+Avatar+Preview)

---

##  Acknowledgements

- [SadTalker](https://github.com/OpenTalker/SadTalker)
- [TinyLLaMA](https://huggingface.co/TinyLlama/TinyLlama-1.1B-Chat-v1.0)
- [Stable Diffusion](https://huggingface.co/runwayml/stable-diffusion-v1-5)
- [gTTS](https://pypi.org/project/gTTS/)

---

##  License

This project is intended for academic and research purposes only. Check each model/tool’s license individually for reuse.
