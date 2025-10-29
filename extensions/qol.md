---
expanded: false
route: /extensions/qol
---

# Quality of Life

Quality of Life extensions focus on creating shortcuts or usability/accessibility enhancements that are a bit too specific in nature to be included in SillyTavern's core codebase. If an extension is primarily focused on customising the UI itself, rather than adding functionality to the engine, it's most likely a QoL extension.

## Extensions

- [Bookmarks](https://github.com/aikohanasaki/SillyTavern-Bookmarks)
  - Adds the ability to bookmark arbitrary messages in chat for quick navigation
  - Discord: https://discord.com/channels/1100685673633153084/1420829230026981386
- [Character Locks](https://github.com/aikohanasaki/SillyTavern-CharacterLocks)
  - Allows many settings to be bound to chats, characters, and groups, including automatic connection-switching
  - Discord: https://discord.com/channels/1100685673633153084/1419026071684120676
- [Chat Top Info Bar](https://github.com/SillyTavern/Extension-TopInfoBar)
  - Adds a compact bar to the top of the chat window with an array of management utilities
    - Useful for managing chats at the file level and searching for text
  - This extension is directly supported by SillyTavern and can be trusted to be compatible with the latest version
- [Guided Generations](https://github.com/Samueras/GuidedGenerations-Extension)
  - Introduces features for more-directly hinting and correcting LLM responses
    - Simplifies the process of adding information before requests, before swipes/regenerations, and with impersonation
  - Reddit: https://www.reddit.com/r/SillyTavernAI/comments/1jublim/guided_generations_becomes_and_extension/
- [Input History](https://github.com/LenAnderson/SillyTavern-InputHistory)
  - Adds keyboard shortcuts for scrolling through past input messages
  - Discord: https://discord.com/channels/1100685673633153084/1188279875581255760
- [Even More Flexible Continues](https://github.com/kawaii-wolf/SillyTavern-EvenMoreFlexibleContinues)
  - Adds more options for how "Continue" behaviour works
    - Does not solve problems where models and context might not play well with blank input
  - Discord: https://discord.com/channels/1100685673633153084/1420632085651128361
- [Notebook](https://github.com/SillyTavern/Extension-Notebook)
  - Adds a `/notebook` command to quickly gain access to an integrated notebook
  - This extension is directly supported by SillyTavern and can be trusted to be compatible with the latest version
- [Prompt Inspector](https://github.com/SillyTavern/Extension-PromptInspector)
  - Adds a convenient way to observe, intercept, and modify prompt-content
    - Answers the recurring question of "what am I actually sending to the LLM?"
  - This extension is directly supported by SillyTavern and can be trusted to be compatible with the latest version
- [Prose Polisher](https://github.com/NemoVonNirgend/ProsePolisher)
  - Subjectively refines and conditions generated output to be less sloppy
  - Reddit: https://www.reddit.com/r/SillyTavernAI/comments/1llmtg5/prose_polisher_extension_guide/
- [Roadway](https://github.com/bmen25124/SillyTavern-Roadway)
  - Generates a number of story path suggestions to help add some flavour to a story
  - Reddit: https://www.reddit.com/r/SillyTavernAI/comments/1jc043c/roadway_let_llm_decide_what_you_are_going_to_do/
- [WeatherPack](https://github.com/bmen25124/SillyTavern-WeatherPack)
  - Repairs common Markdown formatting issues caused by LLMs not being attentive to syntax
  - Discrd: https://discord.com/channels/1100685673633153084/1382435483937673276
- [WorldInfo Info](https://github.com/LenAnderson/SillyTavern-WorldInfoInfo)
  - Provides a list of World Info entries that are currently applicable to the chat
    - Intercepts the results of the last exchange to enumerate active World Info sources
    - Does not predict what will happen
  - *Discussion for this extension was unavailable, but its use seems obvious; please contribute a link if you know one.*
