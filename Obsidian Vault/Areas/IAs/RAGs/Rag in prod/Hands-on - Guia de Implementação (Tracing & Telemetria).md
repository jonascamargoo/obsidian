**Data:** 23/02/2026 **Tópico:** #Python #OpenTelemetry #Weaviate #Phoenix #Coding

---

## 1. Fundamentos de Telemetria (OpenTelemetry)

Para instrumentar um sistema, utilizamos o padrão **OpenTelemetry (OTel)**, que é a base do Arize Phoenix.

- **Span:** A menor unidade de trabalho (ex: uma busca no banco, uma chamada de API).
    
- **Trace:** O conjunto de spans que formam o fluxo completo de uma requisição.
    

### Configuração Inicial do Tracer

Python

```
from phoenix.otel import register
from opentelemetry.trace import Status, StatusCode

# Registro do projeto no Phoenix com Auto-Instrumentação para OpenAI
tracer_provider = register(
    project_name="rag-production-pipeline",
    endpoint="http://127.0.0.1:6006/v1/traces",
    auto_instrument=True # Rastreia chamadas OpenAI/TogetherAI automaticamente
)

tracer = tracer_provider.get_tracer(__name__)
```

---

## 2. Padrões de Instrumentação

### A. Instrumentação Manual (Granular)

Ideal para o componente de **Retriever**, onde você quer logar os metadados dos documentos recuperados.

Python

```
def retrieve(query_text, limit=5):
    # Definimos o 'kind' como retriever para o Phoenix categorizar corretamente no UI
    with tracer.start_as_current_span("query_weaviate", openinference_span_kind="retriever") as span:
        span.set_input(query_text) # Helper do Phoenix para registrar o input
        
        results = collection.query.near_text(query=query_text, limit=limit)

        # Logando atributos específicos de cada documento recuperado no Span
        for i, doc in enumerate(results.objects):
            span.set_attribute(f"retrieval.documents.{i}.document.id", str(doc.uuid))
            span.set_attribute(f"retrieval.documents.{i}.document.content", str(doc.properties))
            
        return results
```

### B. Instrumentação via Decoradores (`@tracer.chain`)

Para funções de processamento lógico (formatação, aumento de prompt), o uso de decoradores simplifica o código e mantém o trace limpo.

Python

```
@tracer.chain
def format_context(results):
    context = ""
    for item in results.objects:
        context += f"Question: {item.properties['question']}\n"
        context += f"Answer: {item.properties['answer']}\n"
    return context

@tracer.chain
def rag_pipeline(query):
    # O trace seguirá o fluxo de execução dessas funções automaticamente
    docs = retrieve(query)
    context = format_context(docs)
    prompt = create_prompt(query, context)
    return query_llm(prompt)
```

---

## 3. Integração com Vector DB (Weaviate)

No laboratório, a integração demonstra como o **Phoenix UI** mapeia a busca semântica.

1. **Conexão:** O cliente Weaviate realiza a busca `near_text`.
    
2. **Captura:** O tracer captura os `properties` do objeto (pergunta/resposta do FAQ).
    
3. **Visualização:** No dashboard do Phoenix, é possível ver o tempo exato que o Weaviate levou para retornar os vizinhos mais próximos vs. o tempo de geração do LLM.
    

---

## 🛠️ Checklist de Implementação para o Engenheiro

> [!CHECKLIST] **O que garantir no seu código:**
> 
> - [ ] **Unique Project Names:** Use `int(time.time())` no nome do projeto em ambientes de teste para evitar conflitos de IDs no Phoenix.
>     
> - [ ] **OpenInference Semantics:** Sempre defina `openinference_span_kind="retriever"` ou `"llm"`. Isso habilita visualizações especializadas no Phoenix (como visualização de chunks).
>     
> - [ ] **Error Handling:** Use `span.set_status(Status(StatusCode.ERROR, str(e)))` dentro de blocos `try/except` para que falhas apareçam em vermelho no dashboard de monitoramento.
>     
> - [ ] **Auto-instrumentation:** Se estiver usando bibliotecas compatíveis com OpenAI, ative o `auto_instrument=True` para poupar centenas de linhas de código de tracing manual.
>