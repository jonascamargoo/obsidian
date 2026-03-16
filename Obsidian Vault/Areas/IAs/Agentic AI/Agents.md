# **Tipos de Agentes de IA**

Os agentes de inteligência artificial podem ser classificados em diferentes categorias com base em sua estrutura e capacidade de tomada de decisão. A seguir, descrevemos os principais tipos:

## **1. Reactive Agents (Agentes Reativos)**

Agentes sem memória ou estado, que tomam decisões baseadas apenas no input recebido no momento. Eles não armazenam informações sobre interações passadas e seguem regras pré-definidas para responder aos estímulos.

- **Exemplo**: Sistemas de recomendação simples baseados em regras, como chatbots que seguem scripts fixos.

## **2. Deliberative Agents (Agentes Deliberativos)**

Agentes que realizam um mapeamento antes da ação, construindo um modelo interno do ambiente para tomar decisões mais elaboradas. Eles analisam diferentes opções antes de agir.

- **Exemplo**: Planejadores automatizados em jogos de estratégia, assistentes virtuais que consideram contexto antes de responder.

## **3. Hybrid Agents (Agentes Híbridos)**

Agentes que combinam características de agentes reativos e deliberativos, equilibrando respostas rápidas com planejamento estruturado.

- **Exemplo**: Sistemas de navegação autônoma que usam regras fixas para evitar obstáculos, mas também planejam rotas estratégicas.

## **4. Learning Agents (Agentes de Aprendizado)**

Agentes que podem melhorar seu desempenho ao longo do tempo com base em experiência e dados coletados. Eles ajustam suas respostas com técnicas de aprendizado de máquina.

- **Exemplo**: Modelos de IA baseados em deep learning, como assistentes de voz que aprendem preferências do usuário.


# **Arquitetura dos Agentes na Prática**

Na implementação prática, um agente de IA segue um fluxo geral de funcionamento:

1. **Perception (Percepção)** – O agente recebe inputs do usuário ou do ambiente.
2. **Decision-Making (Tomada de Decisão)** – O agente processa os inputs e define uma ação apropriada.
3. **Execution (Execução)** – A resposta do agente é gerada e enviada para o usuário.

![[Pasted image 20250314131611.png]]

Um método rudimentar de simular a lógica de um agente é através de _function calling_ ou _json calling_, onde um prompt é estruturado dentro de um JSON para definir a lógica de funcionamento do agente.


```python
import openai

def classify_user_intent(user_query: str, openai_api_key: str) -> str:
    """
    Uses OpenAI's API to classify whether the user intends to generate a PDF or send an email.
    
    :param user_query: The user's input text.
    :param openai_api_key: The OpenAI API key.
    :return: Either 'generate_pdf', 'send_email', or 'unknown'.
    """
    prompt = (
        "Analyze the following user query and determine the intent. "
        "If the user wants to generate a PDF, return exactly 'generate_pdf'. "
        "If the user wants to send an email, return exactly 'send_email'. "
        "If the intent is unclear, return 'unknown'. "
        f"\nUser query: {user_query}\nIntent:"
    )
    
    response = openai.ChatCompletion.create(
        model="gpt-4",
        messages=[
            {"role": "system", "content": "You are an AI assistant that classifies user intent."},
            {"role": "user", "content": prompt}
        ],
        temperature=0
    )
    
    intent = response["choices"][0]["message"]["content"].strip()
    
    if intent in {"generate_pdf", "send_email"}:
        return intent
    return "unknown"

# Example usage:
# api_key = "your_openai_api_key"
# user_query = "Can you create a PDF file for me?"
# print(classify_user_intent(user_query, api_key))
```


MCP Servers... Continua no próximo vídeo do galego