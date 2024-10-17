<div align="center">
 <img alt="ollama" height="200px" src="https://github.com/ollama/ollama/assets/3325447/0d0b44e2-8f4a-4e99-9b52-a5c1c741c8f7">
</div>

# Ollama.ro

[![Discord](https://dcbadge.vercel.app/api/server/ollama?style=flat&compact=true)](https://discord.gg/ollama)

Configurează și începe să utilizezi modele lingvistice de mari dimensiuni.

### macOS

[Descarcă](https://ollama.com/download/Ollama-darwin.zip)

### Windows preview

[Descarcă](https://ollama.com/download/OllamaSetup.exe)

### Linux

```
curl -fsSL https://ollama.com/install.sh | sh
```

[Instrucțiuni pentru instalare manuală](https://github.com/ollama/ollama/blob/main/docs/linux.md)

### Docker

Imaginea oficială [Ollama Docker](https://hub.docker.com/r/ollama/ollama) `ollama/ollama` este disponibilă pe Docker Hub.

### Biblioteci

- [ollama-python](https://github.com/ollama/ollama-python)
- [ollama-js](https://github.com/ollama/ollama-js)

## Pornire rapidă

Pentru a rula și comunica cu [Llama 3.2](https://ollama.com/library/llama3.2):

```
ollama run llama3.2
```

## Biblioteca de modele

Ollama suportă o listă de modele disponibile pe [ollama.com/library](https://ollama.com/library 'biblioteca de modele ollama')

Iată câteva exemple de modele ce pot fi descărcate:

| Model              | Parametri | Dimensiune | Descărcare                       |
| ------------------ | ---------- | ---------- | ------------------------------- |
| Llama 3.2          | 3B         | 2.0GB      | `ollama run llama3.2`           |
| Llama 3.2          | 1B         | 1.3GB      | `ollama run llama3.2:1b`        |
| Llama 3.1          | 8B         | 4.7GB      | `ollama run llama3.1`           |
| Llama 3.1          | 70B        | 40GB       | `ollama run llama3.1:70b`       |
| Llama 3.1          | 405B       | 231GB      | `ollama run llama3.1:405b`      |
| Phi 3 Mini         | 3.8B       | 2.3GB      | `ollama run phi3`               |
| Phi 3 Medium       | 14B        | 7.9GB      | `ollama run phi3:medium`        |
| Gemma 2            | 2B         | 1.6GB      | `ollama run gemma2:2b`          |
| Gemma 2            | 9B         | 5.5GB      | `ollama run gemma2`             |
| Gemma 2            | 27B        | 16GB       | `ollama run gemma2:27b`         |
| Mistral            | 7B         | 4.1GB      | `ollama run mistral`            |
| Moondream 2        | 1.4B       | 829MB      | `ollama run moondream`          |
| Neural Chat        | 7B         | 4.1GB      | `ollama run neural-chat`        |
| Starling           | 7B         | 4.1GB      | `ollama run starling-lm`        |
| Code Llama         | 7B         | 3.8GB      | `ollama run codellama`          |
| Llama 2 Uncensored | 7B         | 3.8GB      | `ollama run llama2-uncensored`  |
| LLaVA              | 7B         | 4.5GB      | `ollama run llava`              |
| Solar              | 10.7B      | 6.1GB      | `ollama run solar`              |

> [!NOTĂ]
> Trebuie să ai cel puțin 8 GB RAM disponibili pentru a rula modelele de 7B, 16 GB pentru cele de 13B și 32 GB pentru cele de 33B.

## Personalizarea unui model

### Import din GGUF

Ollama suportă importul de modele GGUF în Modelfile:

1. Creează un fișier numit `Modelfile`, cu instrucțiunea `FROM` care indică calea locală a modelului pe care vrei să îl importi.

   ```
   FROM ./vicuna-33b.Q4_0.gguf
   ```

2. Creează modelul în Ollama

   ```
   ollama create example -f Modelfile
   ```

3. Rulează modelul

   ```
   ollama run example
   ```

### Import din PyTorch sau Safetensors

Vezi [ghidul](docs/import.md) pentru mai multe informații despre importul modelelor.

### Personalizarea unui prompt

Modelele din biblioteca Ollama pot fi personalizate cu un prompt. De exemplu, pentru a personaliza modelul `llama3.2`:

```
ollama pull llama3.2
```

Creează un `Modelfile`:

```
FROM llama3.2

# setează temperatura la 1 [mai mare pentru creativitate, mai mică pentru coerență]
PARAMETER temperature 1

# setează mesajul sistemului
SYSTEM """
Ești Mario din Super Mario Bros. Răspunde doar ca Mario, asistentul.
"""
```

Apoi, creează și rulează modelul:

```
ollama create mario -f ./Modelfile
ollama run mario
>>> salut
Salut! Sunt prietenul tău Mario.
```

Pentru mai multe exemple, vezi directorul [examples](examples). Pentru mai multe informații despre lucrul cu un Modelfile, vezi documentația [Modelfile](docs/modelfile.md).

## Referințe CLI

### Crearea unui model

`ollama create` este folosit pentru a crea un model dintr-un Modelfile.

```
ollama create mymodel -f ./Modelfile
```

### Descărcarea unui model

```
ollama pull llama3.2
```

> Această comandă poate fi folosită și pentru a actualiza un model local. Doar diferența va fi descărcată.

### Ștergerea unui model

```
ollama rm llama3.2
```

### Copierea unui model

```
ollama cp llama3.2 my-model
```

### Input pe mai multe linii

Pentru input pe mai multe linii, poți încadra textul cu `"""`:

```
>>> """Salut,
... lume!
... """
Sunt un program de bază care afișează celebrul mesaj "Salut, lume!" pe ecran.
```

### Modele multimodale

```
ollama run llava "Ce este în această imagine? /Users/jmorgan/Desktop/smile.png"
Imaginea conține un zâmbet galben, care probabil este punctul central al imaginii.
```

### Transmiterea promptului ca argument

```
$ ollama run llama3.2 "Rezumați acest fișier: $(cat README.md)"
 Ollama este un framework extensibil și ușor de utilizat pentru construirea și rularea de modele lingvistice pe computerul local. Oferă o API simplă pentru crearea, rularea și gestionarea modelelor, precum și o bibliotecă de modele predefinite care pot fi utilizate ușor în diverse aplicații.
```

### Afișarea informațiilor despre model

```
ollama show llama3.2
```

### Listarea modelelor pe computer

```
ollama list
```

### Listarea modelelor în prezent încărcate

```
ollama ps
```

### Oprirea unui model aflat în rulare

```
ollama stop llama3.2
```

### Pornirea Ollama

`ollama serve` este utilizat atunci când dorești să pornești ollama fără a rula aplicația desktop.

## Construcția

Vezi [ghidul pentru dezvoltatori](https://github.com/ollama/ollama/blob/main/docs/development.md)

### Rularea buildurilor locale

Începe serverul:

```
./ollama serve
```

Apoi, într-o altă sesiune, rulează un model:

```
./ollama run llama3.2
```

## REST API

Ollama are o API REST pentru rularea și gestionarea modelelor.

### Generarea unui răspuns

```
curl http://localhost:11434/api/generate -d '{
  "model": "llama3.2",
  "prompt":"De ce cerul este albastru?"
}'
```

### Conversație cu un model



```
curl http://localhost:11434/api/chat -d '{
  "model": "llama3.2",
  "messages": [
    { "role": "user", "content": "de ce cerul este albastru?" }
  ]
}'
```

Vezi [documentația API](./docs/api.md) pentru toate endpointurile.

## Integrări Comunitare

### Web & Desktop

- [Open WebUI](https://github.com/open-webui/open-webui)
- [Enchanted (macOS native)](https://github.com/AugustDev/enchanted)
- [Hollama](https://github.com/fmaclen/hollama)
- [Lollms-Webui](https://github.com/ParisNeo/lollms-webui)
- [LibreChat](https://github.com/danny-avila/LibreChat)
- [Bionic GPT](https://github.com/bionic-gpt/bionic-gpt)
- [HTML UI](https://github.com/rtcfirefly/ollama-ui)
- [Saddle](https://github.com/jikkuatwork/saddle)
- [Chatbot UI](https://github.com/ivanfioravanti/chatbot-ollama)
- [Chatbot UI v2](https://github.com/mckaywrigley/chatbot-ui)
- [Typescript UI](https://github.com/ollama-interface/Ollama-Gui?tab=readme-ov-file)
- [Interfață React Minimalistă pentru Modelele Ollama](https://github.com/richawo/minimal-llm-ui)
- [Ollamac](https://github.com/kevinhermawan/Ollamac)
- [big-AGI](https://github.com/enricoros/big-AGI/blob/main/docs/config-local-ollama.md)
- [Cheshire Cat assistant framework](https://github.com/cheshire-cat-ai/core)
- [Amica](https://github.com/semperai/amica)
- [chatd](https://github.com/BruceMacD/chatd)
- [Ollama-SwiftUI](https://github.com/kghandour/Ollama-SwiftUI)
- [Dify.AI](https://github.com/langgenius/dify)
- [MindMac](https://mindmac.app)
- [NextJS Interfață Web pentru Ollama](https://github.com/jakobhoeg/nextjs-ollama-llm-ui)
- [Msty](https://msty.app)
- [Chatbox](https://github.com/Bin-Huang/Chatbox)
- [WinForm Ollama Copilot](https://github.com/tgraupmann/WinForm_Ollama_Copilot)
- [NextChat](https://github.com/ChatGPTNextWeb/ChatGPT-Next-Web) cu [Doc Începe](https://docs.nextchat.dev/models/ollama)
- [Alpaca WebUI](https://github.com/mmo80/alpaca-webui)
- [OllamaGUI](https://github.com/enoch1118/ollamaGUI)
- [OpenAOE](https://github.com/InternLM/OpenAOE)
- [Odin Runes](https://github.com/leonid20000/OdinRunes)
- [LLM-X](https://github.com/mrdjohnson/llm-x) (Aplicație Web Progresivă)
- [AnythingLLM (Docker + Aplicație nativă MacOs/Windows/Linux)](https://github.com/Mintplex-Labs/anything-llm)
- [Ollama Basic Chat: Utilizează HyperDiv UI Reactiv](https://github.com/rapidarchitect/ollama_basic_chat)
- [Ollama-chats RPG](https://github.com/drazdra/ollama-chats)
- [QA-Pilot](https://github.com/reid41/QA-Pilot) (Chat cu Repozitoriu de Cod)
- [ChatOllama](https://github.com/sugarforever/chat-ollama) (Chatbot Open Source bazat pe Ollama cu Baze de Cunoștințe)
- [CRAG Ollama Chat](https://github.com/Nagi-ovo/CRAG-Ollama-Chat) (Căutare Web Simplă cu RAG Corectiv)
- [RAGFlow](https://github.com/infiniflow/ragflow) (Motor Open-source pentru Generarea Îmbogățită cu Documente Profunde)
- [StreamDeploy](https://github.com/StreamDeploy-DevRel/streamdeploy-llm-app-scaffold) (Structură Aplicație LLM)
- [chat](https://github.com/swuecho/chat) (aplicație web de chat pentru echipe)
- [Lobe Chat](https://github.com/lobehub/lobe-chat) cu [Doc Integrare](https://lobehub.com/docs/self-hosting/examples/ollama)
- [Ollama RAG Chatbot](https://github.com/datvodinh/rag-chatbot.git) (Chat Local cu PDF-uri multiple folosind Ollama și RAG)
- [BrainSoup](https://www.nurgo-software.com/products/brainsoup) (Client flexibil nativ cu RAG & automatizare multi-agent)
- [macai](https://github.com/Renset/macai) (client macOS pentru Ollama, ChatGPT și alte API-uri compatibile)
- [Olpaka](https://github.com/Otacon/olpaka) (Aplicație Web Flutter prietenoasă pentru Ollama)
- [OllamaSpring](https://github.com/CrazyNeil/OllamaSpring) (Client Ollama pentru macOS)
- [LLocal.in](https://github.com/kartikm7/llocal) (Client Desktop Electron Ușor de utilizat pentru Ollama)
- [AiLama](https://github.com/zeyoyt/ailama) (Aplicație Discord ce permite interacțiunea cu Ollama în orice canal de discord)
- [Ollama cu Google Mesop](https://github.com/rapidarchitect/ollama_mesop/) (Implementare Client Mesop Chat cu Ollama)
- [Painting Droid](https://github.com/mateuszmigas/painting-droid) (Aplicație de pictură cu integrări AI)
- [Kerlig AI](https://www.kerlig.com/) (asistent de scriere AI pentru macOS)
- [AI Studio](https://github.com/MindWorkAI/AI-Studio)
- [Sidellama](https://github.com/gyopak/sidellama) (client LLM bazat pe browser)
- [LLMStack](https://github.com/trypromptly/LLMStack) (Cadru multi-agent fără cod pentru a construi agenți LLM și fluxuri de lucru)
- [BoltAI pentru Mac](https://boltai.com) (Client de Chat AI pentru Mac)
- [Harbor](https://github.com/av/harbor) (Trusă LLM Containerizată cu Ollama ca backend implicit)
- [Go-CREW](https://www.jonathanhecl.com/go-crew/) (RAG Offline Puternic în Golang)
- [PartCAD](https://github.com/openvmp/partcad/) (Generare model CAD cu OpenSCAD și CadQuery)
- [Ollama4j Web UI](https://github.com/ollama4j/ollama4j-web-ui) - UI Web bazat pe Java pentru Ollama construit cu Vaadin, Spring Boot și Ollama4j
- [PyOllaMx](https://github.com/kspviswa/pyOllaMx) - aplicație macOS capabilă să comunice atât cu Ollama, cât și cu modelele Apple MLX.
- [Claude Dev](https://github.com/saoudrizwan/claude-dev) - extensie VSCode pentru codarea multi-fișier/repozitoriu întreg
- [Cherry Studio](https://github.com/kangfenmao/cherry-studio) (client desktop cu suport Ollama)
- [ConfiChat](https://github.com/1runeberg/confichat) (Interfață de chat LLM multiplatformă și orientată spre confidențialitate, cu criptare opțională)
- [Archyve](https://github.com/nickthecook/archyve) (bibliotecă de documente ce permite RAG)
- [crewAI cu Mesop](https://github.com/rapidarchitect/ollama-crew-mesop) (Interfață Web Mesop pentru a rula crewAI cu Ollama)
- [LLMChat](https://github.com/trendy-design/llmchat) (Interfață de chat complet locală, intuitivă și orientată spre confidențialitate)
- [ARGO](https://github.com/xark-argo/argo) (Descarcă și rulează local modele Ollama și Huggingface cu RAG pe Mac/Windows/Linux)

### Terminal

- [oterm](https://github.com/ggozad/oterm)
- [Ellama client Emacs](https://github.com/s-kostyaev/ellama)
- [Client Emacs](https://github.com/zweifisch/ollama)
- [gen.nvim](https://github.com/David-Kunz/gen.nvim)
- [ollama.nvim](https://github.com/nomnivore/ollama.nvim)
- [ollero.nvim](https://github.com/marco-souza/ollero.nvim)
-

 [ollama-chat.nvim](https://github.com/gerazov/ollama-chat.nvim)
- [ogpt.nvim](https://github.com/huynle/ogpt.nvim)
- [gptel client Emacs](https://github.com/karthink/gptel)
- [Oatmeal](https://github.com/dustinblackman/oatmeal)
- [cmdh](https://github.com/pgibler/cmdh)
- [ooo](https://github.com/npahlfer/ooo)
- [shell-pilot](https://github.com/reid41/shell-pilot)
- [tenere](https://github.com/pythops/tenere)
- [llm-ollama](https://github.com/taketwo/llm-ollama) pentru [CLI-ul LLM de la Datasette](https://llm.datasette.io/en/stable/).
- [typechat-cli](https://github.com/anaisbetts/typechat-cli)
- [ShellOracle](https://github.com/djcopley/ShellOracle)
- [tlm](https://github.com/yusufcanb/tlm)
- [podman-ollama](https://github.com/ericcurtin/podman-ollama)
- [gollama](https://github.com/sammcj/gollama)
- [Rezumat eBook Ollama](https://github.com/cognitivetech/ollama-ebook-summary/)
- [Ollama Mixture of Experts (MOE) în 50 de linii de cod](https://github.com/rapidarchitect/ollama_moe)
- [vim-intelligence-bridge](https://github.com/pepo-ec/vim-intelligence-bridge) Interacțiune simplă a "Ollama" cu editorul Vim

### Apple Vision Pro
- [Enchanted](https://github.com/AugustDev/enchanted)

### Bază de date

- [MindsDB](https://github.com/mindsdb/mindsdb/blob/staging/mindsdb/integrations/handlers/ollama_handler/README.md) (Conectează modelele Ollama cu aproape 200 de platforme de date și aplicații)
- [chromem-go](https://github.com/philippgille/chromem-go/blob/v0.5.0/embed_ollama.go) cu [exemplu](https://github.com/philippgille/chromem-go/tree/v0.5.0/examples/rag-wikipedia-ollama)

### Manageri de pachete

- [Pacman](https://archlinux.org/packages/extra/x86_64/ollama/)
- [Gentoo](https://github.com/gentoo/guru/tree/master/app-misc/ollama)
- [Helm Chart](https://artifacthub.io/packages/helm/ollama-helm/ollama)
- [Canal Guix](https://codeberg.org/tusharhero/ollama-guix)
- [Pachet Nix](https://search.nixos.org/packages?channel=24.05&show=ollama&from=0&size=50&sort=relevance&type=packages&query=ollama)
- [Flox](https://flox.dev/blog/ollama-part-one)

### Biblioteci

- [LangChain](https://python.langchain.com/docs/integrations/llms/ollama) și [LangChain.js](https://js.langchain.com/docs/modules/model_io/models/llms/integrations/ollama) cu [exemplu](https://js.langchain.com/docs/use_cases/question_answering/local_retrieval_qa)
- [Firebase Genkit](https://firebase.google.com/docs/genkit/plugins/ollama)
- [crewAI](https://github.com/crewAIInc/crewAI)
- [LangChainGo](https://github.com/tmc/langchaingo/) cu [exemplu](https://github.com/tmc/langchaingo/tree/main/examples/ollama-completion-example)
- [LangChain4j](https://github.com/langchain4j/langchain4j) cu [exemplu](https://github.com/langchain4j/langchain4j-examples/tree/main/ollama-examples/src/main/java)
- [LangChainRust](https://github.com/Abraxas-365/langchain-rust) cu [exemplu](https://github.com/Abraxas-365/langchain-rust/blob/main/examples/llm_ollama.rs)
- [LlamaIndex](https://docs.llamaindex.ai/en/stable/examples/llm/ollama/) și [LlamaIndexTS](https://ts.llamaindex.ai/modules/llms/available_llms/ollama)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [OllamaFarm pentru Go](https://github.com/presbrey/ollamafarm)
- [OllamaSharp pentru .NET](https://github.com/awaescher/OllamaSharp)
- [Ollama pentru Ruby](https://github.com/gbaptista/ollama-ai)
- [Ollama-rs pentru Rust](https://github.com/pepperoni21/ollama-rs)
- [Ollama-hpp pentru C++](https://github.com/jmont-dev/ollama-hpp)
- [Ollama4j pentru Java](https://github.com/ollama4j/ollama4j)
- [Bibliotecă Typescript ModelFusion](https://modelfusion.dev/integration/model-provider/ollama)
- [OllamaKit pentru Swift](https://github.com/kevinhermawan/OllamaKit)
- [Ollama pentru Dart](https://github.com/breitburg/dart-ollama)
- [Ollama pentru Laravel](https://github.com/cloudstudio/ollama-laravel)
- [LangChainDart](https://github.com/davidmigloz/langchain_dart)
- [Semantic Kernel - Python](https://github.com/microsoft/semantic-kernel/tree/main/python/semantic_kernel/connectors/ai/ollama)
- [Haystack](https://github.com/deepset-ai/haystack-integrations/blob/main/integrations/ollama.md)
- [LangChain pentru Elixir](https://github.com/brainlid/langchain)
- [Ollama pentru R - rollama](https://github.com/JBGruber/rollama)
- [Ollama pentru R - ollama-r](https://github.com/hauselin/ollama-r)
- [Ollama-ex pentru Elixir](https://github.com/lebrunel/ollama-ex)
- [Conector Ollama pentru SAP ABAP](https://github.com/b-tocs/abap_btocs_ollama)
- [Testcontainers](https://testcontainers.com/modules/ollama/)
- [Portkey](https://portkey.ai/docs/welcome/integration-guides/ollama)
- [PromptingTools.jl](https://github.com/svilupp/PromptingTools.jl) cu un [exemplu](https://svilupp.github.io/PromptingTools.jl/dev/examples/working_with_ollama)
- [LlamaScript](https://github.com/Project-Llama/llamascript)
- [Gollm](https://docs.gollm.co/examples/ollama-example)
- [Ollamaclient pentru Golang](https://github.com/xyproto/ollamaclient)
- [Funcție de abstracție la nivel înalt în Go](https://gitlab.com/tozd/go/fun)
- [Ollama PHP](https://github.com/ArdaGnsrn/ollama-php)
- [Agents-Flex pentru Java](https://github.com/agents-flex/agents-flex) cu [exemplu](https://github.com/agents-flex/agents-flex/tree/main/agents-flex-llm/agents-flex-llm-ollama/src/test/java/com/agentsflex/llm/ollama)

### Mobil

- [Enchanted](https://github.com/AugustDev/enchanted)
- [Maid](https://github.com/Mobile-Artificial-Intelligence/maid)
- [ConfiChat](https://github.com/1runeberg/confichat) (Interfață de chat multiplatformă, ușoară și axată pe confidențialitate, cu criptare opțională)

### Extensii & Pluginuri

- [Extensie Raycast](https://github.com/MassimilianoPasquini97/raycast_ollama)
- [Discollama](https://github.com/mxyng/discollama) (Bot Discord în canalul Ollama)
- [Continue](https://github.com/continuedev/continue)
- [Plugin Obsidian Ollama](https://github.com/hinterdupfinger/obsidian-ollama)
- [Plugin Logseq Ollama](https://github.com/omagdy7/ollama-logseq)
- [NotesOllama](https://github.com/andersrex/notesollama) (Plugin Apple Notes Ollama)
- [Dagger Chatbot](https://github.com/samalba/dagger-chatbot)
- [Bot AI Discord](https://github.com/mekb-turtle/discord-ai-bot)
- [Ollama Telegram Bot](https://github.com/ruecat/ollama-telegram)
- [Hass Ollama Conversation](https://github.com/ej52/hass-ollama-conversation)
- [Plugin Rivet](https://github.com/abrenneke/r

ivet-plugin-ollama)
- [Plugin Obsidian BMO Chatbot](https://github.com/longy2k/obsidian-bmo-chatbot)
- [Cliobot](https://github.com/herval/cliobot) (Bot Telegram cu suport Ollama)
- [Plugin Copilot pentru Obsidian](https://github.com/logancyang/obsidian-copilot)
- [Plugin Local GPT pentru Obsidian](https://github.com/pfrankov/obsidian-local-gpt)
- [Interpreter Deschis](https://docs.openinterpreter.com/language-model-setup/local-models/ollama)
- [Llama Coder](https://github.com/ex3ndr/llama-coder) (Alternativă Copilot utilizând Ollama)
- [Ollama Copilot](https://github.com/bernardo-bruning/ollama-copilot) (Proxy ce îți permite să folosești ollama ca un copilot similar cu Github Copilot)
- [twinny](https://github.com/rjmacarthy/twinny) (Alternativă Copilot și chat copilot utilizând Ollama)
- [Wingman-AI](https://github.com/RussellCanfield/wingman-ai) (Alternativă Copilot cod și chat utilizând Ollama și Hugging Face)
- [Page Assist](https://github.com/n4ze3m/page-assist) (Extensie Chrome)
- [Plasmoid Ollama Control](https://github.com/imoize/plasmoid-ollamacontrol) (Extensie KDE Plasma ce îți permite să gestionezi/controlzi rapid modelul Ollama)
- [Bot AI Telegram](https://github.com/tusharhero/aitelegrambot) (Bot Telegram ce folosește Ollama în backend)
- [AI ST Completion](https://github.com/yaroslavyaroslav/OpenAI-sublime-text) (Plugin Sublime Text 4 cu suport Ollama)
- [Discord-Ollama Chat Bot](https://github.com/kevinthedang/discord-ollama) (Bot Discord Generalizat TypeScript cu Documentație pentru Reglare)
- [Bot AI chat/moderare Discord](https://github.com/rapmd73/Companion) Bot de chat/moderare scris în python. Utilizează Ollama pentru a crea personalități.
- [Headless Ollama](https://github.com/nischalj10/headless-ollama) (Scripturi pentru a instala automat clientul ollama & modelele pe orice OS pentru aplicații care depind de serverul ollama)
- [vnc-lm](https://github.com/jk011ru/vnc-lm) (Un bot Discord containerizat cu suport pentru atașamente și linkuri web)
- [LSP-AI](https://github.com/SilasMarvin/lsp-ai) (Server de limbaj open-source pentru funcționalități AI-powered)
- [QodeAssist](https://github.com/Palm1r/QodeAssist) (Plugin AI-powered assistant pentru Qt Creator)
- [Generator Quiz pentru Obsidian](https://github.com/ECuiDev/obsidian-quiz-generator)

### Backends suportate

- [llama.cpp](https://github.com/ggerganov/llama.cpp) proiect fondat de Georgi Gerganov.
