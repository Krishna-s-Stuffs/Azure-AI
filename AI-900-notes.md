<div align="center">

# 🧠 AI-900 — Microsoft Azure AI Fundamentals
### Complete Exam Notes (Detailed Edition)

![Exam](https://img.shields.io/badge/Exam-AI--900-blue) ![Status](https://img.shields.io/badge/Status-Retired%20June%202026-lightgrey) ![Pass Score](https://img.shields.io/badge/Passing%20Score-700%2F1000-success) ![Source](https://img.shields.io/badge/Source-Microsoft%20Learn-0078D4)

</div>

> [!IMPORTANT]
> **AI-900 officially retired on June 30, 2026** and was replaced by **AI-901**. These notes cover the final AI-900 skills outline (effective May 2, 2025 — five domains: AI workloads & considerations, ML fundamentals, computer vision, NLP, generative AI). Useful for background knowledge, older course material, or comparison against AI-901 — but you can no longer register for or sit this exam. If you need the current, registrable exam, see the separate AI-901 notes.

> [!NOTE]
> No coding was tested on AI-900. It's a pure terminology-and-concepts exam: what each Azure AI service does, what it's called, and when to use it over a similar-sounding alternative. Microsoft explicitly says "data science and software engineering experience are not required."

---

## 📑 Table of Contents

- [Domain Weights](#-domain-weights)
- [1. AI Workloads and Considerations](#-1-ai-workloads-and-considerations-1520)
- [2. Machine Learning Fundamentals](#-2-machine-learning-fundamentals-1520)
- [3. Computer Vision Workloads](#-3-computer-vision-workloads-on-azure-1520)
- [4. NLP Workloads](#-4-natural-language-processing-nlp-workloads-on-azure-1520)
- [5. Generative AI Workloads](#-5-generative-ai-workloads-on-azure-2025--largest-domain)
- [Every Azure AI Service at a Glance](#-every-azure-ai-service-at-a-glance)
- [Quick-Reference: Frequently Confused Pairs](#-quick-reference-frequently-confused-pairs)
- [Practice Questions](#-practice-questions)
- [Exam Tips Checklist](#-exam-tips-checklist)

---

## 📊 Domain Weights

| Domain | Weight |
|---|:-:|
| 1. AI Workloads & Considerations | `15–20%` |
| 2. Machine Learning Fundamentals | `15–20%` |
| 3. Computer Vision Workloads | `15–20%` |
| 4. NLP Workloads | `15–20%` |
| 5. Generative AI Workloads | `20–25%` |

---

## 🔷 1. AI Workloads and Considerations (15–20%)

### 1.1 Common AI Workload Types

- 👁️ **Computer vision** — extracting information from images/video (classification, detection, OCR, facial analysis)
- 📝 **Natural Language Processing (NLP)** — understanding/generating text and speech (sentiment, key phrases, entities, translation, speech-to-text)
- 📄 **Document processing / Knowledge mining** — extracting structured info from unstructured documents (forms, invoices, receipts) via **Azure AI Document Intelligence** (formerly Form Recognizer), plus **Azure AI Search** for indexing/searching large content repositories
- 🤖 **Generative AI** — models that create new content (text, images, code) based on prompts, e.g. GPT models via Azure OpenAI
- 🎙️ **Anomaly detection** — identifying unusual patterns or outliers in data (e.g., fraud detection, equipment failure prediction) — via **Azure AI Anomaly Detector**
- 🗣️ **Conversational AI** — chatbots and virtual agents that hold multi-turn conversations, built with **Azure AI Bot Service** combined with Language service's CLU/Question Answering

<details>
<summary><b>📌 Real-world workload examples the exam likes to test</b> (click to expand)</summary>

| Scenario | Workload type |
|---|---|
| Reading vehicle license plates from traffic camera photos | Computer vision (OCR) |
| Automatically tagging photos uploaded to a social app | Computer vision (image classification/tagging) |
| Summarizing thousands of customer support tickets | NLP (summarization) |
| Detecting fraudulent credit card transactions | Anomaly detection |
| Extracting line items from scanned receipts | Document processing / knowledge mining |
| A chatbot answering FAQs from a knowledge base | Conversational AI (Question Answering + Bot Service) |
| Generating product descriptions from bullet points | Generative AI |
| Detecting whether a manufactured part has a defect | Computer vision (object detection or classification) |

</details>

### 1.2 Responsible AI — Six Guiding Principles

Microsoft's Responsible AI framework, formalized as part of its **Responsible AI Standard**. Know all six and be able to distinguish them in scenario questions — this is one of the most heavily tested single topics on the exam.

![The six Responsible AI principles: fairness, reliability and safety, privacy and security, inclusiveness, transparency, accountability](images/responsible_ai.svg)

| Principle | What it means | Example question cue | Typical mitigation |
|---|---|---|---|
| ⚖️ **Fairness** | AI systems treat all groups equitably; no bias based on gender, race, age, etc. | *"loan approval model performs worse for one demographic"* | Fairlearn / Responsible AI dashboard bias analysis; balanced training data |
| 🛡️ **Reliability & Safety** | System performs consistently and safely, including edge cases and rare scenarios | *"self-driving car must handle rare road conditions"* | Rigorous testing, human-in-the-loop review for high-stakes decisions |
| 🔒 **Privacy & Security** | Protect user data; secure the system from attack or misuse | *"encrypting patient data used to train a model"* | Data anonymization, access controls, encryption at rest/in transit |
| 🌍 **Inclusiveness** | AI empowers everyone, including people with disabilities and diverse backgrounds | *"app supports screen readers, multiple languages"* | Accessibility testing, diverse representation in design/testing |
| 🔍 **Transparency** | Users understand how/why decisions are made; disclose AI involvement | *"explaining why a loan was denied"* | Model interpretability tools, clear disclosure that content is AI-generated |
| 👤 **Accountability** | People/organizations remain responsible for AI systems; governance frameworks exist | *"a team is designated to oversee model behavior"* | Governance boards, audit trails, designated human oversight roles |

> [!WARNING]
> **Common trap:** Fairness vs. Inclusiveness — Fairness = *no bias/discrimination in outcomes*; Inclusiveness = *broad accessibility of the system itself*. A model that works equally well for men and women is fair. An app that works for someone who is blind is inclusive. They can overlap but test different things.

> [!TIP]
> A second common trap: **Reliability & Safety vs. Accountability**. Reliability/Safety is about the *system's technical behavior* under stress or edge cases. Accountability is about *who is responsible* when something goes wrong — governance, not engineering.

### 1.3 Guidelines for Responsible Generative AI (specific sub-skill)

Microsoft also tests a **4-stage responsible generative AI lifecycle** used when building generative AI features:

1. **Identify potential harms** — brainstorm ways the system could produce harmful, inaccurate, or inappropriate output for the intended use case
2. **Measure the presence of harms** — test the system with diverse inputs to see how often and how severely harms occur
3. **Mitigate the harms** — apply techniques at multiple layers: the model itself (choosing/fine-tuning), a safety system (content filters, blocklists on top of the model), the application/UX (design choices like disclaimers, input limits), and positioning/documentation (transparent communication of limitations)
4. **Operate responsibly** — deploy with a plan: phased rollout, ongoing monitoring, user feedback mechanisms, and an incident-response plan

> [!TIP]
> If a question describes content filters, blocklists, or prompt shields layered on top of a model, that's the **mitigate** stage, specifically the "safety system" layer.

---

## 🔶 2. Machine Learning Fundamentals (15–20%)

### 2.1 Core ML Techniques

![Regression predicts a continuous value with a best-fit line, classification separates points into categories with a decision boundary, clustering groups similar points without labels](images/ml_techniques.svg)

- **Regression** — predicts a **continuous numeric value** (e.g., house price, temperature, stock price)
- **Classification** — predicts a **category/class label** (e.g., spam vs. not spam)
  - **Binary classification** (2 classes) vs. **multiclass classification** (3+ classes)
- **Clustering** — groups similar data points **without labeled outcomes** (unsupervised) — e.g., customer segmentation, anomaly grouping

> [!TIP]
> **Key distinction:** Regression/Classification = **supervised learning** (labeled data — you know the "right answer" for training examples). Clustering = **unsupervised learning** (no labels — the algorithm finds structure on its own).

<details>
<summary><b>📈 How model performance is evaluated (often glossed over — worth knowing)</b> (click to expand)</summary>

- **For regression models:**
  - **MAE (Mean Absolute Error)** — average absolute difference between predicted and actual values
  - **RMSE (Root Mean Squared Error)** — like MAE but penalizes larger errors more heavily
  - **R² (R-squared / coefficient of determination)** — how well the model explains variance in the data; closer to 1 is better
- **For classification models:**
  - **Confusion matrix** — a table comparing predicted vs. actual classes (true positives, false positives, true negatives, false negatives)
  - **Accuracy** — proportion of correct predictions overall (can be misleading with imbalanced classes)
  - **Precision** — of everything predicted positive, how much was actually positive
  - **Recall** — of everything actually positive, how much was correctly predicted
  - **F1 score** — harmonic mean of precision and recall, useful when you need a single balancing metric

</details>

### 2.2 Deep Learning & Transformer Architecture

<details>
<summary><b>🧩 Deep learning and neural network basics</b> (click to expand)</summary>

- **Deep learning** — uses multi-layered **neural networks** to model complex patterns; needs large data and compute (often GPUs)
- **Neural network basics:** input layer → hidden layer(s) → output layer; nodes ("neurons") have weights that are adjusted via training
- **Activation functions** — introduce non-linearity so the network can learn complex patterns (e.g., ReLU, sigmoid) — know the term exists, exact math not required
- **Backpropagation** — the process by which a neural network adjusts its weights based on prediction error, working backward from the output layer
- **Convolutional Neural Networks (CNNs)** — a neural network architecture specialized for image data; underlies most computer vision models
- **Recurrent Neural Networks (RNNs)** — older architecture designed for sequential data (like text or time series); largely superseded by Transformers for NLP but the term may still appear

</details>

<details>
<summary><b>🔀 Transformer architecture</b> (click to expand)</summary>

Foundation of modern language models (GPT, BERT):
- **Attention mechanism** — lets the model weigh the importance of different words/tokens relative to each other, regardless of position
- **Encoder** — builds a representation/understanding of input text
- **Decoder** — generates output text based on that representation
- Encoder-only (e.g., BERT — understanding tasks), decoder-only (e.g., GPT — generation tasks), encoder-decoder (translation-style tasks)
- **Tokenization** — breaking text into tokens (words/sub-words) before processing
- **Embeddings** — numeric vector representations capturing semantic meaning; words/phrases with similar meaning end up with similar vectors — this is the basis for semantic search and similarity comparisons

</details>

### 2.3 Core ML Concepts

| Term | Meaning |
|---|---|
| **Features** | Input variables used to make predictions (e.g., square footage, bedrooms) |
| **Labels** | The known output/answer you're trying to predict (e.g., actual sale price) — only present in supervised learning |
| **Training dataset** | Data used to teach/fit the model |
| **Validation dataset** | Separate data used to tune the model and check it isn't overfitting, before final evaluation |
| **Test dataset** | Held-out data to evaluate final model performance (not always distinguished from validation on the exam — focus on train vs. validation) |
| **Overfitting** | Model learns the training data too well (including its noise) and performs poorly on new/unseen data |
| **Underfitting** | Model is too simple to capture the underlying pattern, performing poorly even on training data |

### 2.4 Azure Machine Learning Capabilities

<details>
<summary><b>⚙️ AutoML, Designer, and compute options</b> (click to expand)</summary>

- **Automated ML (AutoML)** — automatically tries multiple algorithms/hyperparameters to find the best-performing model with minimal manual coding; you supply the data and the task type (classification/regression/forecasting), AutoML handles the rest and ranks candidate models by a chosen metric
- **Azure ML Designer** — drag-and-drop, no-code/low-code visual interface for building ML pipelines by connecting modules (data prep → train → score → evaluate) on a canvas
- **Notebooks** — for those who want full code control (Python/R) within the Azure ML workspace, using Jupyter-style notebooks
- **Compute options:**
  - **Compute Instances** — a dev workstation (VM) for authoring, running notebooks
  - **Compute Clusters** — scalable clusters for training jobs (autoscale, can scale to 0 nodes when idle to save cost)
  - **Inference Clusters** — for deploying models, typically Azure Kubernetes Service (AKS)-based
  - **Attached Compute** — link existing external compute resources (e.g., an existing VM or Databricks cluster) into the workspace
- **Data assets/Datastores** — connections to Azure Blob Storage, Data Lake, SQL databases, etc., so pipelines can read data without hardcoding credentials
- **Azure ML Workspace** — the top-level container resource that organizes all these assets (experiments, models, compute, datastores) together

</details>

<details>
<summary><b>📦 Model management & deployment</b> (click to expand)</summary>

- Register trained models in a **model registry** for versioning and tracking lineage
- Deploy as a **real-time endpoint** (immediate, low-latency predictions — e.g., a web service called per request) or a **batch endpoint** (large-scale, scheduled/async predictions over big datasets)
- **Managed online endpoints** — Azure-managed infrastructure for real-time deployment without manually configuring AKS
- **Responsible AI dashboard** — a suite of tools in Azure ML for fairness assessment, model explainability/interpretability, error analysis, and causal analysis
- **MLOps** — the discipline of applying DevOps practices (CI/CD, versioning, monitoring) to ML model lifecycles; Azure ML integrates with Azure DevOps/GitHub Actions for this

</details>

---

## 🔷 3. Computer Vision Workloads on Azure (15–20%)

### 3.1 Types of Computer Vision Solutions

![Comparison of image classification, object detection, and semantic segmentation: classification gives one label for the whole image, object detection draws bounding boxes with labels, segmentation classifies every pixel](images/cv_comparison.svg)

| Solution | What it does |
|---|---|
| **Image classification** | Assigns a label/category to an entire image (e.g., "cat" or "dog") |
| **Object detection** | Identifies **multiple objects** in an image and draws **bounding boxes** around each, with labels |
| **Semantic segmentation** | Classifies **every pixel** into a category (more granular than bounding boxes) |
| **Optical Character Recognition (OCR)** | Extracts printed or handwritten text from images/documents |
| **Facial detection** | Locates human faces in an image (bounding box around face) |
| **Facial analysis** | Extracts attributes from detected faces (age estimate, emotion, head pose) — note: some facial-analysis capabilities (e.g., emotion, gender inference) have been restricted by Microsoft's Responsible AI policies; facial *recognition* (identity verification) requires special access via a Limited Access application |
| **Image analysis (tagging/captioning)** | Automatically generates descriptive tags or a natural-language caption for an image |
| **Spatial analysis** | Analyzes video streams to understand people's movement/presence in physical space (e.g., counting people, checking social distancing zones) |

> [!WARNING]
> **Common trap:** Object detection = bounding box + label per object. Image classification = ONE label for the whole image. Segmentation = pixel-level, most precise.

### 3.2 Azure Tools/Services for Computer Vision

<details>
<summary><b>👁️ Azure AI Vision</b> (formerly Computer Vision) — click to expand</summary>

- **Image analysis** — tags, captions/dense captions, detected objects, brand detection, adult/racy content moderation, detecting image color scheme, generating "smart crop" thumbnails
- **OCR / Read API** — extracts text from images and PDFs, supports both printed and handwritten text, multiple languages
- **Spatial analysis** — container for people-counting and zone-based analytics from video feeds
- Prebuilt, general-purpose — no training required, works out of the box on common object/scene categories

</details>

<details>
<summary><b>🎨 Azure AI Custom Vision</b> — click to expand</summary>

- Train your **own custom** image classification or object detection model using your own labeled images (no ML expertise needed)
- Two project types: **Image Classification** (multiclass or multilabel) and **Object Detection**
- Workflow: upload images → tag/label them → train → evaluate (precision, recall, mAP) → publish as an endpoint
- Useful when the built-in Azure AI Vision categories don't cover your specific domain (e.g., identifying specific manufacturing defects, specific plant species)
- Requires a minimum number of labeled images per tag to train (general guidance: at least 15, more for better accuracy)

</details>

<details>
<summary><b>😀 Azure AI Face service</b> — click to expand</summary>

- **Face detection** — locates faces in an image, returns bounding box + optional attributes
- **Face verification** — "is this the same person?" — one-to-one comparison
- **Face identification** — "who is this person?" — one-to-many comparison against a known group (Limited Access, requires application/approval due to privacy/misuse risk)
- Strict Responsible AI gating: Microsoft has restricted or removed capabilities like emotion and gender classification from general availability due to fairness/accuracy concerns and potential for misuse

</details>

<details>
<summary><b>📄 Azure AI Document Intelligence</b> (formerly Form Recognizer) — click to expand</summary>

- Extracts structured data (key-value pairs, tables, text) from documents like invoices, receipts, ID documents, business cards
- **Prebuilt models** for common document types (invoice, receipt, ID, business card, W-2, etc.)
- **Custom models** trainable on your own document layouts
- **Read model** — general OCR extraction, similar to Azure AI Vision's Read API but positioned specifically for document workflows
- Straddles both the computer vision domain and the "document processing/knowledge mining" workload category from Domain 1

</details>

---

## 🔶 4. Natural Language Processing (NLP) Workloads on Azure (15–20%)

### 4.1 Common NLP Tasks

| Task | Description |
|---|---|
| **Key phrase extraction** | Pulls out the main talking points/phrases from text |
| **Entity recognition (NER)** | Identifies and categorizes entities — people, places, organizations, dates, quantities |
| **Sentiment analysis** | Determines whether text is positive, negative, neutral, or mixed (returns confidence scores per sentiment, plus per-sentence scores) |
| **Language detection** | Identifies which language the text is written in, returns a confidence score and ISO language code |
| **Language modeling** | Predicting/generating likely sequences of words; underlies autocomplete, generation |
| **Speech recognition (speech-to-text)** | Converts spoken audio into text |
| **Speech synthesis (text-to-speech)** | Converts text into natural-sounding spoken audio |
| **Translation** | Converts text/speech from one language to another |
| **PII detection** | Identifies and can redact Personally Identifiable Information (names, phone numbers, SSNs, etc.) in text |
| **Text summarization** | Extractive (pulls key existing sentences) or abstractive (generates new, paraphrased summary) |

### 4.2 Azure Tools/Services for NLP

<details>
<summary><b>💬 Azure AI Language service</b> — click to expand</summary>

- Key phrase extraction, entity recognition, sentiment analysis, language detection, PII detection, summarization
- **Conversational Language Understanding (CLU)** — build custom natural-language understanding models for chatbots/apps; you define **intents** (what the user wants to do) and **entities** (relevant pieces of information), then train the model on sample **utterances**
- **Question Answering** — extract Q&A pairs from documents/FAQs to power a knowledge base; returns a confidence score for each matched answer, and you can set a confidence threshold below which the bot says "I don't know"
- **Custom Text Classification** — train a model to sort documents into your own custom categories
- **Custom Named Entity Recognition (Custom NER)** — train a model to recognize entity types specific to your domain, beyond the built-in categories

</details>

<details>
<summary><b>🎙️ Azure AI Speech service</b> — click to expand</summary>

- **Speech-to-text** — real-time (streaming microphone/audio) and batch (pre-recorded files) transcription
- **Text-to-speech** — supports prebuilt neural voices (many languages/styles) and **Custom Neural Voice** (train a unique branded voice — Limited Access due to potential for misuse/deepfakes)
- **Speech Translation** — real-time translation of spoken input into another language, output as text or synthesized speech
- **Speaker recognition** — verifying or identifying who is speaking (also Limited Access)
- **Intent recognition** — combining speech-to-text with language understanding to determine what a spoken command is asking for
- Accessible via **Speech Studio** (no-code testing UI) or the **Speech SDK**/REST APIs for integration into applications

</details>

<details>
<summary><b>🌐 Azure AI Translator</b> — click to expand</summary>

- Dedicated **text** translation service supporting 100+ languages
- Distinct from Speech Translation, which handles **audio** input/output
- Supports custom translation models (Custom Translator) trained on domain-specific terminology
- Can detect the source language automatically if not specified

</details>

> [!WARNING]
> **Common trap:** Azure AI Language (text-based NLP tasks) vs. Azure AI Translator (dedicated translation) vs. Azure AI Speech (audio in/out). A scenario mentioning "audio" almost always points to Speech; "translate this document" points to Translator; anything else text-analytical (sentiment, entities, key phrases) points to Language.

---

## 🔷 5. Generative AI Workloads on Azure (20–25% — largest domain)

### 5.1 Generative AI Fundamentals

- **Generative AI** — models that create **new** content (text, images, audio, code) rather than just classifying/analyzing existing data
- **Large Language Models (LLMs)** — trained on massive text corpora; generate human-like text; built on the Transformer architecture
- **Small Language Models (SLMs)** — smaller, more efficient models (e.g., Phi family) — faster and cheaper, good for narrower tasks or resource-constrained environments, tradeoff is generally less broad capability than a large frontier model
- **Prompt engineering** — crafting inputs (prompts) to guide model output effectively
  - **System message** — sets the model's behavior/persona/context for a whole conversation
  - **Few-shot prompting** — including examples in the prompt to guide the desired output format (vs. **zero-shot**, no examples given)
  - **Grounding** — providing the model with specific, relevant, up-to-date data (e.g., via retrieval) so it answers based on real facts rather than only its trained knowledge — reduces hallucination
- **Retrieval Augmented Generation (RAG)** — a pattern where relevant documents/data are retrieved from a knowledge source (often a vector search index) and injected into the prompt as context before the model generates a response — the standard way to "ground" an LLM on your own data
- **Embeddings** — numeric vector representations of text used to measure semantic similarity; power the retrieval step in RAG (find documents whose embeddings are "close" to the query's embedding)
- **Hallucination** — when a generative model produces plausible-sounding but factually incorrect or fabricated content
- **Fine-tuning** — further training a pretrained model on a smaller, task-specific dataset to specialize its behavior (different from grounding/RAG, which doesn't change the model's weights)
- **Common generative AI use cases:** content creation/summarization, chatbots/copilots, code generation, image generation, data transformation, semantic search

### 5.2 Responsible AI for Generative AI (specific considerations)

- Risk of **hallucination** and misinformation
- Risk of generating **harmful, biased, or offensive content**
- Need for **content filtering** and moderation (Azure OpenAI has built-in content filters that can flag/block categories like violence, hate, sexual content, self-harm)
- **Copyright and intellectual property** concerns from training data and generated output
- Transparency: disclosing when content is AI-generated
- See the **4-stage responsible generative AI lifecycle** in section 1.3 above — it applies directly here

### 5.3 Azure Generative AI Services

<details>
<summary><b>🏗️ Azure AI Foundry</b> (formerly Azure AI Studio) — click to expand</summary>

- Unified platform to explore, build, test, and deploy generative AI apps and agents
- **Model catalog** — browse and deploy a wide range of foundation models (Microsoft, OpenAI, Meta, Mistral, and other open-source models) in one place
- Provides tools for **prompt flow** (visually designing and testing multi-step LLM workflows), evaluation (testing model output quality/safety), and responsible AI safeguards (content filters, monitoring)
- Supports connecting your own data sources for RAG-style grounding

</details>

<details>
<summary><b>🤖 Azure OpenAI Service</b> — click to expand</summary>

- Microsoft's Azure-hosted access to OpenAI's models (GPT-4/GPT family for text, embeddings models, DALL·E for images, Whisper for speech-to-text) with enterprise security, compliance, and regional availability
- **Content filtering** — built-in moderation to catch harmful content in prompts/completions, configurable severity thresholds
- Supports **fine-tuning** and **grounding with your own data** (Retrieval-Augmented Generation style patterns), often paired with **Azure AI Search** as the vector index
- **DALL·E** — text-to-image generation model available through the service
- Deployment requires creating a **model deployment** within an Azure OpenAI resource, choosing a specific model version and capacity

</details>

<details>
<summary><b>🔎 Azure AI Foundry Model Catalog</b> — click to expand</summary>

- Central hub to compare/deploy foundation models from multiple providers, not just OpenAI
- Lets you filter by task type, modality, and provider, and deploy directly from the catalog

</details>

> [!WARNING]
> **Common trap:** Azure AI Foundry = the overall platform/workspace; Azure OpenAI Service = specifically OpenAI's models hosted on Azure; Model Catalog = the model-browsing feature inside Foundry.

---

## 🗂️ Every Azure AI Service at a Glance

A consolidated cheat-sheet mapping every Azure AI service mentioned across the exam to its one-line purpose — useful for last-minute review.

| Service | One-line purpose |
|---|---|
| **Azure AI Vision** | General-purpose image analysis, tagging, captioning, OCR |
| **Azure AI Custom Vision** | Train your own image classification/object detection model |
| **Azure AI Face** | Face detection, verification, (limited) identification |
| **Azure AI Document Intelligence** | Extract structured data from forms/documents |
| **Azure AI Language** | Text analytics — sentiment, entities, key phrases, CLU, Question Answering |
| **Azure AI Speech** | Speech-to-text, text-to-speech, speech translation |
| **Azure AI Translator** | Text translation between languages |
| **Azure AI Search** | Indexing and searching large content repositories (incl. vector/semantic search) |
| **Azure AI Anomaly Detector** | Detect outliers/unusual patterns in time-series data |
| **Azure AI Bot Service** | Framework for building and deploying conversational bots |
| **Azure Machine Learning** | End-to-end platform for building/training/deploying custom ML models |
| **Azure AI Foundry** | Unified platform for building/deploying generative AI apps and agents |
| **Azure OpenAI Service** | Enterprise access to OpenAI models (GPT, DALL·E, embeddings, Whisper) |

---

## 🧭 Quick-Reference: Frequently Confused Pairs

- **Classification vs. Clustering** — Classification needs labeled data (supervised); clustering finds groups without labels (unsupervised)
- **Object Detection vs. Semantic Segmentation** — bounding boxes vs. pixel-level classification
- **Azure AI Language vs. Azure AI Translator** — general NLP tasks vs. dedicated translation
- **Azure AI Vision vs. Azure AI Custom Vision** — pre-built general model vs. train-your-own custom model
- **Training dataset vs. Validation dataset** — fit the model vs. tune/check the model
- **Azure AI Foundry vs. Azure OpenAI Service** — broad platform vs. OpenAI-specific service within it
- **Face verification vs. Face identification** — one-to-one match vs. one-to-many search (identification is Limited Access)
- **Grounding vs. Fine-tuning** — supplying live/relevant data at inference time (no weight change) vs. retraining the model's weights on custom data
- **Extractive vs. Abstractive summarization** — pulling existing sentences verbatim vs. generating new, paraphrased text
- **Precision vs. Recall** — of predicted positives, how many were right (precision) vs. of actual positives, how many were caught (recall)

---

## ✅ Practice Questions

<details>
<summary><b>Q1.</b> A dataset has no labeled outcomes, and the goal is to group similar customers together. Which ML technique applies?</summary>

A) Regression&nbsp;&nbsp;B) Classification&nbsp;&nbsp;C) Clustering&nbsp;&nbsp;D) Object detection

**Answer: C — Clustering** (unsupervised, no labels)
</details>

<details>
<summary><b>Q2.</b> Which computer vision solution draws a bounding box around each detected item and labels it?</summary>

A) Image classification&nbsp;&nbsp;B) Object detection&nbsp;&nbsp;C) Semantic segmentation&nbsp;&nbsp;D) OCR

**Answer: B — Object detection** (bounding boxes + labels)
</details>

<details>
<summary><b>Q3.</b> Which Azure service would you use specifically to train your own custom image classifier using your own labeled photos?</summary>

A) Azure AI Vision&nbsp;&nbsp;B) Azure AI Custom Vision&nbsp;&nbsp;C) Azure AI Face&nbsp;&nbsp;D) Azure Machine Learning Designer

**Answer: B — Azure AI Custom Vision** (train-your-own model)
</details>

<details>
<summary><b>Q4.</b> What is the difference between a training dataset and a validation dataset?</summary>

A) They are the same thing
B) Training data fits the model; validation data tunes/checks it before final evaluation
C) Validation data is only used for clustering
D) Training data is always unlabeled

**Answer: B** — Training fits, validation tunes/checks
</details>

<details>
<summary><b>Q5.</b> Which Azure AI Language feature would identify that a support ticket is expressing frustration?</summary>

A) Key phrase extraction&nbsp;&nbsp;B) Sentiment analysis&nbsp;&nbsp;C) Language detection&nbsp;&nbsp;D) Entity recognition

**Answer: B — Sentiment analysis**
</details>

<details>
<summary><b>Q6.</b> A company wants its AI chatbot to explain <i>why</i> it denied a customer's request, in plain language. Which Responsible AI principle applies?</summary>

A) Inclusiveness&nbsp;&nbsp;B) Transparency&nbsp;&nbsp;C) Accountability&nbsp;&nbsp;D) Fairness

**Answer: B — Transparency** (explaining decisions to users)
</details>

<details>
<summary><b>Q7.</b> A hiring model consistently rates candidates from one demographic lower, regardless of qualifications. Which principle is being violated?</summary>

A) Fairness&nbsp;&nbsp;B) Inclusiveness&nbsp;&nbsp;C) Privacy and security&nbsp;&nbsp;D) Transparency

**Answer: A — Fairness** (biased outcomes across groups)
</details>

<details>
<summary><b>Q8.</b> Which Azure service is best suited to extract structured key-value fields (like invoice number, vendor, total) from scanned invoices?</summary>

A) Azure AI Custom Vision&nbsp;&nbsp;B) Azure AI Document Intelligence&nbsp;&nbsp;C) Azure AI Translator&nbsp;&nbsp;D) Azure AI Face

**Answer: B — Azure AI Document Intelligence** (document processing/knowledge mining)
</details>

<details>
<summary><b>Q9.</b> What distinguishes abstractive summarization from extractive summarization?</summary>

A) Abstractive picks existing sentences verbatim; extractive generates new paraphrased text
B) Extractive picks existing sentences verbatim; abstractive generates new paraphrased text
C) They are the same technique with different names
D) Abstractive only works on images

**Answer: B** — Extractive = verbatim existing sentences; Abstractive = new generated text
</details>

<details>
<summary><b>Q10.</b> What is "grounding" in the context of generative AI?</summary>

A) Reducing a model's computational cost
B) Supplying relevant, up-to-date data so answers are based on facts, reducing hallucination
C) Converting text input into embeddings
D) Making responses shorter

**Answer: B**
</details>

<details>
<summary><b>Q11.</b> Which Azure service provides enterprise access to OpenAI's GPT models with built-in content filtering?</summary>

A) Azure AI Foundry Model Catalog&nbsp;&nbsp;B) Azure AI Custom Vision&nbsp;&nbsp;C) Azure OpenAI Service&nbsp;&nbsp;D) Azure AI Language

**Answer: C — Azure OpenAI Service**
</details>

<details>
<summary><b>Q12.</b> A model is trained to distinguish between three types of skin lesions from photos. What kind of ML technique is this?</summary>

A) Regression&nbsp;&nbsp;B) Binary classification&nbsp;&nbsp;C) Multiclass classification&nbsp;&nbsp;D) Clustering

**Answer: C — Multiclass classification** (3+ class labels)
</details>

<details>
<summary><b>Q13.</b> Which computer vision capability would count the number of people entering a store from a security camera feed?</summary>

A) Facial recognition&nbsp;&nbsp;B) Spatial analysis&nbsp;&nbsp;C) OCR&nbsp;&nbsp;D) Semantic segmentation

**Answer: B — Spatial analysis** (part of Azure AI Vision)
</details>

<details>
<summary><b>Q14.</b> What is the primary purpose of Azure ML's Automated ML (AutoML) feature?</summary>

A) To manually write training code for every algorithm
B) To automatically try multiple algorithms/hyperparameters and find the best-performing model
C) To deploy models to production only
D) To perform OCR on documents

**Answer: B**
</details>

<details>
<summary><b>Q15.</b> Which term describes when a generative AI model produces a confident but factually incorrect or fabricated response?</summary>

A) Grounding&nbsp;&nbsp;B) Tokenization&nbsp;&nbsp;C) Hallucination&nbsp;&nbsp;D) Fine-tuning

**Answer: C — Hallucination**
</details>

<details>
<summary><b>Q16.</b> A model correctly identifies 80 out of 100 actual fraud cases but also flags 40 legitimate transactions as fraud. Which metric describes "80 out of the actual 100 fraud cases caught"?</summary>

A) Precision&nbsp;&nbsp;B) Recall&nbsp;&nbsp;C) F1 score&nbsp;&nbsp;D) R-squared

**Answer: B — Recall** (of actual positives, how many were correctly predicted)
</details>

<details>
<summary><b>Q17.</b> Which Azure AI Language feature lets you define custom intents and entities to build a chatbot that understands domain-specific requests?</summary>

A) Sentiment analysis&nbsp;&nbsp;B) Conversational Language Understanding (CLU)&nbsp;&nbsp;C) PII detection&nbsp;&nbsp;D) Key phrase extraction

**Answer: B — Conversational Language Understanding (CLU)**
</details>

<details>
<summary><b>Q18.</b> What is Retrieval Augmented Generation (RAG) primarily used for?</summary>

A) Training a model from scratch
B) Retrieving relevant data and injecting it into a prompt so the model's response is grounded in that data
C) Compressing model size for faster inference
D) Detecting anomalies in time-series data

**Answer: B**
</details>

<details>
<summary><b>Q19.</b> A company wants to create a unique, branded synthetic voice for their virtual assistant. Which Azure Speech capability is this, and what access level does it require?</summary>

A) Speaker recognition — general availability
B) Custom Neural Voice — Limited Access
C) Speech Translation — general availability
D) Intent recognition — Limited Access

**Answer: B — Custom Neural Voice, Limited Access** (requires application due to misuse/deepfake potential)
</details>

<details>
<summary><b>Q20.</b> Which stage of the responsible generative AI lifecycle involves layering content filters and blocklists on top of a deployed model?</summary>

A) Identify&nbsp;&nbsp;B) Measure&nbsp;&nbsp;C) Mitigate&nbsp;&nbsp;D) Operate

**Answer: C — Mitigate** (safety system layer)
</details>

---

## 📋 Exam Tips Checklist

- [ ] No coding is tested — focus on **what each service does and when to use it**, not how to implement it
- [ ] Expect scenario-based questions: *"A company wants to X — which service should they use?"*
- [ ] Practice distinguishing between similarly-named services (see Quick-Reference above)
- [ ] Drill the six Responsible AI principles until you can identify the right one instantly from a scenario cue
- [ ] Know the difference between supervised (regression/classification) and unsupervised (clustering) techniques cold
- [ ] Review precision/recall/F1 and MAE/RMSE at a conceptual level — you won't need to calculate them, but you should recognize what each measures
- [ ] Know which capabilities are **Limited Access** (Face identification, Custom Neural Voice, Speaker recognition) — the exam likes to test awareness of Microsoft's misuse-prevention gating
- [ ] Understand grounding/RAG conceptually — it's one of the most tested generative AI concepts
- [ ] Use Microsoft's free official practice assessment before sitting the exam (though note: **this exam is retired — see AI-901 for the current path**)

---

<div align="center">

**Good luck! 🎓**

</div>
