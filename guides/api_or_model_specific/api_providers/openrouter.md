---
route: /guides/api_or_model_specific/api_providers/openrouter
---

# OpenRouter

- Last-tested SillyTavern version: N/A
- Last updated: Oct 27, 2025
- Applicable platforms: N/A
- External resources required: no
- Technical skill required: none
- Safety: perfectly safe
- Expected time-commitment for a novice: 5 minutes

This is a collection of known quirks and workarounds for the [OpenRouter](https://openrouter.ai/) platform.

This guide is neither affiliated with, nor an endorsement of, any products or services.


## Requests to omit reasoning are not honoured

Some models produce `<think/>`-like XML blocks in their output. It has often been reported that OpenRouter does not respect SillyTavern's requests to suppress thinking because their API lacks an appropriate field.

The best-known workaround for this is to add a prompt to the end of your custom list by opening the Chat Completion panel, scrolling to the bottom, and clicking the `+` to add a new entry. Its position should be `In-chat` with a depth of `0` to ensure it appears at the end of what gets sent. Its prompt should simply be the text `/nothink`.

This does not always work, but a number of affected models respect this as a switch to disable their thinking process. If it does not help you, just delete the custom prompt.
