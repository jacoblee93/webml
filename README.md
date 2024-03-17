# 🏠 Fully Local Chat Over Documents

Yes, it's another chat over documents implementation... but this one is entirely local!

It can even run fully in your browser with a small LLM via [WebLLM](https://webllm.mlc.ai/)!

![](/public/images/demo_browser_only.gif)

It's a Next.js app that read the content of an uploaded PDF, chunks it, adds it to a vector store, and
performs RAG, all client side. You can even turn off your WiFi after the site loads.

You can see a live version at https://webml-demo.vercel.app.

Users can choose one of the below options to run inference:

## Browser-only mode

You can run the entire stack your browser via [WebLLM](https://webllm.mlc.ai/). The model used is the small, 2.7B parameter [Phi-2](https://huggingface.co/microsoft/phi-2).

You don't have to leave the window to set this up - just upload a PDF and go!

Note that the first time you start a chat, the app will download and cache the model weights. This download is several GB in size and may take a little while, so make sure you have a good internet connection!

## Fully client-side Ollama

You can run more powerful, general models outside the browser using [Ollama's desktop app](https://ollama.ai). Users will need to download and set up then run the following commands to allow the site access to a locally running Mistral instance:

### Mac/Linux

```bash
$ OLLAMA_ORIGINS=https://webml-demo.vercel.app OLLAMA_HOST=127.0.0.1:11435 ollama serve
```
Then, in another terminal window:

```bash
$ OLLAMA_HOST=127.0.0.1:11435 ollama pull mistral
```

### Windows

```cmd
$ set OLLAMA_ORIGINS=https://webml-demo.vercel.app
set OLLAMA_HOST=127.0.0.1:11435
ollama serve
```
Then, in another terminal window:

```cmd
$ set OLLAMA_HOST=127.0.0.1:11435
ollama pull mistral
```

## ⚡ Stack

It uses the following:

- [Voy](https://github.com/tantaraio/voy) as the vector store, fully WASM in the browser.
- [Ollama](https://ollama.ai/) or [WebLLM](https://webllm.mlc.ai/) to run an LLM locally and expose it to the web app.
- [LangChain.js](https://js.langchain.com) to call the models, perform retrieval, and generally orchestrate all the pieces.
- [Transformers.js](https://huggingface.co/docs/transformers.js/index) to run open source [Nomic](https://www.nomic.ai/) embeddings in the browser.
  - For higher-quality embeddings, switch to `"nomic-ai/nomic-embed-text-v1"` in `app/worker.ts`.

While the goal is to run as much of the app as possible directly in the browser, but you can swap in [Ollama embeddings](https://js.langchain.com/docs/modules/data_connection/text_embedding/integrations/ollama) in lieu of Transformers.js as well.

## 🔱 Forking

To run/deploy this yourself, simply fork this repo and install the required dependencies with `yarn`.

There are no required environment variables!

## 📖 Further reading

For a bit more on this topic, check out [my blog post on Ollama](https://ollama.ai/blog/building-llm-powered-web-apps) or [my Google Summit talk on building with LLMs in the browser](https://www.youtube.com/watch?v=-1sdWLr3TbI).

## 🙏 Thank you!

Special thanks to:

- [@dawchihliou](https://twitter.com/dawchihliou) for making Voy
- [@jmorgan](https://twitter.com/jmorgan) and [@mchiang0610](https://twitter.com/mchiang0610) for making Ollama and for your feedback
- [@charlie_ruan](https://twitter.com/charlie_ruan) for your incredible work on WebLLM
- [@xenovacom](https://twitter.com/xenovacom) for making Transformers.js
- And [@jason_mayes](https://twitter.com/jason_mayes) and [@nfcampos](https://twitter.com/nfcampos) for inspiration and some great conversations.

For more, follow me on Twitter [@Hacubu](https://x.com/hacubu)!
