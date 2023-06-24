# ChatGPT-Prompt-Engineering
This repo is created as a place for all the important notes and points that I'll be learning from this short course: https://www.deeplearning.ai/short-courses/chatgpt-prompt-engineering-for-developers/

## Introduction
There are mainly 2 types of LLM's:

**1. Base LLM** - which predicts next word to follow based on some text training data.
But it fails on questions like "What is the capital of France?" for which it might respond: "What is the France's largest city" because articles on the internet could possibly be a list of questions related to France.

**2. Instruction tuned LLM** - Here, we start with a Base LLM and further fine tune it based on some inputs and outputs which are instructions and good attempt to follow those instructions. Then, we further refine it based on RLHF (Reinforcement Learning with Human Feedback)

For example, if you say: "Write me something about Alan Turing", it would be better if you specify:
- whether you want to know about his personal or professional life
- what should be the tone of the text, whether it's being written by a friend or a professional reporter
- whether there's any text which they should read in advance to get an idea before writing this text

**Usage of OpenAI API:** There are mainly 3 roles for an object - **system**, **user** and **assistant**. Typically, a conversation is formatted with a system message first, followed by alternating user and assistant messages.<br/>
The system role help you set the tone of responses that you want to receive.

```python
import openai

openai.ChatCompletion.create(
  model="gpt-3.5-turbo",
  messages=[
        {"role": "system", "content": "You are a helpful assistant."},
        {"role": "user", "content": "Who won the world series in 2020?"},
        {"role": "assistant", "content": "The Los Angeles Dodgers won the World Series in 2020."},
        {"role": "user", "content": "Where was it played?"}
    ]
)
```

## Guidelines

There are mainly 2 guidelines for prompting.

1. Write clear and specific instructions:
   - clear != short
   - use delimeters to clearly indicate distinct parts of input: they can be anything like: ```, """, < >, tags. This helps to eliminate prompt injection. For example, in the right side image, because we have specified the delimeter, the model knows to summarize the instruction within the triple braces, rather than following the instruction itself.
     Prompt             |  Prompt injection eliminated
     :-------------------------:|:-------------------------:
     ![image](https://github.com/Praddyumn16/ChatGPT-Prompt-Engineering/assets/53634655/fa1820ba-e5f6-41bd-a03d-b6f923e499fe) | ![image](https://github.com/Praddyumn16/ChatGPT-Prompt-Engineering/assets/53634655/e2515261-7a3c-4384-952d-bf2fb235353a)

   - ask for structured output: in JSON or HTML. For example,
     Prompt             |  Output
     :-------------------------:|:-------------------------:
     ![image](https://github.com/Praddyumn16/ChatGPT-Prompt-Engineering/assets/53634655/9291abda-95ef-4b8a-affb-de7917038421) | ![image](https://github.com/Praddyumn16/ChatGPT-Prompt-Engineering/assets/53634655/2c337936-45af-452d-a1a2-dd68ffe26cdc)

   - ask the model to check whether conditions are satisfied. For example,
     Prompt             |  Output
     :-------------------------:|:-------------------------:
      ![image](https://github.com/Praddyumn16/ChatGPT-Prompt-Engineering/assets/53634655/88cde8af-2afe-41e3-8baa-f12d906c368d) | ![image](https://github.com/Praddyumn16/ChatGPT-Prompt-Engineering/assets/53634655/72710c9e-cf3d-4361-8ea1-9b9d8404fb11)
     ![image](https://github.com/Praddyumn16/ChatGPT-Prompt-Engineering/assets/53634655/80e8a9b5-ae05-4eb7-a826-922e96bca581) | ![image](https://github.com/Praddyumn16/ChatGPT-Prompt-Engineering/assets/53634655/7f08c974-e517-48d5-9e44-3cf093b332f8)

   - few shot prompting: it means providing examples of successful execution of the tasks that you want to be performed before actually asking the model to perform it. For example,
     Prompt | Output
     :-------------------------:|:-------------------------:
     ![image](https://github.com/Praddyumn16/ChatGPT-Prompt-Engineering/assets/53634655/1b91e584-7a80-4f2a-99f3-3741e69c3c63) | ![image](https://github.com/Praddyumn16/ChatGPT-Prompt-Engineering/assets/53634655/667158e7-812b-40e5-91ca-ffb9d085ef3b)


2. Give the model time to "think":
   - Specify the steps required to complete a task and maybe also specify the output format
     Prompt | Output
     :--:|:--:
     | ![image](https://github.com/Praddyumn16/ChatGPT-Prompt-Engineering/assets/53634655/e4850505-d771-4e6f-b3cc-3fd3f4658f0d) | ![image](https://github.com/Praddyumn16/ChatGPT-Prompt-Engineering/assets/53634655/bb01e616-8aea-4a41-8393-b2f8cc14d407)
     | ![image](https://github.com/Praddyumn16/ChatGPT-Prompt-Engineering/assets/53634655/c5e65b76-bdc5-44b8-8dd9-4589f39e4116) | ![image](https://github.com/Praddyumn16/ChatGPT-Prompt-Engineering/assets/53634655/8f94a9e2-1266-4a39-b977-3fee8e389d71)

   - Instruct the model to work out its own solution before rushing to a conclusion. For example, in the 1st prompt, the model says the output is correct when it is actually not. We can fix this by instructing the model to work out its own solution first as in the 2nd prompt.
     Prompt | Output
     :--:|:--:
     | ![image](https://github.com/Praddyumn16/ChatGPT-Prompt-Engineering/assets/53634655/2e20a1b8-f6c7-4b0f-8312-fac2ac57fc71) | ![image](https://github.com/Praddyumn16/ChatGPT-Prompt-Engineering/assets/53634655/a6db708e-e458-4a60-85f0-5a3e0281a6a1)
     | ![image](https://github.com/Praddyumn16/ChatGPT-Prompt-Engineering/assets/53634655/f33bcbee-e743-4200-9cbc-30f631acf9bd) | ![image](https://github.com/Praddyumn16/ChatGPT-Prompt-Engineering/assets/53634655/fd34b270-8336-43c5-ab9f-393b664c62a4)


At last, we can reduce the hallucinations made by the model (an answer that looks realistic but is actually not) by asking the model to first extract some relevant information from the text and then use that relevant information only to answer questions.


 






