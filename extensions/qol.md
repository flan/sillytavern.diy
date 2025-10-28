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
- [Prompt Inspector](https://github.com/SillyTavern/Extension-PromptInspector)
  - Adds a convenient way to observe, intercept, and modify prompt-content
    - Answers the recurring question of "what am I actually sending to the LLM?"
  - This extension is directly supported by SillyTavern and can be trusted to be compatible with the latest version
- [WorldInfo Info](https://github.com/LenAnderson/SillyTavern-WorldInfoInfo)
  - Provides a list of World Info entries that are currently applicable to the chat
    - Intercepts the results of the last exchange to enumerate active World Info sources
    - Does not predict what will happen
  - *Discussion for this extension was unavailable, but its use seems obvious; please contribute a link if you know one.*
