# XTTS-2-UI: A User Interface for XTTS-2 Text-Based Voice Cloning

This repository contains the essential code for cloning any voice using just text and a 10-second audio sample of the target voice. XTTS-2-UI is simple to setup and use. [Example Results 🔊](#examples)

Works in [16 languages](#language-support) and has in-built voice recording/uploading. 
Note: Don't expect EL level quality, it is not there yet. 

## Model 
The model used is `tts_models/multilingual/multi-dataset/xtts_v2`. For more details, refer to [Hugging Face - XTTS-v2](https://huggingface.co/coqui/XTTS-v2) and its specific version [XTTS-v2 Version 2.0.2](https://huggingface.co/coqui/XTTS-v2/tree/v2.0.2).

<h1 align="center">    
  <img src="demo_info/ui.png" width="100%"></a>  
</h1>

## Table of Contents

- [XTTS-2-UI: A User Interface for XTTS-2 Text-Based Voice Cloning](#xtts-2-ui-a-user-interface-for-xtts-2-text-based-voice-cloning)
  - [Model](#model)
  - [Table of Contents](#table-of-contents)
  - [Requirements](#requirements)
  - [Setup](#setup)
  - [Inference](#inference)
  - [Target Voices Dataset](#target-voices-dataset)
  - [Sample Audio Examples:](#sample-audio-examples)
  - [Language Support](#language-support)
  - [Notes](#notes)
  - [Credits](#credits)


## Requirements

 - Python 3.11 (eg. Python 3.11.9, tested)
 - Windows, Mac or Linux (Universal)

## Setup

To set up this project, follow these steps in a terminal:

1. **Clone the Repository**

    - Clone the repository to your local machine.
      ```bash
      git clone https://github.com/pbanuru/xtts2-ui.git
      cd xtts2-ui
      ```

2. **Create a Virtual Environment:**
   - Run the following command to create a Python virtual environment:
     ```bash
     python -m venv venv
     ```
   - Activate the virtual environment:
     - Windows:
       ```bash
       # cmd prompt
       venv\Scripts\activate
       ```
       or
       
       ```bash
       # git bash
       source venv/Scripts/activate
       ```
     - Linux/Mac:
       ```bash
       source venv/bin/activate
       ```

3. **Install PyTorch:**
   
   - If you have an Nvidia CUDA-Enabled GPU, choose the appropriate PyTorch installation command:
     - Before installing PyTorch, check your CUDA version by running:
       ```bash
       nvcc --version
       ```
     - For CUDA 12.1:
       ```bash
       pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
       ```
     - For CUDA 11.8:
       ```bash
       pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
       ```
   - If you don't have a CUDA-enabled GPU,:
     Follow the instructions on the [PyTorch website](https://pytorch.org/get-started/locally/) to install the appropriate version of PyTorch for your system.

4. **Install Other Required Packages:**
   - Install direct dependencies:
     ```bash
     pip install -r requirements.txt
     ```
   - Upgrade the TTS package to the latest version:
     ```bash
     pip install --upgrade TTS
     ```


     

After completing these steps, your setup should be complete and you can start using the project.

Models will be downloaded automatically upon first use.

Download paths:
- MacOS: `/Users/USR/Library/Application Support/tts/tts_models--multilingual--multi-dataset--xtts_v2`
- Windows: `C:\Users\ YOUR-USER-ACCOUNT \AppData\Local\tts\tts_models--multilingual--multi-dataset--xtts_v2`
- Linux: `/home/${USER}/.local/share/tts/tts_models--multilingual--multi-dataset--xtts_v2`



## Inference
To run the application:

```
python app.py
OR
streamlit run app2.py 
```
Or, You can also run from the terminal itself, by providing sample input texts on texts.json and generate multiple audios with multiple speakers, (you may need to adjust on appTerminal.py)
```
python appTerminal.py
```
On initial use, you will need to agree to the terms:

```
[XTTS] Loading XTTS...
 > tts_models/multilingual/multi-dataset/xtts_v2 has been updated, clearing model cache...
 > You must agree to the terms of service to use this model.
 | > Please see the terms of service at https://coqui.ai/cpml.txt
 | > "I have read, understood and agreed to the Terms and Conditions." - [y/n]
 | | >
 ```

Important: during your first generation, if you encounter an error:

```bash
Running on local URL:  http://127.0.0.1:7860

To create a public link, set `share=True` in `launch()`.
IMPORTANT: You are using gradio version 4.7.1, however version 4.44.1 is available, please upgrade.
--------
ERROR:    Exception in ASGI application
Traceback (most recent call last):
  File "/Users/USER/path/venv/lib/python3.11/site-packages/pydantic/type_adapter.py", line 271, in _init_core_attrs
    self.core_schema = _getattr_no_parents(self._type, '__pydantic_core_schema__')
                       ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/Users/USER/path/venv/lib/python3.11/site-packages/pydantic/type_adapter.py", line 55, in _getattr_no_parents
    raise AttributeError(attribute)
AttributeError: __pydantic_core_schema__

During handling of the above exception, another exception occurred:
...
```

Install a compatible version of gradio: 

```bash
pip install -U gradio==4.44.1

and relaunch the app.

```bash
python app.py
OR
streamlit run app2.py 
```

This solution comes from [Issue 258 on GitHub from jhj0517/Whisper-WebUI](https://github.com/jhj0517/Whisper-WebUI/issues/258#issuecomment-2333390291)

If your model is re-downloading each run, please consult [Issue 4723 on GitHub](https://github.com/oobabooga/text-generation-webui/issues/4723#issuecomment-1826120220).

## Target Voices Dataset
The dataset consists of a single folder named `targets`, pre-populated with several voices for testing purposes.

To add more voices (if you don't want to go through the GUI), create a 24KHz WAV file of approximately 10 seconds and place it under the `targets` folder. 
You can use yt-dlp to download a voice from YouTube for cloning:
```
yt-dlp -x --audio-format wav "https://www.youtube.com/watch?"
```


## Sample Audio Examples:

| Language | Audio Sample Link |
|----------|-------------------|
| English  | [▶️](demo_info/Rogger_sample_en.wav) |
| Russian  | [▶️](demo_info/Rogger_sample_ru.wav) |
| Arabic   | [▶️](demo_info/Rogger_sample_aa.wav) |

## Language Support
Arabic, Chinese, Czech, Dutch, English, French, German, Hungarian, Italian, Japanese[ (see setup)](#notes), Korean, Polish, Portuguese, Russian, Spanish, Turkish

## Notes
If you would like to select **Japanese** as the target language, you must install a dictionary.
```bash
# Lite version
pip install fugashi[unidic-lite]
```
or for more serious processing:
```bash
# Full version
pip install fugashi[unidic]
python -m unidic download
```
More details [here](https://github.com/polm/fugashi#installing-a-dictionary).


## Credits
1. Heavily based on https://github.com/kanttouchthis/text_generation_webui_xtts/ 
