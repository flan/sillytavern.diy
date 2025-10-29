---
expanded: false
route: /extensions/worldinfo
---

# World Info

World Info extensions focus primarily on the management of Lorebooks and other means of conditionally injecting information into the prompt sent to an LLM when generating a response.

## Extensions

- [Lorebook Ordering](https://github.com/aikohanasaki/SillyTavern-LorebookOrdering)
  - Allows for granular control over lorebook priority for cases where available context is (or should be) limited
  - Discord: https://discord.com/channels/1100685673633153084/1418367705014337628
- [Memory Books](https://github.com/aikohanasaki/SillyTavern-MemoryBooks)
  - Semi-automatically generates lorebooks based on ranges of a chat, allowing "memories" to be cleanly partitioned and added to context in longer stories
    - Greatly reduces the amount of effort required to keep a story coherent; also has support for using lorebooks to guide the story through "Side Prompts"
    - Is not magic: requires a bit of setup and understanding on the user's part
  - Reddit: https://www.reddit.com/r/SillyTavernAI/comments/1nik127/st_memory_books/
- [WIBulk Mover](https://github.com/leandrojofre/SillyTavern-WI-Bulk-Mover)
  - Copy, move, or delete any number of entries across lorebooks
  - Discord: https://discord.com/channels/1100685673633153084/1356581029409980467
- [World Info Locks](https://github.com/aikohanasaki/SillyTavern-WorldInfoLocks)
  - Allows policies to be defined to automatically load lorebooks and configure various properties to rapidly configure chats
  - Discord: https://discord.com/channels/1100685673633153084/1391959172052156540
- [World Info Recommender (WREC)](https://github.com/bmen25124/SillyTavern-WorldInfo-Recommender/)
  - Attempts to generate World Info (lorebooks) based on events in chat history
  - Discord: https://discord.com/channels/1100685673633153084/1353430925861589052
