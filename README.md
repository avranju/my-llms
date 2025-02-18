# My Local LLMs

This repo contains docker compose files for standing up my local LLM deployments. Right now it brings up the following containers:

- An [ollama](https://ollama.com) instance configured to use my local NVIDIA GPU.
- A [litellm](https://www.litellm.ai) instance setup to proxy LLM requests to Anthropic AI models with an Open AI API. This lets me use the latest Claude models from Open WebUI which only knows how to talk Open AI speak.
- An [Open WebUI](https://openwebui.com) instance setup to interface with the ollama service.

After bringing up the Open WebUI site, I manually configure the UI to talk to the `litellm` instance (oddly enough the URL you provide here needs to be one that works from the browser, i.e., the call to external APIs is done directly from the browser and not brokered via the Open WebUI server which means that you can't use the docker network local name).

The API key for Anthropic can be provided via `docker-compose.override.yml` file. You can copy the provided sample [docker-compose.override.yml.example](docker-compose.override.yml.example) file and make your changes.

```yaml
services:
  litellm:
    environment:
      - ANTHROPIC_API_KEY=### YOUR ANTHROPIC API KEY HERE ###
```

That's about it.
