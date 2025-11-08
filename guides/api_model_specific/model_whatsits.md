---
order: 9999
route: /guides/api_model_specific/model_whatsits
---

# Token? Parameter? Quant?

- Last-tested SillyTavern version: N/A
- Last updated: Oct 29, 2025
- Applicable platforms: N/A
- External resources required: no
- Technical skill required: none
- Safety: perfectly safe
- Expected time-commitment for a novice: 15 minutes

This is a brief overview of common terminology surrounding LLMs that people are likely to just assume you know.

## Models

A model is the LLM created by a training process. ChatGPT, Claude, DeepSeek, and Llama are all examples of models.

They are made up of a collection of parameters, typically counted in the billions, that an execution-engine, such as [llama.cpp](https://github.com/ggml-org/llama.cpp), pumps strings and tokens into to get tokens and strings back.

Many popular models are proprietary and can only be accessed through their provider's interfaces.

Some are considered open source, or at least have open weights, a reference to their parameters having been published. This allows them to be hosted locally or by an API provider with access to a lot of computing power. Depending on their licensing terms, there may be finetuned derivatives that are specialised for a specific task, like storytelling.

### Inference and training

These refer to the two major lifecycles of any given model.

Inference is what most people do with an LLM or other similar model: they are fed information and tasked with inferring a suitable response.

Training is the process of compiling a model from a corpus of input material and an assembly methodology: it is what produces the LLM or other similar model.

## Tokens and strings

The term "token" gets thrown around a lot and, as such, is quite overloaded.

Begin by considering a few words, like "the cat is cute". Each of these words is likely one token, one digestible bit of information for the LLM to work with. If that's all you take away from this section, that's good enough. Together, they form a "string" of text, a programming term used to refer to a sequence of letters or numbers.

A typical token is around three or four Latin characters, as in our example; non-Latin language-sets may end up using a full token per character, so there is no absolute rule, and it varies from model to model.

Now, you may think there are only four tokens in our example; it's a string made up of four words, after all, but there are actually seven: the spaces, ` `, need to be encoded, too, which makes this string a sequence like [`the`, ` `, `cat`, ` `, `is`, ` `, `cute`]. There are ways to compress this, but we'll keep things simple.

When the LLM is given the text "the cat is cute", it chunks it into tokens, which it internally maps into a series of numbers, so this sentence might be represented as [10, 2, 311, 2, 14, 2, 8921]. These numbers are the real tokens, an efficient mapping from a textual form to something that the model's interfaces can quickly process.

Now consider a longer word like "spectacular". This would likely be tokenised as [`spec`, `tac`, `ular`] depending on the model's training data and methodology. In general, common prefixes, suffixes, and stems are partitioned so a single token-integer can be mapped as broadly as possible for efficiency. You don't *really* need to know this part, but it helps to understand why text streams the way it does and why vectorisation for World Info can sometimes be wonky, especially with triggers that don't have enough context to distance themselves from, or closely associate with, the parts of chat that you think might be applicable.

## Finetunes and merges

A finetune is a model that has gone through additional training or modification after its weights were released to enthusiasts. This process is computationally intensive and generally involves baking an additional corpus of text into a model, either extending its knowledge of a particular topic or, in some cases, radically changing the ways its parameters choose to respond to certain inputs, such as giving greater emphasis to material of an academic or lewd nature.

The vast majority of self-hosted models intended for roleplay purposes are some sort of finetune, while assistant and programming models tend to be unmodified.

Early on, the process of finetuning was poorly understood, often resulting in models that unintentionally behaved very strangely, whether in a quirky or very broken manner, and, as such, there is a lot of material that suggests they should be avoided. This is all highly situational and many of the more prominent finetuners have become quite adept at controlling the process.

Merges are a related concept, typically taking two or more models that have been finetuned from the same common ancestor (though this is not always the case) and running them through a process that either rebalances their weights to try to get some attributes from tuning one to come through in the productions of another, or by focusing on the layers themselves, duplicating (for emphasis), eliminating, or exchanging them. The results are often more than a little unpredictable, but they can be very unique for roleplay purposes.

### Retrieval-Augmented Generation (RAG)

This is a concept related to finetuning that comes up more often in business-like contexts: RAGs are effectively a searchable database of material that an LLM can subjectively load into its working context to give it information that is very domain-specific without needing to be told to look up a certain document or topic. The trade-off is that any information loaded from a RAG consumes tokens in context.

A finetune bakes this information into the model itself so it has no additional evaluation cost, but it has the downside of the material becoming inextricably part of the model's data.

## Parameters

In simple terms, the number of parameters reflects how "intelligent" a model may be, though advancements in technology and introduction of new assessment techniques allow smaller models to compete with their older, larger counterparts. A model can be thought of as an enormous tree, where you start on the ground, at the trunk, and flip a coin to decide whether to climb a branch to the left or right, then flip that coin to go left or right again all the way until you reach a leaf at the end.

In LLM terms, each decision-point is a node in a graph and each leaf is an output-token. Every coin-flip is a complex calculation based on the way that model was trained and every input-token that has gone through this process before. Yes, this means that, in order to get the next "he said" in your story, billions of coins must be flipped thousands of times.

Each parameter is typically one of a few varieties:

- Weights, which are used to  determine the importance of any given node in moving towards the next token to be produced
- Biases, which contribute to traversal of nodes for the current input-token, refined as layers are traversed
- Activations, which consider the current token, its biases, and the weight, to decide which node will be reached next

Though primitive, the [Markov chain](https://en.wikipedia.org/wiki/Markov_chain) is very important to probability research and it may help to illustrate the basic concept of what is involved if this piques your interest.

A 70-billion parameter model will have 70,000,000,000 nodes like these, with some subset of each being used to determine what token comes next in the output-stream appearing on your screen. In a naive search, all 70-billion parameters must also be considered each time, which is why the concept of memory-bandwidth is so important to LLM inferencing.

A 70-billion parameter model will not have a bigger vocabulary than a 7-billion parameter model, but it will likely be better-able to pick up on nuance and patterns in code or natural language because there are so many more opportunities for its training data to guide production of the next token towards something suitable and to then build upon that to choose a better-focused follow-up over and over until the response is complete.

## Quantisation

Have you ever heard an old MP3 file and wondered why cymbals sound like distorted waterfalls? Or watched a low-bitrate movie a friend obtained through less-than-legal means? If so, great, you've experienced lossy compression. If not, uh, just try to think of how if you round a number up or down, you throw away the decimal part in exchange for "good enough" simplicity.

Quantisation is similar to that: it is a form of lossy compression, where some precision is lost, but you can still recognise and mostly appreciate the thing you're observing. You're not going to mistake the number `6` for a `5` or `7`, but it's no longer `6.251614789`, and that makes you as sad as it makes me.

For simplicity, we're going to ignore floating-point numbers since the basic concept is the same, though the math itself differs. (If you care about the distinction, you already know enough to skip this part)

At full sixteen-bit resolution, which is how most models are published, each parameter occupies two bytes of data, encoding up to 65,536 possible values, which allows for a lot of precision in choosing which node to reach next as the activation-chain passes through the parameter-tree. Arguably, way more than is typically ever needed.

At eight-bit quantisation, typically written as `q8`, the amount of data is cut in half, to one byte, which reduces the number of possible values to 256. This is a *much* smaller number, but given the complexity of a model, with billions of parameters, and each one not having nearly enough transition possibilities to justify 16-bit precision in most circumstances, this is still more than enough to encode for virtually everything, which is why most people consider `q8` to be "full quality".

`q7` is often skipped because it doesn't provide any meaningful trade-off benefit.

`q6` is often considered the ideal compression-point: with the ability to encode 64 options, the most likely transitions are strongly retained and some less-likely possibilities are kept, as well. Statistical outliers start to get discarded at this point, but for creative storytelling, there is effectively no perceivable loss.

`q5` is a good middle-ground option. Not much to say: slower than `q4`, only a little less precise than `q6` in most cases.

`q4` is generally the quality/speed sweet-spot, with the ability to encode `16` discrete values. Compared to the sixty-five thousand that were shed since 16-bit, that seems downright tiny, but most of the time, only the most statistically important paths are traversed anyway, so there is still enough diversity in evaluation to get interesting, reasonably-reliable results; for creative writing, the loss in precision doesn't hurt too much.

Below `q4`, though, things start to get murky: `q3` still allows for a bit of a range in possibilities, but by `q1`, it's effectively a weighted coin-flip. For very big models, `q1` might still be more intelligent than a much tinier `q8` just because of the statistical significance of having so many more possible transitions, but the incidence of repetition and slop will increase significantly as quantisation becomes more severe: those detailed cymbals will turn into grating noise, souring the harmony of the now-enormous orchestra playing a much more complex composition.

### Anxious optimisation note

You might be aware of things like your GPU's ability to work with matrices in `int4`, `int8`, `fp4`, `fp8`, and `fp16` modes. For LLM inferencing, this isn't super-important, since memory-bandwidth is the most significant bottleneck by far, but `q8` will map to `int8` and smaller sizes are packed with an interleaving strategy for speed, typically being expanded to the next-highest size before evaluation, so don't worry about trying to make the numbers align.

## GGUF, GGML, and SafeTensors

These are encoding formats for models. If you are not self-hosting, that's all you really need to know.

SafeTensors can be thought of as uncompressed data, like a `.wav` file that you might get from ripping a CD: full precision, no imposed compression, and very big. These typically come in sixteen-bit floating-point precision, which means that, roughly speaking, each parameter takes two bytes of data to encode. Most GPUs from the past decade do well with this format, but it consumes a ton of memory. Very few people actually run them outside of specialised hosting providers.

GGUF, the GPT-Generated Unified Format, is the successor to GPT-Generated Markup Language, both more-compact, specialised ways of repacking SafeTensor data. GGUF is notable and extremely popular because it provides standardisation for the practice of quantisation.

### Computer science history note

The name "SafeTensors" comes from the roots of a lot of AI research being done with the [Python programming language](https://www.python.org/), which had a long-deprecated method of serialising data alongside code in a process referred to as "pickling", like preserving pickles or eggs, which gave rise to the extension "PickleTensors", with "Tensors" being a mathematical concept commonly used in machine-learning. While easy to use and convenient, pickled data can do malicious things when unpickled, so a successor that ensured the data would be inert upon unpickling was created and deemed "safe".

## iMatrix

This is both very complex and very simple. There's enough complexity in this document already.

Some models may be advertised as being "iMatrix" (or "i1") and these typically have far more downloads. This is because they are generally better: their quanitsation process involves additional analysis to determine the most important weights and gives them more presence in the compressed model. This is much slower to produce and a little slower to evaluate (though nothing compared to the memory-bandwidth problem), so as long as the slightly larger size isn't a problem for your VRAM, just go for iMatrix.

As for other flags like `K` and `IQ`, which refer to refer to how blocks of weights are grouped or split, this can generally be ignored in favour of picking the largest usable model from a given quantised set. `S`, `M`, and `L` mean the same thing they do for shirt-sizes: small, medium, large, and are really just there for min/maxing when every byte and clock-cycle matters.

## Layers, context, and memory-footprint

When an LLM is constructed, it is partitioned into "layers". If you can run the entire model in VRAM (or system RAM), this shouldn't be much of a consideration. But if you need to split models across multiple GPUs or between a GPU and system RAM, it becomes a very important concept.

As each output-token is evaluated, the context being processed must be available for both analysis and production, and this is done one layer at a time. This means that, for *each token produced*, the working context, which is typically around 1 GiB per 2k tokens (due to another process, known as "vectorisation", that ascribes semantic and contextual significance to the token itself as it is evaluated, well beyond `311` representing "cat"), must be relocated to the same memory-pool as the next stage of execution. This can introduce a very severe bandwidth limitation that might not have been considered before: the PCIe bus. This need to move context around is why there is such a sharp drop-off in token-generation speed when more than one layer is located in either pool and why it may be faster to only use system memory than to split layers with a GPU.

## Mixture of Experts (MoE)

This is a strategy for partitioning a dense model into a collection of much smaller models, each trained to be specialised in a specific aspect of the source corpus.

The name is, as of 2025, still aspirational: the "experts" aren't really subject-matter experts the way a human might think of the term, as like having specialisation in physics, chemistry, or biology, but rather in parts of the token-production chain: punctuation, sentence clauses, conjunction, location, numbers. A routing component sits in front, determining which "experts" to engage for the next production step (which may be as few as one or a complex sequence involving repeated invocation of the same sub-model).

The MoE flow works similarly to layers, passing the context through each, with the most significant difference being that, because only a subset of the whole model is required to generate each token, the process can run several times faster than with a linear dense model.

Theoretically, the potential quality should be comparable to a dense model. In practice, it varies significantly based on training, partitioning, and routing strategies.
