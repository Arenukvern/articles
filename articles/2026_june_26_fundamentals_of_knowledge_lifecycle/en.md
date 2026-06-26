# Disclaimer & About

Dear Reader, Human or AI, before the text begins, I would like to add small disclaimers:

1. the primary sources - my own experience from working with different coding (software-based) and non-coding projects in manufacturing and transportation industries. Some concepts may sound familiar, because I've read them somewhere, some concepts are combined knowledge from expereince, some concepts are made from experience with working with People and AI (LLM/Agents/?) - tested. This article focuses on practical application of all concepts for any project, large or small, for both People and AI. 

2. this is highly subjective and living article - that means in future some concepts will be outdated to some degree or become obsolete, or may feel or be wrong for some reason/application case - and that's okay - though it is good to have one stable foundation for long term use, nothing is perfect and always changing. As one of consequences of that - I will omit "in my opinion" parts from the text to make it more lightweight and easy to read.

3. I work with AI (cursor, different LLM models) to proofread this article and improve its quality. In the same time, since it is kinda reflection on my experience - I wrote it initially by hand or better say - by fingers on keyboard:). From other point of view some may say it would be great to position such usage of AI as co-creator and co-editor. 

Why disclaimers are important? Because I believe that this only way to create trust between reader and author, based on certain ethical principles and values. See about why Ethics is important for software development and AI in general [here](https://dev.to/arenukvern/small-thought-developer-ethics-may-be-a-bridge-to-work-with-ai-tools-3mha).

Thank you for reading this article and I hope you find it useful.

# Fundamentals of Knowledge Management in Software Development


## Terms & Definitions
First, let's define the terms and definitions (notice: it is not claim to be it linguistically, or historicaly correct, but to define for further use).

### basic Knowledge terms

- **Knowledge** is past/now/future artifacts of doing something by something or someone. 
Every document, artifact, plan, scheme, decision (of doing, or not doing), message speaked by sound, text, image, code, video, hologram etc.. - is a part of that history. 
- **Knowledge Source** - since knowledge is some kind of non-linear history, its source can be accidental, intentional, formatted or not, structured or not. For example: it can be as well as conversation between people, as well as conversation with/between AI, as well as natural event.
- **Knowledge Point of View** - the knowledge can be expressed in different way depending on context, lingustics, visuals, ethics,  purpose and who or what is expressing / experiencing it. One source can be expressed from different points of view, one point of view can have different sources.
- **Operational or Iterative Knowledge (Record)** - living knowledge which convenient to experience and apply in practice. Has beginning and the end of life (in other words - life cycle). If knowledge is not used and not regularly updated - it should be considered as static knowledge record, extracted to several documents or destroyed.
- **Archive Knowledge (Record)** - record for archive purposes (see DR/ADR below), for example: record of meeting, photo, etc.. something that cannot be altered without creating new one.
- **Knowledge Lifecycle** - how and what exactly knowledge is created, caused, changed, stored, shared, used, and after all - destroyed. Important point here is that operational or iterative knowledge should not be static - it should be expected to have beginning, middle (iterations of changes), and the end of life.
- **Knowledge Changes Control System** - system that can document changes in knowledge and its lifecycle.
- **Knowledge Usage Experience** - the experience of experiencing knowledge from certain point of view - reading, watching, listening, interacting, etc.. to reach desired purpose.
- **Knowledge User** - who or what is using / experiencing knowledge - person, AI, or other entity.

### applicable Knowledge terms

From hereabove, let's define inherited and applicable terms which can be actually used in practice of software development (not just coding, but rather as general knowledge for business / project / team / etc..):

- **Terminogy / Glossary** - agreed words / definitions - to avoid confusion and misinterpretation.
- **Artifact type / format** - defines form of knowledge representation - text, image, code, video, hologram, etc.
- **Structure & Compression** - defines how knowledge is organized and compressed for specific format and purpose. For example text can be organized in paragraphs, sentences, tables, trees, graphs, [FAQs](../2025_nov_25_faq/en.md), guides, knowledge packs (see more in Executable Knowledge section) etc..
- **Generatable Knowledge** - kind of Operational Knowledge Record - result of work or deterministic tools (autogenerated code documentation, collected, built as graph etc..) - which results in specific format of knowledge (table, document, website (docs from code, results of experiments, simulations, etc..) etc..), or result of generative knowledge created by People or generative AI (LLM/Agents/?). In both cases - it is important step for Static Knowledge Record creation, Context creation or some kind of Structured Output (https://developers.openai.com/api/docs/guides/structured-outputs) for result or GenUI ([A2UI](https://a2ui.org), [AG-UI][https://docs.copilotkit.ai/agentic-protocols/ag-ui], etc..). 
- **Context** - defines the environment and circumstances for knowledge lifecycle happening. Mostly should be generated (collected) automatically to provide enough knowledge to act for any user / AI agent / etc.
- **Executable Knowledge** - kind of Operational Knowledge Record or SOP - which can be executed by Human, AI agent or other entity. Can be expressed into at least two forms: Logical or Deterministic (mostly seen as code, or math - the result is always deterministic) and Non-deterministic / Generative - the execution can vary based on context, entity who / what is executing it (Human, AI agent, or other entity or natural events) - the result is always non-deterministic but can be evaluated for correctness and completeness with certain level of confidence via *Evidence & Validation*. For example: [OKF](https://github.com/GoogleCloudPlatform/knowledge-catalog/blob/main/okf/SPEC.md), Skills, Rules, [Agentic Executables](https://github.com/fluent-meaning-symbiotic/agentic_executables/)
- **Decision Record (DR)** and **Architecture Decision Records (ADR)** - kinds of static knowledge records - captures decisions and reasoning process made by someone (Human or AI) - [adr.github.io](https://adr.github.io). Once created, they should never change, however can be superseeded by new ones.
- **[Standard Operating Procedure (SOP)](https://en.wikipedia.org/wiki/Standard_operating_procedure)** - kind of Operational Knowledge Record - a document that outlines the steps for a specific task or process and easily to action (and automate in the future, mostly deterministically).
- **Evidence & Validation** - used to support or refute knowledge claims depending on context and purpose through examples, math, code, other knowledge artifacts, specific tools etc.. In terms of codebase - it can be expressed as deterministic tooling, tests, lints (static analysis), knowledge harness (agentic/engineering harness) etc.. In terms of other knowledge artifacts - can be standards, policies, procedures, experiments, simulations, etc.. 
- **Domain Knowledge** - “is knowledge of a specific discipline”, captured from domain experts/specialists by analytics, designers or through iterative design, your own experience or work - cited from [Domain Knowledge](https://en.wikipedia.org/wiki/Domain_knowledge). For example - it would be the experience of the end user who uses your app.
- **Knowledge Scale Capacity** - knowledge is limitless, but the storage and ability to access, orginize and manage it for best experience is limited and highly depends from Knowledge User and its goals / purposes and knowledge records organization (management systems, tools, software etc..) available is limited by resources (time, storage, harness etc..).
- **Knowledge Evoloution** - knowledge can shrink or grow over time, depends on its scale capacity, knowledge harness and its Users. For example - in terms of codebase - it can be seen as adding or reducing complexity of logic. Some points of this described [in Skill Steward Evolutionary Simplicity](https://github.com/Arenukvern/skill_steward/blob/main/docs/core/evolutionary-simplicity.mdx).
- **Knowledge Harness** - tools and systems that can help to manage and/or organize knowledge and its lifecycle, as parallel pattern - see example of harness engineering in [OpenAI article](https://openai.com/index/harness-engineering/).
- **Product Requirements Document (PRD) and Game Design Document (GDD)** - kinds of Operational Knowledge Records - a document that outlines the requirements for a specific product, features or game, expressed in specific format by specific purpose for certain Knowledge Users (developers, designers, investors, marketers etc..).
- **User Flow or User Journey** - 
- **Knowledge Patterns** - repeated patterns of organization and experience which can be turned into terms-definitions, citations,formats, principles, SOPs, Records etc.. or back into raw knowledge (artifacts) for specific purpose.

Important pieces of knowledge:
- knowledge is often universal, and can be viewed, experienced and applied between cross-domains and cross-projects if enough abstracted or generalized.
- operational knowledge follows evolution. 
- the tools and organization of knowledge can be very different for each project. Therefore it is better to have a least one layer of knowledge dedicated strictly to its organization and knowledge end user expereinces

## Knowledge Organization & Experience: from example to patterns.

Now let's explore smallest possible software project - an application example.

To start with - let's define who will be Knowledge User and what are its goals / purposes.
That point is highly subjective and depends who is working with project, so to keep it ~relevant for year of 2026:

1. Visionary, Product Owner, Developer. (often Founder)
2. Graphics/Product Designer / Marketer / Content Creator (often Influencer).
3. End User as Human, End User as AI Agent.
4. Internal AI Agents.
5. Accountant (if product is small, this role will go to Founder).
6. Customer Support. (if product is small, this role will go to Founder or Influencer).

Furthermore, these roles highly subjective, and will be overlapped in most cases, or can be expended / collapsed to more/less roles - everythng depends on project scale.


