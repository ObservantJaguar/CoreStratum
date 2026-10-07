# Тематическая инструкция: wiki «Нейросети и ИИ»

> **Как использовать:** объедините с общим шаблоном `00-template.md` — сначала шаблон (структура, конфиги, правила кодировки), затем эта тематическая часть. Скопируйте в новый чат MultiTool.

## Тема и назначение

Постройте англоязычную wiki-энциклопедию о нейросетях, машинном обучении и искусственном интеллекте — для инженеров, DevOps-инженеров и разработчиков, интересующихся open-source инструментами и само-хостингом. Стиль — технический, по образцу основной вики CoreStratum.

## Важные принципы содержания

- Фокус на **технологиях и инструментах**, а не на маркетинге «ИИ-продуктов».
- Предпочтение **open-source** (Llama, Mistral, Stable Diffusion, Whisper и пр.); проприетарные модели и сервисы (GPT-4, Claude и т.п.) — отмечать как Proprietary, но включать (это реальность индустрии).
- Честно указывать статус: версия, лицензия модели (например, Llama 3.1 Community License — не OSI), требования к железу.
- Помечать грань между «моделью» (веса) и «инструментом» (программа запуска).

## Структура в трёх классах

### Theory (теория и концепции)

- **ML/DL fundamentals** — обучение, градиентный спуск, нейрон (перцептрон), слои, функции активации.
- **Transformer architecture** — attention, self-attention, positional encoding; почему это основа современных LLM.
- **Model families и парадигмы** — encoder-only (BERT), decoder-only (GPT), encoder-decoder (T5); LLM, VLM, diffusion models, multimodal.
- **Training concepts** — обучение с нуля, fine-tuning, LoRA/QLoRA, RLHF, instruction tuning, few-shot.
- **Inference** — инференс, KV-cache, квантизация (INT8, INT4), сжатие, batch processing.
- **Benchmarks и оценка** — perplexity, MMLU, HumanEval, косты и метрики качества.
- **Ethics and safety** — нейтрально, факты: bias, hallucination, jailbreak, alignment.

### Tools (энциклопедия ПО)

Категории инструментов (каждая — с отдельными страницами):

- **Runtimes/фреймворки** — PyTorch, TensorFlow, JAX; ONNX Runtime; llama.cpp (CPU/GPU инференс).
- **LLM-серверы и платформы инференса** — vLLM, TGI (Text Generation Inference), Ollama, llama.cpp, LocalAI, LM Studio (GUI), llama-server.
- **Self-hosted LLM-приложения** — text-generation-webui (oobabooga), Haystack, LangChain/LlamaIndex (фреймворки для приложений).
- **Embeddings и векторные БД** — sentence-transformers, Chroma, Qdrant, Weaviate, Milvus, pgvector, FAISS.
- **Обучение и fine-tuning инструменты** — Hugging Face Transformers/PEFT/TRL, axolotl, unsloth, DeepSpeed, FSDP.
- **Определение данных и датасеты** — Hugging Face Datasets, Common Crawl, наборы для бенчмарков.
- **Генерация изображений/видео/аудио** — Stable Diffusion (AUTOMATIC1111, ComfyUI), Fooocus; Whisper (ASR), Bark, ElevenLabs (prop), RVC.
- **Пайплайны и оркестрация** — Airflow (опционально), Flyte, Kubeflow; MLflow (эксперименты), Weights & Biases (включая open-source альтернативы).
- **Промпт-инженерия и агенты** — LangChain, LlamaIndex, CrewAI, AutoGen.

### Practice (практические руководства)

- Как запустить LLM локально: Ollama/llama.cpp — скачать модель, запустить, проверить инференс.
- Как развернуть сервер инференса (vLLM или TGI) на GPU-сервере с API OpenAI-совместимым.
- Как поднять Retrieval-Augmented Generation (RAG): векторная БД + эмбеддинги + LLM.
- Как сделать fine-tune модели (LoRA) на своём датасете.
- Как установить Stable Diffusion (ComfyUI) и сгенерировать изображение.
- Как запустить Whisper для транскрибации аудио.
- Безопасность и CI: квантование модели для слабого железа, Docker.

## Рекомендуемая структура доменов

```
docs/
├── sections/ (theory/tools/practice)
├── theory/           → категории: fundamentals, transformer, model-families, training, inference, benchmarks, safety
├── runtimes/         → фреймворки: PyTorch, TensorFlow, JAX, ONNX Runtime
├── llm-servers/      → Ollama, vLLM, TGI, LocalAI, llama.cpp, LM Studio
├── embeddings/       → векторные БД: Qdrant, Weaviate, Milvus, Chroma, pgvector, FAISS
├── finetuning/       → PEFT, axolotl, unsloth, DeepSpeed, TRL
├── multimodal/       → Stable Diffusion, ComfyUI, Whisper, Bark
├── agent-frameworks/ → LangChain, LlamaIndex, CrewAI, AutoGen
├── observability/    → MLflow, эксперименты, метрики (опционально)
└── guides/           → практические руководства
```

## Ключевые принципы содержания

- Каждая страница: `# Имя`, 2–4 предложения, `## Key features`, `## Resources` (официальные сайты/доки/GitHub).
- Для моделей указывайте: архитектура, размеры параметров, лицензия весов, контекстное окно, поддерживаемое железо.
- Для инструментов: язык, GPU/CPU требования, лицензия, статус зрелости.
- Помечайте проприетарное: `**License:** Proprietary — not open source`.
- Все ссылки — официальные; эмодзи нет; английский язык.

## Процесс

1. Возьмите структуру и конфиги из шаблона `00-template.md`.
2. Создайте TOC (index.md).
3. Наполняйте: каркас категорий → страницы инструментов партиями.
4. Прогоните чек-лист: ссылки, front matter, кодировка, сборка.
5. Push на GitHub.