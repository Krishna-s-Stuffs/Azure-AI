# AI-901: Microsoft Azure AI Fundamentals — Detailed Study Notes

**Official skills outline as of April 15, 2026** (source: Microsoft Learn). AI-901 replaced AI-900, which retired June 30, 2026. Passing score: 700/1000. Requires basic Python familiarity and awareness of Azure resources, REST APIs, SDKs, and CLIs — a step up from AI-900, which needed no coding at all.

**Key shift from AI-900:** AI-900 asked you to *describe* what Azure AI services do. AI-901 asks you to *actually build* small AI apps/agents using **Microsoft Foundry** (Foundry portal + Foundry SDK). Expect some "what would this code/config do" style questions, not just terminology.

---

## Domain Weights

| Domain | Weight |
|---|---|
| **1. Identify AI concepts and capabilities** | 40–45% |
| **2. Implement AI solutions by using Microsoft Foundry** | 55–60% |

Domain 2 is now the majority of the exam — hands-on Foundry skills matter more than pure theory.

---

# DOMAIN 1: Identify AI Concepts and Capabilities (40–45%)

## 1.1 Principles of Responsible AI

Same six pillars as AI-900 — still foundational, appears across both domains.

| Principle | Meaning | Scenario cue |
|---|---|---|
| **Fairness** | AI treats all groups equitably; actively test for and mitigate bias | "A hiring model favors one gender over another" |
| **Reliability & Safety** | Consistent performance, including rare/edge cases; rigorous testing before deployment | "A medical AI tool must be tested extensively before clinical use" |
| **Privacy & Security** | Protect personal data; secure the system against misuse/attack | "Anonymizing training data"; "restricting access to model endpoints" |
| **Inclusiveness** | AI systems benefit and are usable by people of all abilities, backgrounds | "App supports screen readers and multiple languages" |
| **Transparency** | Users understand how/why an AI reached a decision; disclose AI use | "Providing explanations for a loan denial"; "labeling AI-generated content" |
| **Accountability** | Humans/organizations remain responsible for AI outcomes; governance in place | "A governance board reviews model behavior before release" |

**Exam trap:** Fairness = *no biased outcomes*. Inclusiveness = *broad accessibility of the system*. Don't confuse the two.

## 1.2 AI Model Components and Configurations

### How generative AI models work
- **Large Language Models (LLMs)** are built on the **Transformer architecture**.
- **Tokenization** — input text is broken into tokens (words or sub-words) before processing.
- **Embeddings** — tokens are converted into numeric vectors that capture semantic meaning; similar meanings → similar vectors.
- **Attention mechanism** — lets the model weigh which tokens matter most relative to each other, regardless of position in the sequence — this is what lets transformers handle long-range context well.
- **Next-token prediction** — generative models work by predicting the most probable next token given everything before it, repeated to build full responses.
- **Encoder vs. decoder:**
  - **Encoder-only** (e.g., BERT-style) — good for understanding/classification tasks
  - **Decoder-only** (e.g., GPT-style) — good for generation tasks
  - **Encoder-decoder** — good for transformation tasks like translation/summarization
- **Multimodal models** — accept/generate more than one content type (text + image, text + audio), e.g., GPT-4o-class models. AI-901 leans heavily on multimodal models because Foundry tasks use them for vision and speech.

### Choosing an appropriate model based on capabilities
Considerations tested:
- **Task fit** — does the model support text, vision, audio, or multiple modalities?
- **Context window size** — how much input (tokens) the model can consider at once
- **Cost vs. performance tradeoffs** — smaller/cheaper models for simple tasks vs. larger models for complex reasoning
- **Latency requirements** — smaller models respond faster, useful for real-time apps
- **Specialization** — some models are tuned for code, reasoning, or specific domains
- **Licensing/openness** — proprietary (e.g., OpenAI models via Azure OpenAI) vs. open-source models available in the Foundry Model Catalog

### Model deployment options and configuration parameters
- **Deployment options in Foundry:**
  - **Serverless API / pay-as-you-go endpoints** — no infrastructure management, billed per use
  - **Managed compute / real-time endpoints** — dedicated compute, more control, needed for high-throughput or custom scenarios
  - **Batch deployment** — for large-scale, asynchronous, non-real-time processing
- **Key configuration parameters to know:**
  - **Temperature** — controls randomness/creativity; low = more deterministic/focused, high = more varied/creative
  - **Max tokens** — caps the length of the generated response
  - **Top P (nucleus sampling)** — controls diversity by limiting token choices to a cumulative probability mass
  - **Frequency/presence penalties** — reduce repetition in output
  - **Stop sequences** — strings that tell the model to stop generating

## 1.3 Identify AI Workloads

### Common AI workload categories (know examples of each)
- **Generative AI** — creating new text, images, audio, or code (e.g., drafting content, generating illustrations)
- **Agentic AI** — AI systems (**agents**) that can autonomously plan, use tools/functions, and take multi-step actions toward a goal, not just respond to a single prompt. New emphasis vs. AI-900.
- **Text analysis** — extracting insight from written text (see 1.3.1 below)
- **Speech** — recognizing and synthesizing spoken language
- **Computer vision** — extracting information from images/video
- **Information extraction** — pulling structured data out of unstructured sources (documents, forms, images, audio, video) — powered in Foundry by **Content Understanding**

### 1.3.1 Text Analysis Techniques
| Technique | Description |
|---|---|
| **Keyword/key phrase extraction** | Identifies the most important words/phrases representing the main points of text |
| **Entity detection (NER)** | Identifies and categorizes named entities — people, organizations, locations, dates, quantities, etc. |
| **Sentiment analysis** | Classifies text as positive, negative, neutral, or mixed, typically with confidence scores |
| **Summarization** | Condenses longer text into a shorter version — **extractive** (pulls key existing sentences) vs. **abstractive** (generates new, paraphrased summary text) |

### 1.3.2 Speech Recognition and Synthesis
- **Speech recognition (speech-to-text)** — converts spoken audio into text; supports real-time (streaming) and batch (pre-recorded file) transcription
- **Speech synthesis (text-to-speech)** — converts text into natural spoken audio; supports prebuilt neural voices and custom voice creation
- **Speech translation** — real-time translation of spoken input into another language (text or speech output)
- Relevant capability: **responding to spoken prompts using a deployed multimodal model** — some modern multimodal models can take audio input directly rather than requiring a separate speech-to-text step first

### 1.3.3 Computer Vision and Image-Generation Models
| Capability | Description |
|---|---|
| **Image classification** | Assigns one label to a whole image |
| **Object detection** | Detects multiple objects and draws bounding boxes with labels |
| **Semantic segmentation** | Classifies every pixel into a category — most granular |
| **OCR** | Extracts printed/handwritten text from images |
| **Facial detection/analysis** | Locates faces and extracts attributes (subject to Responsible AI restrictions on identification use cases) |
| **Image generation** | Generative models (e.g., DALL·E-class, diffusion models) create new images from text prompts |
| **Multimodal vision models** | Models that can interpret an image passed alongside a text prompt and respond about its content (visual question answering, image captioning) |

### 1.3.4 Extracting Information from Text, Images, Audio, and Video
This ties directly to **Azure AI Content Understanding** (a core Foundry Tools capability new to this exam):
- Extracts **structured data** from **unstructured** multimodal content
- Works across **documents/forms** (invoices, receipts, contracts), **images**, **audio**, and **video**
- Typical outputs: key-value fields, tables, entities, timestamps/transcripts, classifications
- Distinct from simple OCR — Content Understanding can combine multiple modalities and apply schemas/templates to extract exactly the fields you define

---

# DOMAIN 2: Implement AI Solutions by Using Microsoft Foundry (55–60%)

**Microsoft Foundry** (successor branding to Azure AI Studio / Azure AI Foundry) is the unified platform for building, testing, and deploying generative AI apps and agents. This domain tests whether you know the *workflow* of building with it, not just what it is.

## 2.1 Implement Generative AI Apps and Agents Using Foundry

### Prompt engineering — system and user prompts
- **System prompt/message** — sets the model's role, tone, constraints, and behavior for the whole session (e.g., "You are a helpful customer support agent for a software company. Only answer questions about billing.")
- **User prompt** — the actual end-user input/question
- **Effective prompting techniques:**
  - Be specific and give context
  - Use **few-shot examples** (show sample input/output pairs) to guide format
  - Break complex tasks into steps (**chain-of-thought style prompting**)
  - Define output format explicitly (e.g., "respond in JSON with fields X and Y")
  - **Grounding** — supply the model with specific, current, relevant data (e.g., via retrieval) so answers are based on real facts instead of only the model's trained knowledge; reduces **hallucination** (confident but false/fabricated output)

### Deploying and interacting with a model in the Foundry portal
Typical workflow:
1. Browse the **Model Catalog** in Foundry (models from Microsoft, OpenAI, Meta, Mistral, and other providers)
2. Select and **deploy** a model to an endpoint (choosing a deployment type — serverless/pay-as-you-go vs. managed compute)
3. Use the **Foundry portal's chat playground** to test prompts interactively and tune parameters (temperature, max tokens, etc.) before writing code
4. Review responses, adjust the system prompt, and iterate

### Building a lightweight chat client with the Foundry SDK
- The **Foundry SDK** lets you call deployed models from your own code (Python is the emphasized language for this exam)
- A minimal chat client typically: authenticates to the Foundry project/endpoint → sends a system message + user message → receives and displays the model's response → optionally loops for multi-turn conversation, appending prior turns to maintain context
- Know that conversation history must be resent each turn since these APIs are stateless by default (unless a specific "threads"/session feature is used)

### Creating and testing a single-agent solution in the Foundry portal
- An **agent** = a model configured with a specific **role/instructions**, plus optionally **tools/functions** it can call (e.g., a search tool, a calculator, a custom API) and/or **knowledge sources** it can retrieve from
- Building an agent in the portal typically involves:
  1. Defining the agent's instructions (its system prompt/persona and task)
  2. Attaching **tools** (function calling) so the agent can take actions beyond just generating text
  3. Optionally attaching a **knowledge source** (files, a search index) for grounding
  4. Testing the agent in a chat/playground interface to confirm it invokes tools correctly and produces grounded answers
- **Agentic AI** = the model doesn't just answer — it can decide *which* tool to call and *when*, sometimes chaining multiple steps to reach a goal

### Building a lightweight client application for an agent
- Similar to the chat client, but the client code needs to also handle **tool-call events**: when the agent's response indicates it wants to invoke a function, the client code executes that function and returns the result to the agent to continue reasoning
- Understand this basic loop: **user input → agent reasons → agent may call a tool → tool result returned to agent → agent produces final response**

## 2.2 Implement AI Solutions for Text and Speech Using Foundry

- **Text analysis app** — a lightweight app calling a Foundry-deployed model (or a Language service resource within Foundry Tools) to perform key phrase extraction, sentiment analysis, entity recognition, or summarization on user-supplied text, then display results
- **Responding to spoken prompts using a multimodal model** — feeding **audio input directly** to a multimodal model (rather than manually transcribing first) so the model can understand spoken questions and generate a response — reflects newer multimodal capabilities
- **Azure Speech in Foundry Tools** — building an app using Speech capabilities (speech-to-text, text-to-speech, translation) accessible from within the Foundry ecosystem, e.g., a voice assistant that transcribes user speech, sends the text to a model, and speaks back the response

## 2.3 Implement AI Solutions with Computer Vision and Image-Generation Using Foundry

- **Interpreting visual input via a multimodal model** — passing an image alongside a text prompt to a deployed multimodal model so it can describe, analyze, or answer questions about the image (visual Q&A, image captioning use cases)
- **Creating new visual outputs with generative models** — using an image-generation model (deployed via Foundry) to produce new images from text prompts; understand basic parameters like prompt wording, image size/resolution, and style guidance
- **Building a lightweight vision-capable app** — combining the above into a simple client: user uploads an image and/or types a prompt → app sends both to the model → displays the generated text or image response

## 2.4 Implement AI Solutions for Information Extraction Using Foundry (Content Understanding)

**Azure AI Content Understanding** (within Foundry Tools) is a major new focus area. Know these four extraction scenarios:

| Source | What Content Understanding does |
|---|---|
| **Documents and forms** | Extracts structured fields (key-value pairs, tables, line items) from invoices, receipts, contracts, applications — using a defined schema/template |
| **Images** | Extracts structured information from image content (e.g., reading labels, extracting fields from a photographed form, classifying visual content) |
| **Audio and video** | Extracts transcripts, speaker information, key moments/timestamps, and summaries from audio/video content |
| **Building an app with information extraction** | A lightweight client that submits a file (document/image/audio/video) to a Content Understanding analyzer and displays the structured output (fields, values, confidence scores) |

**Exam trap:** Content Understanding is broader than OCR — OCR only reads text; Content Understanding applies a schema across modalities to output structured, labeled data (e.g., "Invoice Number," "Total Due," "Vendor Name" as distinct fields), and can do this on images, audio, and video too, not just documents.

---

## Quick-Reference: Frequently Confused Concepts

| A | B | Difference |
|---|---|---|
| **Fairness** | **Inclusiveness** | No biased outcomes vs. broad system accessibility |
| **OCR** | **Content Understanding** | Reads raw text vs. extracts structured, schema-based fields across multiple modalities |
| **Agent** | **Basic chat model call** | Agent can invoke tools/functions and take multi-step actions; a plain chat call just returns text |
| **System prompt** | **User prompt** | Sets persistent behavior/role vs. the specific ask in a given turn |
| **Grounding** | **Fine-tuning** | Supplying live/relevant data at inference time vs. retraining/adjusting model weights on custom data |
| **Serverless/pay-as-you-go deployment** | **Managed compute deployment** | No infra to manage, billed per call vs. dedicated compute you provision and manage |
| **Temperature (low)** | **Temperature (high)** | More deterministic/focused output vs. more random/creative output |
| **Speech-to-text (separate step)** | **Multimodal audio input** | Manually transcribe then send text to model vs. model directly consumes audio |

---

## Practice Questions

Test yourself before checking answers at the bottom.

**Q1.** A company wants its AI chatbot to explain *why* it denied a customer's request, in plain language the customer can understand. Which Responsible AI principle does this primarily address?
A) Inclusiveness
B) Transparency
C) Accountability
D) Fairness

**Q2.** You are configuring a generative model deployment and want the output to be highly consistent and deterministic (minimal randomness) across repeated runs with the same prompt. Which parameter should you set low?
A) Max tokens
B) Top P
C) Temperature
D) Frequency penalty

**Q3.** Which of the following best describes an "agent" in the context of Microsoft Foundry?
A) A model that only classifies text into fixed categories
B) A model configured with instructions and the ability to invoke tools/functions to take multi-step actions toward a goal
C) A synonym for any deployed generative model
D) A dataset used to fine-tune a model

**Q4.** A retail company wants to automatically extract the vendor name, invoice number, and total amount from thousands of scanned invoices in different layouts. Which Foundry capability is best suited for this?
A) Azure AI Content Understanding
B) Sentiment analysis
C) Semantic segmentation
D) Speech synthesis

**Q5.** What is the primary purpose of "grounding" a generative AI model's responses?
A) To make responses shorter
B) To reduce the model's computational cost
C) To supply relevant, up-to-date data so answers are based on facts, reducing hallucination
D) To convert text input into embeddings

**Q6.** Which deployment option in Foundry would you choose for a low-traffic prototype where you don't want to manage or provision any infrastructure?
A) Managed compute / real-time endpoint
B) Batch deployment
C) Serverless / pay-as-you-go endpoint
D) On-premises deployment

**Q7.** A developer wants their chat client to maintain context across multiple turns of conversation using the Foundry SDK. What must the client application do?
A) Nothing — the API automatically remembers all prior turns
B) Resend the full relevant conversation history with each new request, since the API is stateless by default
C) Only send the very first message each time
D) Use a separate model for each turn

**Q8.** Which text analysis technique would best identify that a paragraph mentions "Microsoft," "Seattle," and "March 2026" as distinct categorized items?
A) Sentiment analysis
B) Entity detection (NER)
C) Summarization
D) Keyword extraction

**Q9.** A team wants their multimodal model to directly answer a spoken question from an uploaded audio clip, without a separate transcription step. What capability enables this?
A) Semantic segmentation
B) A multimodal model accepting audio input directly
C) Object detection
D) Batch deployment

**Q10.** What distinguishes abstractive summarization from extractive summarization?
A) Abstractive picks existing sentences verbatim; extractive generates new paraphrased text
B) Extractive picks existing sentences verbatim; abstractive generates new paraphrased text
C) They are the same technique with different names
D) Abstractive only works on images

**Q11.** Which principle of Responsible AI is most directly addressed by conducting extensive edge-case testing of a self-driving car's AI system before deployment?
A) Transparency
B) Reliability and Safety
C) Inclusiveness
D) Privacy and Security

**Q12.** In the Foundry Model Catalog, what is a key reason you might choose a smaller model over a larger one for a specific task?
A) Smaller models are always more accurate
B) Smaller models typically offer lower latency and lower cost for simpler tasks
C) Smaller models support more modalities
D) Smaller models cannot be deployed via Foundry

---

### Answer Key
1. **B** — Transparency (explaining decisions to users)
2. **C** — Temperature (low = deterministic)
3. **B** — Agent = instructions + tool use for multi-step actions
4. **A** — Azure AI Content Understanding (structured extraction across varied layouts)
5. **C** — Grounding supplies real, relevant data to reduce hallucination
6. **C** — Serverless/pay-as-you-go = no infrastructure management
7. **B** — Must resend history; APIs are stateless by default
8. **B** — Entity detection identifies and categorizes named entities like organizations, places, dates
9. **B** — Direct audio input to a multimodal model
10. **B** — Extractive = verbatim existing sentences; Abstractive = new generated text
11. **B** — Reliability and Safety (consistent performance including edge cases)
12. **B** — Lower latency/cost tradeoff for simpler tasks

---

## Exam Tips
- This exam expects you to reason about **workflows** (deploy → prompt → test → build client) not just define terms — review the actual steps of using the Foundry portal and SDK.
- Basic Python literacy is assumed — you should recognize what a simple API call to send a prompt and receive a response looks like, even if you don't need to write it from scratch.
- **Agentic AI and Content Understanding are the biggest new content areas** vs. AI-900 — spend extra time here.
- Old AI-900 material on standalone "Azure AI Vision," "Azure AI Language," etc. as separate resources is still conceptually useful (Domain 1 overlaps a lot with AI-900), but the *implementation* focus has shifted to accessing these capabilities through Foundry.
- Use Microsoft's free official practice assessment on **AI Skills Navigator** before the real exam.
