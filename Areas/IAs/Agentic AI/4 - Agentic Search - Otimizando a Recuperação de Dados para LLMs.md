---
tipo: aula
area: IAs
tags:
- ia/agentes
criada: '2026-04-20'
---

## 1. O Problema: Modelos Paramétricos vs. Dados Dinâmicos

O paradigma _Zero-Shot_ padrão de LLMs sofre de um gargalo fundamental: os pesos do modelo são estáticos (limitados ao _cutoff_ de treinamento). O uso de motores de busca é a solução clássica para aterramento (_grounding_) temporal (ex: "Qual foi o placar do jogo de ontem?").

No entanto, há uma diferença arquitetural massiva entre uma interface de busca projetada para humanos (ex: Google Search) e uma projetada para máquinas/agentes (Agentic Search).

---

## 2. Busca Regular vs. Busca Agentic

### A Abordagem de Busca Clássica (Humana)

Quando utilizamos motores tradicionais (como demonstrado com a API do DuckDuckGo), o fluxo é altamente ineficiente para um pipeline de agente:

1. **Input:** A query retorna uma lista de links (URLs).
    
2. **Scraping:** O agente (ou nosso código Python usando `BeautifulSoup`) precisa acessar a URL.
    
3. **Parsing de HTML:** O agente recebe a estrutura do DOM (centenas de milhares de caracteres contendo tags, scripts, CSS e anúncios).
    
4. **Extração de Texto:** Precisamos aplicar lógica arbitrária (ex: buscar apenas tags `h1`, `p`) e expressões regulares para limpar o payload.
    
5. **LLM Inference:** O texto limpo (mas ainda longo e desestruturado) é passado para a janela de contexto do LLM.
    

**Gargalos para o Agente:** Altíssima latência (múltiplos _round-trips_ HTTP), poluição de tokens (custo alto de injeção de contexto) e risco de falhas de _parsing_ devido à volatilidade do layout dos sites.

![[Pasted image 20260419100051.png]]

### A Abordagem Agentic Search (Ex: Tavily)

Ferramentas de _Agentic Search_ invertem o paradigma. A complexidade do roteamento, _scraping_ e vetorização é movida para o lado do provedor da ferramenta, abstraindo o processo para o LLM.

**O Fluxo Interno de uma API Agentic:**

1. **Roteamento Dinâmico (Routing):** A ferramenta identifica o domínio da query (ex: percebe que a query é sobre clima e roteia a busca para uma Weather API em vez de fazer scraping genérico na web).
    
2. **Chunking e Vector Search (Retrieval):** Se a busca for na web, a ferramenta faz o download do conteúdo, divide-o em _chunks_, realiza uma busca vetorial interna (K-NN) usando a sub-query e retém apenas os parágrafos relevantes.
    
3. **Filtragem de Relevância (Scoring):** A ferramenta pontua os chunks extraídos e descarta "ruído" algorítmico.
    
4. **Output Estruturado:** O retorno final não é um DOM HTML ou uma URL, mas um `JSON` denso, limpo e altamente previsível, contendo apenas a resposta explícita e suas fontes (URLs/Citações).
    
![[Pasted image 20260419102022.png]]
---

## 3. Implementação e Análise de Output

### Teste de Falha (Busca Regular via DuckDuckGo + BeautifulSoup)

A demonstração expõe como o payload bruto do scraping (mesmo limpando `\s+` e focando em headers) gera um bloco de texto com ruídos de interface (ex: _"The Weather Channel... Today... Hourly..."_). O LLM precisaria gastar processamento computacional apenas para encontrar o dado útil nesse bloco.

### Teste de Sucesso (Agentic Search via Tavily)

O uso da API da Tavily (`client.search(query)`) simplifica a infraestrutura:

```Python
result = client.search("what is the current weather in San Francisco?", max_results=1)
data = result["results"][0]["content"]
```

**O Output (A Perspectiva da Máquina):** A resposta retorna um dicionário JSON estrito (ex: `{'temp': 65, 'condition': 'partly cloudy', 'humidity': '60%'}`).

- Para um usuário humano, ler JSON puro no terminal é visualmente pobre (preferimos o Widget renderizado do Google).
    
- Para um agente (LLM), o JSON é o **ambiente perfeito**. Ele extrai o valor de `temp` sem ambiguidades, minimizando o uso de tokens e eliminando o risco de alucinar informações de anúncios que poderiam ter sido raspados.

## Notebook

```python
# Lesson 3: Agentic Search[](https://s172-29-117-238p8888.lab-aws-production.deeplearning.ai/notebooks/L3/Lesson_3_Student.ipynb#Lesson-3:-Agentic-Search)

# libraries

from dotenv import load_dotenv

import os

from tavily import TavilyClient

​

# load environment variables from .env file

_ = load_dotenv()

​

# connect

client = TavilyClient(api_key=os.environ.get("TAVILY_API_KEY"))

# run search

result = client.search("What is in Nvidia's new Blackwell GPU?",

                       include_answer=True)

​

# print the answer

result["answer"]

​

## Regular search[](https://s172-29-117-238p8888.lab-aws-production.deeplearning.ai/notebooks/L3/Lesson_3_Student.ipynb#Regular-search)

# choose location (try to change to your own city!)

​

city = "San Francisco"

​

query = f"""

    what is the current weather in {city}?

    Should I travel there today?

    "weather.com"

"""

> Note: search was modified to return expected results in the event of an exception. High volumes of student traffic sometimes cause rate limit exceptions.

import requests

from bs4 import BeautifulSoup

from duckduckgo_search import DDGS

import re

​

ddg = DDGS()

​

def search(query, max_results=6):

    try:

        results = ddg.text(query, max_results=max_results)

        return [i["href"] for i in results]

    except Exception as e:

        print(f"returning previous results due to exception reaching ddg.")

        results = [ # cover case where DDG rate limits due to high deeplearning.ai volume

            "https://weather.com/weather/today/l/USCA0987:1:US",

            "https://weather.com/weather/hourbyhour/l/54f9d8baac32496f6b5497b4bf7a277c3e2e6cc5625de69680e6169e7e38e9a8",

        ]

        return results  

​

​

for i in search(query):

    print(i)

def scrape_weather_info(url):

    """Scrape content from the given URL"""

    if not url:

        return "Weather information could not be found."

    # fetch data

    headers = {'User-Agent': 'Mozilla/5.0'}

    response = requests.get(url, headers=headers)

    if response.status_code != 200:

        return "Failed to retrieve the webpage."

​

    # parse result

    soup = BeautifulSoup(response.text, 'html.parser')

    return soup

​

> Note: This produces a long output, you may want to right click and clear the cell output after you look at it briefly to avoid scrolling past it.

# use DuckDuckGo to find websites and take the first result

url = search(query)[0]

​

# scrape first wesbsite

soup = scrape_weather_info(url)

​

print(f"Website: {url}\n\n")

print(str(soup.body)[:50000]) # limit long outputs

# extract text

weather_data = []

for tag in soup.find_all(['h1', 'h2', 'h3', 'p']):

    text = tag.get_text(" ", strip=True)

    weather_data.append(text)

​

# combine all elements into a single string

weather_data = "\n".join(weather_data)

​

# remove all spaces from the combined text

weather_data = re.sub(r'\s+', ' ', weather_data)

print(f"Website: {url}\n\n")

print(weather_data)

## Agentic Search[](https://s172-29-117-238p8888.lab-aws-production.deeplearning.ai/notebooks/L3/Lesson_3_Student.ipynb#Agentic-Search)

# run search

result = client.search(query, max_results=1)

​

# print first result

data = result["results"][0]["content"]

​

print(data)

import json

from pygments import highlight, lexers, formatters

​

# parse JSON

parsed_json = json.loads(data.replace("'", '"'))

​

# pretty print JSON with syntax highlighting

formatted_json = json.dumps(parsed_json, indent=4)

colorful_json = highlight(formatted_json,

                          lexers.JsonLexer(),

                          formatters.TerminalFormatter())

​

print(colorful_json)
```


![](https://s172-29-117-238p8888.lab-aws-production.deeplearning.ai/notebooks/L3/google_sample.png)