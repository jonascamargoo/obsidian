---
tipo: conceito
area: IAs
tags:
- ia/rag
criada: '2025-08-27'
---

Greedy decoding
* sampling strategy that always select the token with the highest probability at each step of the text generation
* deterministic: if I feed LLM with the same prompt, it will always generate the same prompt response;
* generic-sounding text
* can get stuck in a loop:...


![[Pasted image 20250827105924.png]]


Temperature
* Parameter that changes the shape of the distribuition genereted by the LLM
* Setting temperature as 0 forces the model to perform greedy decoding. Set as 0.5 make more spiky distribuition and set as 1 is the original distribution

Advanced token sampling

Top-K -> picks only from the k most likely tokens, ignoring the rest. Top-K of 5 means only the 5 most likely tokens can be chosen;
Top-P -> Picks from tokens whose cumulative probability is bellow some threshold. Top-P of 85% includes tokens until their probability is above 85%
Top-K vs Top-P: top-p is more dynamic than top-k; top-k always includes the same number of tokens regardless of the shape of the distribuition; top-P includes more or fewer tokens depending on how "certain" the model is


Token specific Strategies

* Repetition Penalties: reduce the probability of already used tokens, discouraginf repetition
* Logit Biases: allow direct manipulation of token probabilities by adding or subtracting values from the model's raw calculated probabilities. Biases can filter profanity, boost categoriesin a classifier LLM



![[Pasted image 20250827111956.png]]

Using sampling strategies

* Set temperature at top-p that fits your application's need
* Code or factual domain -> low temperature and top-P
* Creative domain -> explore higher temperature and top-p
* Then add repetition penalties, logit biases, etc. as need arise


