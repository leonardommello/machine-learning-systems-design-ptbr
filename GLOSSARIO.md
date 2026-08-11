# Glossário de Tradução — PT-BR

Referência canônica para a tradução deste repositório. Toda tradução deve consultar
este arquivo antes de escolher um termo. Em caso de conflito, este arquivo vence.

Política adotada: **tradução integral para o português**, usando o termo consagrado em
português sempre que existir. Nomes próprios, produtos e siglas do setor não são
traduzidos.

---

## 1. Regra de ouro

Traduz-se **prosa**. Não se traduz **nome**.

Nome de modelo, empresa, produto, biblioteca, benchmark, artigo ou conferência fica
como está. Tudo ao redor vai para o português.

---

## 2. NÃO traduzir — lista de bloqueio

| Categoria | Exemplos |
|---|---|
| Modelos e famílias | GPT-4, Claude, Gemini, Llama, Mistral, Qwen, DeepSeek, Stable Diffusion |
| Empresas e laboratórios | OpenAI, Anthropic, Google DeepMind, Meta, Hugging Face, Mistral AI |
| Produtos e plataformas | ChatGPT, Copilot, LangChain, LlamaIndex, Weights & Biases, Ray, vLLM |
| Bibliotecas e ferramentas | PyTorch, TensorFlow, transformers, FastAPI, Kubernetes, Docker, Airflow |
| Benchmarks e conjuntos de avaliação | MMLU, HumanEval, HELM, GSM8K, SWE-bench, Chatbot Arena |
| Técnicas com sigla consagrada | RAG, RLHF, DPO, LoRA, PEFT, MoE, CoT, KV cache |
| Títulos de artigos e livros | mantidos no idioma original |
| Nomes de arquivos, caminhos e URLs | `resources.md`, `scripts/`, qualquer `https://...` |
| Formatos e siglas de infraestrutura | JSON, YAML, CSV, API, SDK, GPU, TPU, CPU, RAM, SLA, QPS |

**Nota sobre siglas.** A sigla em inglês permanece. Na primeira ocorrência de um
documento, expandir em português e manter a sigla entre parênteses — por exemplo
"geração aumentada por recuperação (RAG)" — e depois usar só a sigla.

---

## 3. Termos centrais de engenharia de IA

| Inglês | Português | Observação |
|---|---|---|
| machine learning (ML) | machine learning | mantido em inglês; é a forma usada no mercado brasileiro e no título da edição oficial da Alta Books |
| MLOps | MLOps | manter |
| AI engineering | engenharia de IA | |
| foundation model | modelo de fundação | |
| large language model (LLM) | modelo de linguagem de grande porte (LLM) | sigla mantida |
| multimodal model | modelo multimodal | |
| prompt | prompt | manter |
| prompt engineering | engenharia de prompt | |
| system prompt | prompt de sistema | |
| few-shot / zero-shot | few-shot / zero-shot | manter |
| chain-of-thought | cadeia de raciocínio (CoT) | sigla mantida |
| context window | janela de contexto | |
| token | token | plural: tokens |
| tokenizer | tokenizador | |
| embedding | incorporação | plural: incorporações |
| vector database | banco de dados vetorial | |
| retrieval | recuperação | |
| retrieval-augmented generation | geração aumentada por recuperação (RAG) | |
| chunking | fatiamento | de documentos |
| reranking | reordenação | |
| agent | agente | |
| tool use / function calling | uso de ferramentas / chamada de função | |
| planning | planejamento | |
| memory | memória | de agentes |
| fine-tuning | ajuste fino | |
| instruction tuning | ajuste por instrução | |
| alignment | alinhamento | |
| misalignment | desalinhamento | |
| preference tuning | ajuste por preferência | |
| reward model | modelo de recompensa | |
| distillation | destilação | |
| quantization | quantização | |
| pruning | poda | |
| inference | inferência | |
| inference optimization | otimização de inferência | |
| batching | agrupamento em lote | |
| caching | cache | verbo: usar cache |
| streaming | streaming | manter |
| latency | latência | |
| throughput | vazão | |
| time to first token | tempo até o primeiro token | |
| cost per token | custo por token | |
| evaluation | avaliação | |
| eval | avaliação | nunca "eval" solto na prosa |
| benchmark | benchmark | manter como substantivo |
| ground truth | verdade de referência | |
| hallucination | alucinação | |
| guardrails | salvaguardas | |
| safety | segurança | no sentido de danos |
| security | segurança | no sentido de ataques |
| prompt injection | injeção de prompt | |
| jailbreak | jailbreak | manter |
| red teaming | red teaming | manter |
| observability | observabilidade | |
| monitoring | monitoramento | |
| drift | desvio | de dados ou de modelo |
| feedback loop | ciclo de retroalimentação | |
| human in the loop | humano no ciclo | |
| dataset | conjunto de dados | |
| data pipeline | pipeline de dados | |
| synthetic data | dados sintéticos | |
| data curation | curadoria de dados | |
| annotation / labeling | anotação / rotulagem | |
| deployment | implantação | |
| serving | serviço de inferência | verbo: servir |
| scaling | escalonamento | |
| open weights | pesos abertos | |
| open source | código aberto | |
| API provider | provedor de API | |
| rate limit | limite de requisições | |
| use case | caso de uso | |
| trade-off | compromisso | |
| best practice | boa prática | |
| state of the art | estado da arte | |

---

## 4. Convenções de escrita

**Registro.** Segunda pessoa indireta ("você"), tom analítico, presente do indicativo.

**Gerundismo.** Proibido. "Vamos avaliar", nunca "vamos estar avaliando".

**Números e unidades.** Vírgula decimal (`0,5`), ponto de milhar (`1.024`).
Valores em dólar permanecem em dólar, com o símbolo antes do número (`US$ 20`).

**Títulos de seção.** Traduzir o texto, preservar a numeração e a hierarquia exatas.

**Capitalização de títulos.** O inglês usa *Title Case*; o português, não. Em título —
cabeçalho, item de sumário ou legenda — só levam maiúscula a primeira palavra e os nomes
próprios.

- Errado: `## Avaliando Modelos de Fundação em Produção`
- Certo: `## Avaliando modelos de fundação em produção`

Nomes próprios, produtos e siglas continuam capitalizados como sempre: OpenAI, PyTorch,
Hugging Face, RAG, MLOps, GPU. `scikit-learn` e `vLLM` mantêm a grafia oficial mesmo em
início de título.

**Markdown.** Preservar intactos: níveis de cabeçalho, tabelas, listas, blocos de
código, tags HTML, delimitadores LaTeX (`$`, `$$`) e âncoras de link internas.

**Links.** URLs nunca mudam. O texto do link traduz-se apenas quando é prosa; quando é
o título de um artigo ou de um livro, permanece no idioma original.

**Referências ao livro.** O título *Machine Learning Systems Design* permanece em
inglês por ser o nome pelo qual o booklet é conhecido.

---

## 5. Escopo

A tradução vive em `Translation/Portuguese-BR/`, espelhando os caminhos dos arquivos
originais, e é submetida à autora por pull request — mesmo formato da tradução para o
farsi já aceita no repositório original.

O site deste repositório **não republica a obra**: publica apenas o estado do projeto,
este glossário e a orientação para contribuir. O booklet original é de Chip Huyen e
deve ser lido em [huyenchip.com](https://huyenchip.com/machine-learning-systems-design/toc.html).
