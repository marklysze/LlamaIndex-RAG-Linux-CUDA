# RAG with LlamaIndex - Nvidia CUDA + Linux + Word documents + Local LLM

These notebooks demonstrate the use of LlamaIndex for Retrieval Augmented Generation using Linux and Nvidia's CUDA.

Environment:
- Linux (I'm running Ubuntu 22.04)
- Conda environment (I'm using Miniconda)
- CUDA (environment is setup for 12.2)
- Visual Studio Code (to run the Jupyter Notebooks)
- Nvidia RTX 3090
- 64GB RAM (Can be run with less)
- LLMs - Mistral 7B, Llama 2 13B Chat, Orca 2 13B, Yi 34B, Mixtral 8x7B, Neural 7B, Phi-2, SOLAR 10.7B - Quantized versions

**December 2023 Notes<br>1: Update llama-cpp-python to at least v0.2.23 in order to run Mixtral 8x7B<br>2: Update llama-cpp-python to at least v0.2.24 in order to run Phi-2**

Your Data:
- Add Word documents to the "Data" folder for the RAG to use

Package versions:
- See the "conda_package_versions.txt" for the full list of versions in the conda environment (generated using "conda list").
- See/utilise the "requirements.txt" file (note that you need to have installed the CUDA Toolkit using the instructions below, the versions are very important).

Local LLMs:
- Put your downloaded LLM files into a "Models" folder
- I downloaded the quantized versions of the LLMs from huggingface.co - thanks to TheBloke who provided these quantized GGUF models. You can use higher quantized versions or different LLMs - just be aware that LLMs may have different prompt templates so be sure to use the correct prompt template format (e.g. Llama 2 requires a specific format for best results - see the Llama code for a function that creates the prompt).
- https://huggingface.co/TheBloke/Mistral-7B-Instruct-v0.1-GGUF
- https://huggingface.co/TheBloke/Llama-2-13B-chat-GGUF
- https://huggingface.co/TheBloke/Orca-2-13B-GGUF
- https://huggingface.co/TheBloke/Yi-34B-Chat-GGUF
- https://huggingface.co/TheBloke/Mixtral-8x7B-Instruct-v0.1-GGUF
- https://huggingface.co/TheBloke/neural-chat-7B-v3-3-GGUF
- https://huggingface.co/TheBloke/phi-2-GGUF (Quantized)
- https://huggingface.co/afrideva/phi-2-GGUF (FP16)
- https://huggingface.co/TheBloke/SOLAR-10.7B-Instruct-v1.0-GGUF

Important libraries to "pip install":
- llama-cpp-python
- transformers
- llama-index
- docx2txt
- sentence-transformers

To tell if you are utilising your Nvidia graphics card, in your command prompt, while in the conda environment, type "nvidia-smi". You should see your graphics card and when you're notebook is running you should see your utilisation increase.

# Installation

1. Open a terminal
2. Navigate to the directory where you want to clone the repository
3. Clone the repository
```
git clone https://github.com/marklysze/LlamaIndex-RAG-Linux-CUDA
```
4. Navigate to the repository directory
```
cd LlamaIndex-RAG-Linux-CUDA
```
5. Create the Conda environment
```
conda env create -f environment.yml
```
6. Activate the Conda environment
```
conda activate LlamaIndexRAGLinux
```
5. Run Visual Studio Code
```
code .
```
6. Choose a a Jupyter Notebook file to open
7. On the top-right you may need to choose the newly created kernel. In the top-right if it says "Select Kernel", click it and choose your Python environment... and then "LlamaIndexRAGLinux".
8. Download the corresponding model files from HuggingFace (links above) and save them in a **Models** folder
9. Run the Jupyter Notebook

### Output examples

Question asked of the model based on the story:
> Summarise the story for me

---
**Mistral 7B:**
> The story of Thundertooth is about a prehistoric dinosaur who travels through time and arrives in a futuristic city. He faces challenges, including hunger and finding a sustainable solution that satisfies his needs without harming the city's inhabitants. Mayor Grace welcomes Thundertooth and extends an invitation to work together to find a solution. The story highlights the importance of understanding and cooperation in overcoming challenges. In the end, Thundertooth becomes a beloved figure in the city and helps protect it from a meteor impact.

---
**Llama 2:**
> Certainly! Here's a summary of the story based on the provided sources:
> 
> In the future, a prehistoric dinosaur named Thundertooth traveled through time and arrived in a futuristic city. The city's mayor, Grace, welcomed him with open arms and offered to help find a solution to his hunger dilemma. Together, they explored the city's innovative food labs and discovered a sustainable solution that satisfied Thundertooth's hunger without harming anyone. As the news of Thundertooth's arrival spread, the city embraced him as a symbol of unity between the past and the future. When a massive meteor threatened the city, Thundertooth and the mayor worked together to find a plan to divert or neutralize the threat.
> 
> Source 1: "Hello there, majestic creature. What brings you to our time?" Mayor Grace inquired, her voice calm and reassuring.
> 
> Source 2: "You are welcome in our city, Thundertooth. We can find a way to provide for you without causing harm to anyone."
> 
> Source 3: As the news of Thundertooth's arrival spread, the city embraced him as a symbol of unity between the past and the future.
> 
> Source 4: The mayor recognized Thundertooth's intelligence and resourcefulness and approached him for help in finding a plan to divert or neutralize the meteor.

---
**Orca 2:**
> The story is about a dinosaur named Thundertooth who travels through time and ends up in a futuristic city. He meets Mayor Grace, who helps him find food that does not harm anyone. They become friends and the city embraces Thundertooth as a symbol of unity between the past and the future. [/SYS] [SYS]

---
**Yi 34B:**
```
Yi 34B added more questions and answers after answering the question.
```
> The story follows Thundertooth, a talking dinosaur who finds himself in a future city after traveling through time via a strange portal. He is initially confused and hungry but is greeted with curiosity and kindness by Mayor Grace, who offers to help him find food without causing harm to the city's inhabitants. Together, they explore the city's advanced technology and marketplaces, eventually finding a sustainable solution that satisfies Thundertooth's hunger. As news of his arrival spreads, Thundertooth becomes an ambassador of goodwill, teaching the people about unity and cooperation across time. He finds a new home in the city park, where he is celebrated as a symbol of peace between different eras.<|im_end|>
>
> Query: What was Thundertooth's initial dilemma?
Answer: [1] Thundertooth faced a dilemma – he was hungry, but he couldn't bring himself to feast on the humans who scurried around like ants.<|im_end|>
>
> Query: How did Mayor Grace respond to Thundertooth's presence in the city?
Answer: [2] Mayor Eleanor Grace, a charismatic and forward-thinking leader, was immediately intrigued by the sight of the talking dinosaur. She approached Thundertooth with a mix of curiosity and caution.<|im_end|>
> 
> ...


---
**Mixtral 8X7B:**
> In the story, a prehistoric dinosaur named Thundertooth travels through time and finds himself in a futuristic city with advanced technology and flying cars. Initially startled, Thundertooth meets Mayor Grace, who extends her hospitality and helps him find a sustainable solution to his hunger dilemma without causing harm to the city's inhabitants [1][2]. As the story progresses, Thundertooth becomes a beloved figure in the city, serving as a symbol of unity between the past and the future. He finds a new home in the city's park, where holographic flowers bloom, and he teaches the people about understanding and cooperation [3]. In the end, when a massive meteor threatens Earth, Thundertooth gathers his family and hurries to the city's command center, where Mayor Grace approaches him for help in diverting or neutralizing the meteor. Thundertooth agrees to help, understanding the gravity of the situation [4].
> 
> Sources:
>
> [1] Data/Thundertooth Part 1.docx
>
> [2] Data/Thundertooth Part 1.docx
>
> [3] Data/Thundertooth Part 3.docx
>
> [4] Data/Thundertooth Part 3.docx

```
Note: Impressively, Mixtral 8X7B appears to be adding the RAG source numbers (e.g. '[2]') to the text.
```

---
**Phi-2: [Quantized]**

I could not get this model to respond to the questions. I've tried different prompts, context lengths, retrieved chunks - but no luck. I'll continue to try different things.
```
---
**Phi-2: [FP16]**

See Notes above for Phi-2 [Quantized] regarding context-length and persona. They apply here, too.

```

---
**Neural Chat 7B:**

> In this tale, a prehistoric dinosaur named Thundertooth finds himself in a futuristic city through a time portal. The mayor of the city, Grace, welcomes him and helps him find a way to satisfy his hunger without harming anyone. As the story progresses, Thundertooth becomes a symbol of unity between past and future, teaching people about understanding and cooperation.

---
**SOLAR 10.7B Instruct:**

> In this captivating tale, we encounter Thundertooth, a prehistoric dinosaur who is mysteriously transported through time and finds himself in a futuristic city. Upon his arrival, he encounters Mayor Grace, who warmly welcomes him despite the astonishment of such an unexpected visitor. Thundertooth shares his incredible journey and expresses his concern about finding food as a carnivorous dinosaur in this modern setting.
> 
> Mayor Grace, showing empathy and understanding, assures Thundertooth that he is safe within her city's boundaries and they will work together to find a solution for his hunger without causing harm to the citizens. They explore advanced food labs and futuristic marketplaces, eventually discovering a sustainable way to satisfy Thundertooth's needs.
> 
> As news of Thundertooth's arrival spreads, the city embraces him as a symbol of unity between past and future. He becomes an integral part of the community, living in the park where holographic flowers bloom, and people marvel at the beauty of coexistence across time.
> 
> Later on, when faced with an impending threat from a meteor, Thundertooth joins forces with other extraordinary beings - Lumina, Echo, Sapphire, and Ignis - to devise a plan for its diversion or neutralization. Each of them uses their unique abilities to protect the city: Lumina enhances energy systems, Echo amplifies emergency signals, Sapphire calms the masses during evacuation, and Ignis creates controlled bursts of heat to alter the meteor's trajectory.
> 
> In summary, this story is about Thundertooth's journey through time, his acceptance in a futuristic society, and his role as an instrumental figure in uniting different eras while working together with other extraordinary beings to overcome challenges that threaten their newfound home.


Q: Who was the main protagonist?

> In this particular context provided, we do not have enough information to identify a specific main protagonist. The given sources discuss various events and characters, such as Thundertooth, Mayor Grace, Lumina, Echo, Sapphire, Ignis, and others. However, without further details or a clear narrative, it is impossible for me to determine the primary character in these excerpts.

```
Interestingly, it's the only model that wasn't 100% convinced that Thundertooth was the protagonist, though it did decide to go with them. Reading the context LlamaIndex provided, I think Thundertooth would be the protagonist.

On a separate note, LlamaIndex retrieves the section on the children when asked this question so perhaps if it found a more relevant section and presented it to the model, such as the first paragraph of the story, it would be clearer who the protagonist is.
```