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

### What's the sweet-spot?

The answer to this always depends on what hardware you have, but in general, the following rule-of thumb works well:

quant | what this means
--- | ---
`q8` | virtually identical to the original in practice; use this if your hardware can fit the model and necessary context and you don't care too much about speed
`q7` | doesn't exist, statistically no point
`q6` | if you're obsessed with not sacrificing quality, but have slight space-constraints or would like just a little more speed, this is practically as good as `q8` for any model over the 6-8B range and only a very slight degradation below that
`q5` | if you're okay with some very minor compromises for better speed, on any model above around 20B, this will be about as good as `q6`
`q4` | this should usually be the lowest to accept outside of experimentation, generally good enough, but hallucinations and lost trains of thought become more common below this point
`q3`-`q1` | there are only two reasons to consider these: either they're necessary to do something like run a 70B model instead of a 24B (more parameters means more opportunity for a model to regain focus if it starts to drift) or you're a researcher; all other things about models being equal (which is rarely the case), `q1` 70B will be capable of producing more insightful output than a `q8` 24B, though you may need to scrutinise or regenerate it a bit more often

`q4_k_m` through `q5_k_m` are often considered good enough for actual production use for text-based tasks on models above 20B. For coding applications, a tiny loss in precision can be significant, but for storytelling and summarisation, the differences will be like using a synonym or a different idiom.

Rephrased: `q6` if you can manage it, `q4` if you can't, and `q1` only if it lets you just barely run a much bigger model than you could normally. The incidences of repetition and slop increase significantly as quantisation becomes more severe: those detailed cymbals will turn into grating noise, souring the harmony of the now-enormous orchestra playing a much more complex composition.

### What does iMatrix mean?

iMatrix ("importance matrix", often just written as `i` or `i1`) formats are generally preferred if available (they sometimes are not, due to the increased preparation costs), reflected in their typically higher numbers of downloads. They are a little bigger and run just a tiny bit slower, but make up for it by providing more statistical information around key decision-points in the model, allowing a smaller quantisation to perform better than it otherwise typically would.

### What does the `K` mean?

`K` and its often-omitted siblings `0` (default) and `1` (uncommon) refer to how blocks of data are encoded.

In short, `K` is usually best if, like with [iMatrix](#what-does-imatrix-mean), you can fit it within your hardware constraints. `0` is the default and is fine if `K` is not available. `1` is a simpler form of what `K` does and is better than `0`. You can usually just pick the biggest model that works for your setup and not worry about it.

#### What do these *really* mean?

Naively, it might seem like taking a 16-bit value, which, ignoring the decimal nature of FP16, can encode 65,535 discrete numbers and reducing it to 4-bit value, which can only encode 16, means that there is no way a `q4` quantisation can come anywhere close to the accuracy of the original model, but that ignores both that there are a finite number of transitions between any given nodes in an LLM and that these numbers form part of [complex matrices](https://en.wikipedia.org/wiki/Tensor). Because groups of numbers are used together to perform calculations, the losses in precision from any one data-point are largely reduced. The actual math involved is a bit beyond a simple quick-start guide, but if you recall high school linear algebra, many related concepts apply.

Where the `K` comes in is that it denotes that groups of numbers used for these calculations are quantised together, with shared relative origin, scaling, and range parameters, allowing that small number of values to more precisely represent a narrow (or wide) spectrum of data, like when a line-graph is shown zoomed-in, making small differences look massive, even when they're only 0.05% apart from each other in absolute terms.

`1` is a simpler approach, encoding groups of numbers with less granular metadata; it's still good, but it trades accuracy for faster processing speed, but LLMs are typically bandwidth-constrained, rather than compute-limited, making this a bit unimportant.

`0` has still less metadata: even faster but no notable accuracy benefit.

### What about the other letters?

`XS`, `S`, `M`, `L`, `XL`, and others refer to the degree of compression within the given quantisation target. Since compression is lossy, choosing the largest one that works for your hardware is the right solution; dropping down a quantisation level to go with `L` instead of `S` is not a good idea, unless the publisher specifically says there is a quirk that justifies it.

### Anxious optimisation note

You might be aware of things like your GPU's ability to work with matrices in `int4`, `int8`, `fp4`, `fp8`, and `fp16` modes. For LLM inferencing, this isn't super-important, since memory-bandwidth is the most significant bottleneck by far, but `q8` will map to `int8` and smaller sizes are packed with an interleaving strategy for speed, typically being expanded to the next-highest size before evaluation, so don't worry about trying to make the numbers align.

## GPTQ, GGUF, GGML, and SafeTensors

These are encoding formats for models. If you are not self-hosting, that's all you really need to know.

SafeTensors can be thought of as uncompressed data, like a `.wav` file that you might get from ripping a CD: full precision, no imposed compression, and very big. These typically come in sixteen-bit floating-point precision, which means that, roughly speaking, each parameter takes two bytes of data to encode. Most GPUs from the past decade do well with this format, but it consumes a ton of memory. Very few people actually run them outside of specialised hosting providers.

GGUF, the GPT-Generated Unified Format, is the successor to GPT-Generated Markup Language, both more-compact, specialised ways of repacking SafeTensor data. GGUF is notable and extremely popular because it provides standardisation for the practice of quantisation.

GPTQ is the successor to GGUF, though both are likely to co-exist for a while. It introduces more-efficient packing strategies and better separation of parameter-types, making it possible to have more variable weight quantisations alongside variable-precision activations, so that further compression may be achieved without notable additional loss.

The GPTQ format refers to model files that have been compressed using the GPTQ (Generative Pre-trained Transformer Quantization) algorithm, a post-training quantization (PTQ) method. This format is primarily used to reduce the size of large language models (LLMs) and accelerate inference, making them runnable on consumer-grade GPUs with limited VRAM. 
Key Characteristics
Weight-Only Quantization: The core of the GPTQ format is quantizing the model's weights (typically in the linear layers) to very low bit-widths, such as 4-bit (INT4), 3-bit, or even 2-bit. Activations are usually kept in a higher precision, like FP16, during inference.

### EXL and MLX

These are alternate model encoding strategies for specific hardware implementations: EXL for nVidia and MXL for Apple Silicon.

If available for the model you want to use, they are likely to offer better performance than the more-generic GPTQ and GGUF formats, but they are typically only published for high-profile research and assistant uses.

### Computer science history note

The name "SafeTensors" comes from the roots of a lot of AI research being done with the [Python programming language](https://www.python.org/), which had a long-deprecated method of serialising data alongside code in a process referred to as "pickling", like preserving pickles or eggs, which gave rise to the extension "PickleTensors", with "Tensors" being a mathematical concept commonly used in machine-learning. While easy to use and convenient, pickled data can do malicious things when unpickled, so a successor that ensured the data would be inert upon unpickling was created and deemed "safe".

## Layers, context, and memory-footprint

When an LLM is constructed, it is partitioned into "layers". If you can run the entire model in VRAM (or system RAM), this shouldn't be much of a consideration. But if you need to split models across multiple GPUs or between a GPU and system RAM, it becomes a very important concept.

As each output-token is evaluated, the context being processed must be available for both analysis and production, and this is done one layer at a time. This means that, for *each token produced*, the working context, which varies in size from model to model, must be relocated to the same memory-pool as the next stage of execution. This can introduce a very severe bandwidth limitation that might not have been considered before: the PCIe bus. This need to move context around is why there is such a sharp drop-off in token-generation speed when more than one layer is located in either pool and why it may be faster to only use system memory than to split layers with a GPU.

### Vectorisation and memory use

Vectorisation is a critical part of how LLMs work, essential to the processes that give them semantic awareness and emergent properties.

Simplified, it expands a token, like the representation of "cat", from `311` into hundreds or thousands of different numbers, referred to as "dimensions", that each encode some aspect of what they token seems to represent in relation to the text as a whole, and it is this collection of vectors that gets tuned by the biasing process as a model is evaluated, eventually collapsing back into a token like "dog" for output.

As of 2025, tools such as https://huggingface.co/spaces/NyxKrage/LLM-Model-VRAM-Calculator may be used to estimate how much memory a model will use in practice relative to its context-size. (If the model you want to use is restricted in some way, selecting a related finetune or another model from the same base family is usually fine.)

## Mixture of Experts (MoE)

This is a strategy for partitioning a dense model into a collection of much smaller models, each trained to be specialised in a specific aspect of the source corpus.

The name is, as of 2025, still aspirational: the "experts" aren't really subject-matter experts the way a human might think of the term, as like having specialisation in physics, chemistry, or biology, but rather in parts of the token-production chain: punctuation, sentence clauses, conjunction, location, numbers. A routing component sits in front, determining which "experts" to engage for the next production step (which may be as few as one or a complex sequence involving repeated invocation of the same sub-model).

The MoE flow works similarly to layers, passing the context through each, with the most significant difference being that, because only a subset of the whole model is required to generate each token, the process can run several times faster than with a linear dense model.

Theoretically, the potential quality should be comparable to a dense model. In practice, it varies significantly based on training, partitioning, and routing strategies.
