# LATS (Language Agent Tree Search) Implementation for Ollama
LATS (Language Agent Tree Framework) is a MAG framework that originates from https://arxiv.org/abs/2310.04406 . It builds on ToT (Tree of Thoughts) by incorporating a MCTS (Monte Carlo Tree Selection). This tree works differently from BFS or DFS by not solely being bound to the score of a node but also the visits. It selects nodes by looking at their upper confidence bounds which aims to strike a balance between exploration and node score values.

The original paper implementation is here (Though I discovered it after I did this one.): https://github.com/andyz245/LanguageAgentTreeSearch

Here are the sources I used (Except Langchain documentation.):
Implementation of LATS: https://github.com/langchain-ai/langgraph/blob/main/examples/lats/lats.ipynb
Calling tools in Langchain: https://medium.com/pythoneers/power-up-ollama-chatbots-with-tools-113ed8229a7a

A primitive and an inefficient implementation of LATS for usage alongside Ollama. It can possibly be extended to support every API out there.

##The Reason

The implementation I used as a source is very robust and is very explanative. However, it is only usable for OpenAI API. This is due to how bind_tools works. Both of them work fundementally different in how they call their tools. There exists a solution in the form of Langchain called OllamaFunctions but I found it to be incomplete. Hence I developed this expendable framework to support different APIs.

This implementation is a bit incomplete and inefficient.

Things to look for:
- There exists no leaf parallelization. (That is each node is done once by once while we can parallelize in expansion doing in batch. This is easy to implement.)
- I couldn't get OpenAI to work with it however the fix should be easy. (The reason I found is due to message roles.)