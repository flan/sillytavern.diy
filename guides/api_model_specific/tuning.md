---
order: 10000
route: /guides/api_model_specific/tuning
---

# Parameter tuning

- Last-tested SillyTavern version: N/A
- Last updated: Oct 27, 2025
- Applicable platforms: N/A
- External resources required: no
- Technical skill required: none
- Safety: perfectly safe
- Expected time-commitment for a novice: 10 minutes

This is a brief overview of how parameters and sampling values work with LLMs for some common use-cases.

Rather than providing any model-specific guidance, this is more of an overview of the concepts to help you understand how to adjust values for your own uses.

This guide focuses on the parameters most likely to cause problems for newer users of SillyTavern and its focus is on Chat Completion due to the prevalence of hosted APIs moving away from Text Completion; Text Completion-specific settings will be marked as such with `[Text Completion]` in their headings. For a more comprehensive list, see [the official documentation](https://docs.sillytavern.app/usage/common-settings/).

## Foreword

A note on numbers: many programmers use values of `0.0` to refer to 0% and `1.0` to refer to 100% because it makes math easier and more efficient. When you see `1.0`, it is actually a very big value, not the immediate successor to `0`.

## Temperature

Temperature is a modifier on how much randomness, or how exaggerated, the output of an LLM should be.

Low temperature values, approaching 0, will produce very similar output when given the same input (note that SillyTavern builds its input using a lot of things, including your current chat's history, so this does not specifically refer to your last message).

Higher temperatures cause the model to produce tokens that may be less-related to those that came before in the response, creating a less-focused response. Pushing it too high will cause a model to devolve into incoherent gibberish including random use of tokens from other languages.

Most models are trained with a value of `1.0` being suitable for general use. Programming and business use-cases generally prefer low temperatures, while creative writing and roleplaying often benefit from higher values.

When adjusting temperature, starting with increments of `0.1` is recommended. Dialing things in at `0.01` granularity does make a difference, since that's still modifying probabilities by a full percentage point.

Fine-tuned models, those specifically trained for roleplaying purposes, generally have their own recommended ranges, which may be below `1.0` depending on how well they should adhere to their training.

## Frequency Penalty

Frequency Penalty discourages the LLM from repeating tokens in its output. Non-zero values can affect how natural the prose seems, but it may come at the cost of making the model seem stupider by omitting information that simply cannot be well-presented without a common pre-amble or coda in the target language.

It works based on the number of times the tokens have appeared in recent context (including the ongoing generation), making it a proportionally weighted value.

## Presence Penalty

Presence Penalty functions much the same as Frequency Penalty, except it looks at the context as an absolute: rather than considering how many times a token-sequence has occurred or their proximity to the text being generated, it looks at the entire context as considers everything on a `pass`/`fail` basis, which makes it much more strict and likely much less useful for storytelling.

## Top P

Top P works in tandem with Temperature, reducing the set of candidate tokens that can follow the last-generated bit of text. For each token an LLM produces, it enumerates a list of candidates that can follow, assigning them a probability score; Temperature adds some randomness to these probabilities, and Top P sorts them from most-probable to least-probable, then throws away some of the least-likely options, making output more predictable.

While the default vlaue of `1.0` (which does _not_ mean "consider everything") is reasonable for most models, if your chat sometimes ends up changing languages or going in a very strange direction, it could be because the LLM considered that "猫" is a possible option for "cat" in your story, even though it was scored quite low, but a roll of the dice made it the next token, and then something else outside of English was much more likely to follow. In case this is happening to you, try lowering it in steps of `0.025`

## Min P

Min P acts as a filter on which tokens can enter consideration for Top P and Typical P by stating the lowest probability that a token must have to be allowed into the set. If a token only has a 1% chance of being a viable successor and Min P is set to `0.05`, it will just be discarded immediately.

## Typical P `[Text Completion]`

Typical P works with Top P to help filter the list of candiate successor-tokens prior to scoring. The default value of `1.0` does not cause anything to be prematurely discarded, while lower values reduce variance relative to an "average" point, discarding the highest-probability and lowest-probability options, which may increase the stability of production in exchange for making it more bland, but also less predictable for common phrases in the target language.

It should probably not be changed from `1.0` for storytelling purposes; slightly lower values may make sense for exploring ideas in an assistant capacity.

## Top K

Top K is sort of an alternative to Top P: where Top P filters the pool of candidates based on cumulative probability, Top K filters the pool by considering the `k` top-ranked options, providing a fixed number of choices.

## Top A `[Text Completion]`

Top A is sort of an alternative to Min P where the least-likely candidate tokens are dropped from the pool based on how far away they are from the most-likely candidate.

## Context Size

Context Size is maximum number of tokens that may be sent to the LLM. SillyTavern employs some strategies to format your chat, including custom prompts and card information, to fit within this window. Notably, it always includes essential fields like the system prompt and the message you just entered, and conditionally includes information like lorebook entries, optional prompts, and as many chat-history entries as it can manage to hit this target.

A *very* common beginner mistake is to set your context as high as possible. When it comes to maintaining an LLM's focus on subject-matter, less is usually better. As this number grows, not only will you be spending more time or money on input-token processing cost, but you are also asking the LLM to search through many more pages of often-meaningless flavour text, like "he said", conjunctions, and *so many* "the"s. Having some of this is good for maintaining a consistent writing style, but having too many will cause your important plot-points to become lost in the sea of data, and it's all just text to an LLM.

As of late 2025, it is strongly recommended that you start with a context-size of 16k (`16384`) and scale it up (or sometimes down) in steps of 2k (`2048`) up to a maximum of 32k (`32768`). Smaller models usually maintain better focus with smaller contexts, while larger models can sometimes find something useful in a large window, but your overall experience will be better with numbers like these.

While there is a case for large contexts, such as searching a knowledgebase or looking for patterns in code, those typically have a lot of structure for an LLM agent to work with; a creative story does not.

Let mechanisms like SillyTavern's built-in "Summarize" extension, or some other popular World Info extensions, help to keep your story on track, and help them out with custom lorebooks or Author's Note entries.

## Max Response Length

Max Response Length does _not_ strictly tell the LLM how many tokens to produce (hinting in your prompts with mechanisms like `produce {{random::2,3,3,3,4}} paragraphs of text` is the best way to do that as of 2025). Rather, it constrains how many tokens SillyTavern will accept and display. Combined with mechanisms like SillyTavern's ability to detect and remove unfinished sentences, this can help trim messages at a more sensible length for certain chat-styles (instant-messaging simulation, for example), but it is often a good idea to set it to a value around `300` for more chat-like interactions, `500` for longer-format narrative stories, and `1000` or more for assistant uses. There is no real penalty for setting it too high, except that a rambling LLM might continute for way too long before being interrupted.

## Prompt Size `[implicit]`

Prompt Size is not a configurable field, but it is a potential cause of confusion.

LLMs work by receiving context as input, in the form of a series of tokens, then filling out the rest of the context with tokens that should follow, the "intelligent auto-complete" nature of their operation.

SillyTavern uses the following general approach to partition the Context Size:

*Prompt Size = Context Size - Max Response Length*

Content | Limit
--- | ---
System Prompt and other similar data | Reproduced exactly as written
World Info | Whatever is set to be triggered (up to a default limit of 25% of Prompt Size, highest-priority first)
Persona and Character info | Reproduced exactly as written
Chat History | As much as fits in remaining Prompt Size
User-submitted message | Reproduced exactly as written
Buffer for response | Max Response Length

This means that setting an enormous Max Response Length will eat into the Prompt Size available for World Info and Chat History, since it is subtracted before those resource calculations are performed.

## Multiple swipes per generation

This causes the LLM to produce multiple candidate responses every time you submit a message, to speed up the swiping process.

It defaults to `1`. This is good. Leave it there until you're absolutely sure you know how your model behaves and whether you actually are a swiper.

Setting it to higher numbers and not using it just wastes money, and many APIs have an upper limit (often `1`), with an error-response being produced if the request from SillyTavern exceeds this target.
