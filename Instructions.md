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
