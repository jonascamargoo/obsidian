
Encoder: processes the original text (e.g., German paragraph). Develops deep contextual undertanding of the text's meaning; Decoder: uses the deep understanding from the encoder. Generates new text in target language (e.g., English translation)


Once the text is tokenized, each token is assigned an initial dense vector representation. Dense semantic vector "first guess of meaning". This guesses are static, so every time we feed LLM the same token, it will be assigned with the same vector. Semantic and position vectors sent along together for processing

![[Pasted image 20250827100136.png]]

The token now enter the attention mechanism of the transformer. Each token essentially looks at every other token in the prompt and can see both their meaning and their position. Each token decides which other tokens it should pay the most attention to.

![[Pasted image 20250827100400.png]]
No exemplo "the brown dog sat next the red fox", a palavra dog vai prestar atenção 70 % em brown e 20 em sat, os outros 10% são distribuídos ao pelos outros tokens

Explique a relação disso com attention head.  Explique o caminho até os refined embeddings.

"To generate the next token, the model repeats the entire process from scratch. This loop continues until it hits either token limit or end of completation token"

Why RAGs works
1. LLMs can deeply understand information added to prompts through: Attention mechanism processing; World knowledge in feed forward layers. 
2. Inherent randomness remains: LLMs may randomly ignore injected information; Need to control randomness; Must confirm LLM grounds answers in retrived information
3. Computation expense: Generating single tokens requires extensive processing; Costs grow with prompt/completion length; Each token must examine all others for context; Most RAG system costs come from running transformers