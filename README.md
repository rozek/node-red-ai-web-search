# node-red-ai-web-search #

a simple AI LLM Web Search Summarizer based on the Node-RED-AI-Toolkit

![AI WebSearch Screenhot](AI-WebSearch-Screenshot.png)

This repository contains a [Node-RED](https://nodered.org/) flow which implements an AI-assisted web search. It is primarily intended to serve as an example for the [Node-RED AI Toolkit](https://github.com/rozek/node-red-ai-toolkit), but may also be used on its own.

![AI WebSearch Flow](AI-WebSearch-Flow.png)

"AI-assisted" means:

- after specifying what you are looking for, the AI constructs an efficient prompt for a web search engine (and runs a search on the web)
- after receiving a list of documents which might contain the requested information, these documents are downloaded one after the other and the AI tries to extract the information you need

The flow stops after the first successful information retrieval, i.e. it does not (yet) combine the contents of several documents.

## Installation ##

This example requires a running Node-RED instance with installed [Node-RED AI Toolkit](https://github.com/rozek/node-red-ai-toolkit). If not already done, please follow the [installation instructions for the toolkit](https://github.com/rozek/node-red-ai-toolkit#installation) before continuing.

Then, follow the [instructions found in the UIBuilder Docs](https://totallyinformation.github.io/node-red-contrib-uibuilder/#/walkthrough1?id=how-to-get-started-4-steps-to-a-data-driven-web-app) to install the UIBuilder nodes.

Now, it's time to import the contents of file [AI-WebSearch-Flow.json](https://raw.githubusercontent.com/rozek/node-red-ai-web-search/master/AI-WebSearch-Flow.json) - preferably into a new Node-RD workflow.

If necessary, you may also download a supported AI model (in GGUF format) into the toolkit's model folder.

## Usage ##

UIBuilder and the AI WebSearch flow will create and manage all files needed for the web frontend. Just navigate your browser to [http://127.0.0.1:1880/ai-web-search](http://127.0.0.1:1880/ai-web-search) where `1880` is the port number configured for Node-RED and its flow editor.

The web page should immediately receive a list with all installed AI models - just choose one and you're set.

Now enter your request. Feel free to describe your wishes (but don't expect too much right now - I'm still in the process of making prompt generation and text inference more robust and useful), then press "Sumbit".

> Nota bene: web search currently does not restrict its findings to a certain language (such as english) it may therefore happen that you get a response in a different language. However, the results may stil be impressive...

While running, the flow emits several progress messages:

- the first one informs about the actual search prompt the AI has constructed and which is now used to search the web
- additional messages show the URL of documents found by the web search which are now fetched and analyzed by the AI

Analysis is done in two steps:

1. at first, the requested information is extracted from the downloaded text document (before, HTML documents are converted into text and non-text documents such as videos are ignored)
2. unfortunately, however, the AI is not always right with its output (sometimes it just complains that no relevant information could be found). For that reason, in a second step, the extract from step 1 is checked against what was originally requested.

This additional validation step significantly enhances the quality of the final output.

## License ##

[MIT License](LICENSE.md)
