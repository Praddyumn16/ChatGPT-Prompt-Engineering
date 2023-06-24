# ChatGPT-Prompt-Engineering
This repo is created as a place for all the important notes and points that I'll be learning from this short course: https://www.deeplearning.ai/short-courses/chatgpt-prompt-engineering-for-developers/


There are mainly 2 types of LLM's:

1. Base LLM - which predicts next word to follow based on some text training data.
But it fails on questions like "What is the capital of France?" for which it might respond: "What is the France's largest city" because articles on the internet could possibly be a list of questions related to France.

2. Instruction tuned LLM - Here, we start with a Base LLM and further fine tune it based on some inputs and outputs which are instructions and good attempt to follow those instructions. 
Then, we further refine it based on RLHF (Reinforcement Learning with Human Feedback)
