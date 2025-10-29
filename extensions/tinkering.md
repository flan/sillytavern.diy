---
expanded: false
route: /extensions/tinkering
---

# Tinkering

Tinkering extensions have no real focus, instead exposing system internals and adding non-standard features for people who want to more directly play with LLM interactions, SillyTavern features, or other things that don't really have high portability to other people's environments. These are geared towards learning, experimentation, and rapid-prototyping.

## Extensions

- [Alternate Fields](https://github.com/nbrown725/SillyTavern-AlternateDescriptions)
  - Adds support for quick-swap values in character-card fields, allowing you to quickly experiment with prompt revisions
    - Avoids the need to use multiple copies of a card to try out different ideas
  - This extension will create non-standard cards; they should remain compatible with other systems, but sanitise them before sharing
- [Character Creator (CREC)](https://github.com/bmen25124/SillyTavern-Character-Creator)
  - Attempts to generate character cards based on events in chat history
  - Discord: https://discord.com/channels/1100685673633153084/1355543982201114746
- [Model Injection](https://github.com/aikohanasaki/SillyTavern-ModelInjection)
  - Makes the LLM model-ID accessible for use in scripting
  - Discord: https://discord.com/channels/1100685673633153084/1430637350706352178
  