---
route: /guides/api_model_specific/api_providers/nanogpt
---

# NanoGPT

- Last-tested SillyTavern version: 1.13.5
- Last updated: Oct 30, 2025
- Applicable platforms: N/A
- External resources required: no
- Technical skill required: none
- Safety: perfectly safe
- Expected time-commitment for a novice: 5 minutes

This is a collection of known quirks and workarounds for the [NanoGPT](https://nano-gpt.com/) platform.

This guide is neither affiliated with, nor an endorsement of, any products or services.

# Connecting NanoGPT to SillyTavern

This guide will walk you through the process of generating a NanoGPT API key and connecting it to SillyTavern for both chat and text completions.

## Getting a NanoGPT API Key

First, you need to generate an API key from your NanoGPT account.

1.  Navigate to the API section of your NanoGPT account. You can go directly to [https://nano-gpt.com/api](https://nano-gpt.com/api) or click **API** under the **Account** section on the main website.
2.  Click the **+ Create API Key** button.
3.  Assign a descriptive name to the key, such as "SillyTavern".
4.  Click the copy icon (two overlapping boxes) next to the newly generated key to copy it to your clipboard.
5.  You will paste this key into the appropriate field in SillyTavern as described below.

You can return to the API page at any time to view or copy your key again.

## Connecting to SillyTavern

You can connect SillyTavern to NanoGPT using two different modes: Chat Completions or Text Completions. For most users and general use, **Chat Completions** is the recommended method.

---

### Method 1: Chat Completions

In SillyTavern, navigate to the **API Connections** tab (the plug icon). You have two options for setting up NanoGPT for chat.

#### Using the Built-in NanoGPT Endpoint (Recommended)

This is the simplest method and is required if you want to use NanoGPT's official image generation features.

1.  In the API dropdown, select **NanoGPT**.
2.  Paste your key into the **NanoGPT API Key** field.
3.  Click **Connect**. Your key will be saved and hidden for future use.
4.  Once connected, you can select any available model from the model dropdown menu.

#### Using the Custom (OpenAI-compatible) Endpoint

This method provides more granular control over which models appear in your model list.

1.  In the API dropdown, select **Custom (OpenAI-compatible)**.
2.  In the **Custom Endpoint (Base URL)** field, enter one of the following URLs:
    *   `https://nano-gpt.com/api/v1` - The standard endpoint that shows all available NanoGPT models.
    *   `https://nano-gpt.com/api/subscription/v1` - **Recommended for subscribers.** This endpoint only shows models included in your subscription plan.
    *   `https://nano-gpt.com/api/paid/v1` - Only shows pay-per-use models.
    *   `https://nano-gpt.com/api/personalized/v1` - Shows a personalized list of models based on your NanoGPT account settings.
3.  Paste your API key into the **Custom API Key (Optional)** field.
4.  Click **Connect**.
5.  After connecting, choose a model from the dropdown menu.

> ##### Endpoint Variations
> NanoGPT offers two variations of the `v1` endpoint for specific use cases:
> *   **`v1legacy`**: Sends model reasoning in an older format. This is recommended if you are using a SillyTavern version older than 1.13.5.
> *   **`v1thinking`**: Sends all model reasoning as part of the normal response. This is generally not needed for SillyTavern.

#### Chat Completions Settings & Troubleshooting

When using NanoGPT in Chat Completions mode, you can find unique settings under the **Generation Settings** tab (sliders icon) in the **Sampling** panel.

*   **Enable Websearch**: Allows the model to access the internet to answer questions. This is only available when using the built-in **NanoGPT** endpoint and may incur an extra cost.
*   **Send inline images**: Allows you to attach and send images to vision-capable models. When this is enabled, models with vision capabilities will appear green in the model dropdown list.
*   **Request model reasoning**: Instructs NanoGPT to send the model's "thinking" process to SillyTavern. This is useful for debugging but is not needed if you use the `v1legacy` or `v1thinking` custom endpoints.

If you experience strange formatting, navigate to the **API Connections** tab and try adjusting the **Post Prompt Processing** settings. Toggling **Single user mode** or **Merge consecutive roles** can often resolve issues.

---

### Method 2: Text Completions

Text Completions mode can be more effective for SillyTavern's "Continue" function and may support a wider range of samplers for certain models.

1.  Go to the **API Connections** tab.
2.  In the top API dropdown, select **Text Completions**.
3.  In the second API dropdown, select **Custom (OpenAI-compatible)**.
4.  Enter one of the NanoGPT endpoint URLs (listed in the Chat Completions section) into the **Custom Endpoint (Base URL)** field.
5.  Paste your API key into the **Custom API Key (Optional)** field.
6.  Click **Connect**.

> **Note:** There is no UI option to request model reasoning in Text Completions mode.

#### Supported Models and Samplers

Text Completions mode is best supported on models provided by Arli AI, which include:
*   Llama 3.3 70b Finetunes (65k Context)
*   Gemma 27b Finetunes (32k Context)
*   GLM 4.5 Air Finetunes (131k Context)

When using these models, you gain access to all samplers supported by Arli AI. You must manually select them using the **Sampler Select** option. For more information on these samplers, visit the [Arli AI API Documentation](https://www.arliai.com/docs/api?lang=en).

---

### Advanced: Model Thinking Control

Instead of using in-prompt commands like `/think` or `/nothink`, NanoGPT controls a model's thinking process through specific API calls. This is handled by selecting a variant of a model name.

For example, you might see `zai-org/GLM-4.5-FP8` for a standard response and `zai-org/GLM-4.5-FP8:thinking` to enable the model's reasoning process. This allows you to control the behavior by choosing the appropriate model from the dropdown list.

Credits

- DeathStalker