
## Engenharia de Tensores: Manipulação, Formatos e Tipagem

A maioria dos erros críticos em PyTorch não ocorre devido à lógica matemática do modelo, mas sim devido à manipulação incorreta de tensores (dimensões incompatíveis ou tipos de dados errados). Este guia estabelece os fundamentos para operar a estrutura de dados central do Deep Learning.

## 1. Anatomia Dimensional (Shapes)

A propriedade mais crítica de um tensor é o seu formato (`shape`). É a primeira coisa a verificar durante a depuração.

Ao inspecionar um tensor de entrada típico::

```python
print(distances.shape)
# Saída: torch.Size([6, 1])
```

Isso representa uma matriz $X \in \mathbb{R}^{N \times D}$, onde:

1. **Dimensão 0 ($N$ - Batch Size):** O número de amostras processadas simultaneamente (neste caso, 6 registros).
    
2. **Dimensão 1 ($D$ - Features):** O número de atributos por amostra (neste caso, 1 característica: distância).
    

### O Conceito de "Batch Dimension"

Modelos PyTorch são projetados para processar lotes (batches), não apenas amostras individuais.

- O modelo espera que a **primeira dimensão** seja sempre a contagem de "quantos itens existem na pilha".
    
- O modelo aplica as operações matemáticas (pesos e viés) de forma idêntica a cada item dessa pilha, independentemente se $N=1$ ou $N=1000$.
    

> **Erro Comum:** Tentar passar 3 features (ex: Distância, Hora, Clima) para um modelo treinado apenas com 1 feature resultará em `RuntimeError: mat1 and mat2 shapes cannot be multiplied`.

---

## 2. Tipagem de Dados (Dtypes) e Precisão

O controle explícito dos tipos de dados é essencial para a estabilidade numérica e eficiência de memória.

|**Tipo de Dado**|**Código PyTorch**|**Uso Típico**|**Notas de Engenharia**|
|---|---|---|---|
|**Float 32**|`torch.float32`|**Padrão** para Pesos/Ativações|O "Sweet Spot": equilíbrio ideal entre precisão e velocidade em GPUs modernas.|
|**Float 64**|`torch.float64`|Cálculos Científicos|Alta precisão, mas dobro do consumo de memória e mais lento. Evite em Deep Learning padrão.|
|**Int 64**|`torch.int64`|Índices, Contagens|Padrão para inteiros.|

### Promoção de Tipos (Type Promotion)

O PyTorch moderno suporta operações mistas. Se você somar um `Int` com um `Float`, ele realiza o _casting_ implícito para `Float` (semelhante ao Python nativo) para evitar perda de dados.

- `tensor_int + tensor_float` $\rightarrow$ `tensor_float`
    

---

## 3. Criação e Interoperabilidade

Além de criar tensores do zero (`torch.zeros`, `torch.ones`, `torch.randn`), a interoperabilidade com o ecossistema Python é robusta.

### NumPy Bridge

```python
# Cuidado: Compartilhamento de Memória
numpy_array = np.array([1, 2, 3])
tensor = torch.from_numpy(numpy_array)
```

**Atenção:** A conversão de NumPy para Tensor (e vice-versa) geralmente cria uma _view_ e não uma cópia. Se você alterar o valor no tensor, o array NumPy original também será alterado (e vice-versa), pois ambos apontam para o mesmo endereço de memória.

## 4. Manipulação Dimensional (Reshaping)

Frequentemente, você terá dados brutos que não possuem as dimensões necessárias para o modelo.

### O Problema do Escalar

Se você quiser fazer uma previsão para uma única distância (ex: 25 milhas), o dado bruto é um escalar (dimensão 0). O modelo exige dimensão 2 (Batch, Feature).

```python
x = torch.tensor(25.0)      # Shape: [] (Escalar)
# O modelo exige: [1, 1]
```

### Ferramentas de Ajuste: Squeeze e Unsqueeze

- **`unsqueeze(dim)`:** Adiciona uma dimensão de tamanho 1 na posição especificada. Fundamental para transformar uma única amostra em um "batch de 1".

```python
x = torch.tensor([25.0]) # Shape: [1]
x = x.unsqueeze(0)       # Shape: [1, 1] -> Agora o modelo aceita
```

**`squeeze()`:** Remove todas as dimensões que tenham tamanho 1. Útil para limpar saídas do modelo antes de pós-processamento.

## 5. Extração de Valores e Indexação

A manipulação de tensores segue a lógica de fatiamento (slicing) do Python/NumPy.

- **Slicing:** `tensor[0:3]` (Pega as 3 primeiras amostras).
    
- **Extração Escalar (`.item()`):** Para converter um tensor de um único elemento em um número Python puro (float/int), usamos `.item()`.
    
    - _Nota:_ Isso falha se o tensor tiver mais de um elemento.

```python
predicao = tensor[0] # Retorna um tensor
valor_real = predicao.item() # Retorna um float Python
```

### 🛠️ Resumo de Depuração

1. **Sempre** verifique `tensor.shape` antes de qualquer operação de matriz.
    
2. Garanta que a entrada é `float32`.
    
3. Lembre-se que o modelo sempre espera `[Batch_Size, Features]`.