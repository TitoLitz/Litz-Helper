# 🦊 Litz-Helper

O **Litz-Helper** é um assistente pessoal baseado em IA construído sobre a arquitetura **RAG (Retrieval-Augmented Generation)**. Seu objetivo principal é fornecer respostas precisas, diretas e contextualizadas a partir da raspagem contínua de sites de referência, mantendo uma comunicação no tom e estilo do usuário.

O projeto foi planejado para ser **100% gratuito**, podendo alternar entre modelos em nuvem (Gemini API) ou inferência local via GPU (Ollama/Llama 3), rodando em servidor VPS ou máquina pessoal.

---

## 🎯 Objetivos do Projeto

- **Consulta Estruturada:** Raspar e indexar informações de 3 fontes primárias de referência:
  - [PrydwenGG](https://www.prydwen.gg/)
  - [Gachabase](https://gachabase.net/?lang=en)
  - [Nanoka](https://nanoka.cc/)
- **Alinhamento de Persona:** Responder no tom de voz, clareza e padrão de comunicação do usuário.
- **Eficiência de Recursos:** Funcionar sem dependência contínua da GPU local através de consumo de APIs gratuitas na nuvem.
- **Integração Futura:** Atuar como backend para bots (ex: Bot de Discord com comandos `!duvida`).

---

## 🏗️ Arquitetura do Sistema

```text
[ Scraping (3 Sites) ] ➡️ [ Processamento de Textos ]
                                    ⬇️
                         [ Banco Vetorial (ChromaDB) ]
                                    ⬇️
 [ Usuário / Discord ] ➡️ [ RAG Engine + Prompt Persona ] ➡️ [ LLM (Gemini API / Ollama) ]
                                    ⬇️
                           [ Resposta Final ]

## Estrutura recomendada de pastas
Litz-Helper/
│
├── data/                   # Arquivos raspados e base de dados local
│   ├── raw/                # Conteúdo bruto retornado dos sites (.md ou .json)
│   └── chroma_db/          # Banco de dados vetorial indexado
│
├── src/                    # Código-fonte principal
│   ├── scraper.py          # Script de raspagem dos 3 sites
│   ├── vector_store.py     # Script para gerar e salvar embeddings no ChromaDB
│   ├── rag_engine.py       # Lógica do RAG (ChromaDB + Gemini/Ollama)
│   └── bot.py              # Script da integração com o Discord (futuro)
│
├── .env.example            # Exemplo de variáveis de ambiente
├── .gitignore              # Arquivos e pastas a serem ignorados pelo Git
├── requirements.txt        # Dependências do projeto Python
└── README.md               # Documentação do repositório

.env Exemplo
# Provedor Ativo: "gemini" ou "ollama"
LLM_PROVIDER=gemini

# Chaves de API
GEMINI_API_KEY=sua_chave_do_google_ai_studio_aqui

# Configurações do Ollama Local
OLLAMA_HOST=http://localhost:11434
OLLAMA_MODEL=llama3

# Discord (Futuro)
DISCORD_TOKEN=seu_token_do_bot_aqui

