---
expanded: false
route: /extensions/roleplaying
---

# Roleplaying

Roleplaying extensions add new functionality to the storytelling capabilities of SillyTavern. They are typically highly dependent on the LLM used to structure responses and may require a considerable amount of upkeep and experimentation, but they add structure that may be incredibly desirable to people looking for a more game-like experience.

These will likely break often as stories progress and might cause significant frustration. Moreso than with any other type of extension, you will likely be on your own in terms of help if something is not working. Please do not ask the SillyTavern developers for assistance with any of these: there is literally nothing they can do.

## Extensions

- [Outfit Tracker](https://github.com/lannashelton/ST-Outfits/)
  - Adds a structured interfave for tracking character clothing
  - *Discussion for this extension was unavailable, but its use seems obvious; please contribute a link if you know one.*
- [Presence](https://github.com/leandrojofre/SillyTavern-Presence)
  - Adds flags to messages to keep track of which characters were present for a given scene, so that future LLM productions are less omniscient
    - Requires some user assistance to mark who is around at any given time and does not completely solve the problem of globally shared knowledge
  - Discord: https://discord.com/channels/1100685673633153084/1297615132289011854
- [Typing Indicator](https://github.com/SillyTavern/Extension-TypingIndicator)
  - Adds a `X is typing...` notification while message-generation is in progress, whether streaming or not, for that high-anxiety chat feeling
  - This extension is directly supported by SillyTavern and can be trusted to be compatible with the latest version
- [WTracker](https://github.com/bmen25124/SillyTavern-WTracker)
  - Introduces structured metadata for complex scenes, such as character locations and equipment, allowing the LLM to construct more-tailored descriptions
    - Prone to degredation: you may need to adjust this data with some regularity in order to have it maintain structure and accuracy
  - Discord: https://discord.com/channels/1100685673633153084/1415737449782706299
