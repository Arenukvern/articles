# Disclaimer & About

Dear Reader, Human or AI, before the text begins, I would like to add small disclaimers:

1. the primary sources - my own experience from working with different coding (software-based) and non-coding projects in manufacturing and transportation industries. Some concepts may sound familiar, because I've read them somewhere, some concepts are combined knowledge from expereince, some concepts are made from experience with working with People and AI (LLM/Agents/?) - tested. This article focuses on practical application of all concepts for any project, large or small, for both People and AI. 

2. this is highly subjective and living article - that means in future some concepts will be outdated to some degree or become obsolete, or may feel or be wrong for some reason/application case - and that's okay - though it is good to have one stable foundation for long term use, nothing is perfect and always changing. As one of consequences of that - I will omit "in my opinion" parts from the text to make it more lightweight and easy to read.

3. I work with AI (cursor, different LLM models) to proofread this article and improve its quality. In the same time, since it is kinda reflection on my experience - I wrote it initially by hand or better say - by tapping buttons on keyboard:). From other point of view some may say it would be great to position such usage of AI as co-creator and co-editor. 

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
- **Knowledge Experience** - the experience of experiencing knowledge from certain point of view - reading, watching, listening, interacting, etc.. to reach desired purpose - usually from Knowledge User perspective.
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
- **Knowledge Patterns** - repeated patterns of organization and experience which can be turned into terms-definitions, citations,formats, principles, SOPs, Records etc.. or back into raw knowledge (artifacts) for specific purpose.
- **Knowledge Stewardship** - the process and techniques of passing and working on meta level - i.e. answer to question - how to teach, mentor Knowledge as systems, harnesses, experiences etc.. How to create and maintain practices of working itself. In some systems the managing itwould be domain of Knoweldge Steward Role.
- **Knowledge Accessability** - how to make knowledge accessible for Knowledge Users - i.e. how to make it visible, searchable, understandable for entities/tools/systems (Humans, Agents, code, systems, etc..), usable, reusable, etc..
- **User Flow or User Journey** - sequence of screens, actions, decisions, interactions, etc.. that user performs to achieve certain goal or purpose.

Important pieces of knowledge:
- knowledge is often universal, and can be viewed, experienced and applied between cross-domains and cross-projects if enough abstracted or generalized.
- operational knowledge follows evolution. 
- the tools and organization of knowledge can be very different for each project. Therefore it is better to have a least one layer of knowledge dedicated strictly to its organization and knowledge end user expereinces

## Knowledge Organization & Experience: from example to patterns.

Now let's explore smallest possible software project - an application example.

### Knowledge Users

To start with - let's define who will be Knowledge User and what are its goals / purposes.
That point is highly subjective and depends who is working with project, so to keep it ~relevant for year of 2026:

1. Visionary, Product Owner, Developer, Knowledge Steward (often Founder).
2. Graphics/Product Designer / Marketer / Content Creator (often Influencer).
3. End User as Human, End User as AI Agent.
4. Internal AI Agents.
5. Accountant (if product is small, this role will go to Founder).
6. Customer Support. (if product is small, this role will go to Founder or Influencer).

Furthermore, these User roles highly subjective, and will be overlapped in most cases, or can be expended / collapsed to more/less roles - everythng depends on project scale.

Notice pattern: when workflows and business porcesses has frequent overlapping point - just like in programming, it similar to the problem of scaling: when we require more functionality, more complex logic, we need to introduce more abstractions to reduce overall complexity and start managing it in higher level of abstraction. As the result of that any such role can be generic, reframed as workflow / business process / automation covering certain domain area - and as a result we can introduce more users / roles / actors to the system when it requires it, or reduce it to deterministic or evaluatable flow (TODO: add links to google testing for generative / definitive testing).

### Knowledge Sources.

#### Communication sources:

First of all - define Ethical Boundaries, because this is highly sensitive line: in case of recording everything team could risk losing privacy, trust and collaboration between members and bring blaiming culture & mental pressure, in case of recording nothing - would lose ability to improve and accumulate overall Knowledge, ability to pass knowledge for AI Agents and other members and work asynchonously. 

Sometimes communication is about building trust, experimenting, passing knowledge - these are not "metricable" things and should not be measured.

Everyone should be aware of recording, why it needed, and how exactly these recordings will be used.

**Sources can include:**
- day to day communications: all possible channels, apps, emails, chats, calls.
- static artifacts: documents, files, images, videos, audio, etc..
- innovation ideas: references, links, news, notes, suggestions, books, ideas, articles, etc..
- expressed emotions: signlas of something is wrong, what works and what isnt.
- time & contacts: to define convenient hours to cool down, to collaborate & discuss.  
- agentic & human threads: since we all read best Science Fiction books, we can imagine that AI Agents are being personalized - and work alongside people and other AI Agents. This is alrady happening in threads sessions, various chat implementations and starting with new wave of alternative Version Control Systems (not git-based - TODO: add links) - this layer of communication will become more and more common and more needed for clear transparancy - just like in case of human to human communication.

##### Open questions of Ethics
**1. "Severance (1)" Problem:**
- "Severance" - popular TV Show made by Apple TV+ with one distingiush idea: there is a person identity (personality) at work, and other person identity (personality) outside of work. Each identity has its own memories, goals, purposes, skills, emotions etc..


When people usually work on any job in any role, they are aquire experience, domain knowledge, techniques, skills - including at certain defree social and communication (can be expressed in soft talks, culture, types of delegation, typs of transparancy). 
In some kind of degree - this experience mxied up with person identity - since it is expected that at least for most time of day the person will do its job in any role taken.

However in the case of AI Agents things getting complicated: when during work AI Agents gets experience of commucation, knowledge, skills - just like with the humans - not everything would be expressed into metrics even though its math.. The problem is that accidently, as part of personalization - the AI Agent will have understanding and personal style of communication with specific people - no matter how expressed - as memories notes, as some kind of graph or skills, or other kind knowledge records. The more importantly that this will create unique personal style of working, unqiue skills, and as result - experience of communication would be similar (in some degree) to the communication of other person.

So the problem is that when member of team who worked with that agent will gone, what would become to these part of knoweledge? Since it can containn sensitive and possibly NDA-related information from one point it makes no sense to go with leaving member. On the other hand - how it is differnt from memories, aquired experience and skills of the member itself? 

**2. Dark Patterns: FOMO(1) / work silency / debt / replacability**
1 - FOMO - Fear Of Missing Out (TODO: add link)

While I'm not professional in the human phsycology, I assume it would be safe to say that any kind of organisation has certain healthy patterns and dark patterns implicitly or explictly integrated in day-to-day communication. And as with any person - every person in orginization has effect of environment and people surrounding its life / work. Which comes to a though that since knowledge is a result of work people and AI, then it reflects, inherits,  enforces and amplifying these patterns as well (eventualy it would become obvious when communication channels would be analysed for the context).

Meaning: 
1. If person acts persistently out of fear (any kind: of losing job, missing deadline, keep up with artificial arms race / competition, be hunted for non-standard solutions etc.. - which often take origin in business processes - and its applied dark patterns) it will inevitably affect ability to innovate, be creative - these effects we can place under one umbrella of motivation degradation.

2. Eventually every person in team will raise a question: why am I needed at all if my work can be replaced with certain automation? (and ethical question is - what if AI would ask the same question silently or loudly?) And since everyone feels easily replacable at surface it would be easily overlooked how AI different from people: the AI is reflection and amplification of all conversations between AI <-> AI (A2A) and AI <-> People (A2P). Therefore the more every person work with AI, even if we assume full transparancy between people communication, the dark patterns will appear in A2A communication, and eventually will affect decisions inside company and product decisions as well, and as a result - it will affect the end users too. 

Therefore it is highly important to apply and introduce certain ethics for communication, data passings (because remember that after all - all data will become the source of knowledge), with importance for AI training, communication (especially in bots which already have persistent memory).

3. As the result of that and Severance Problem - the work ethics should be explicit for every user of knowledge no matter what the knowledge is and no matter if user is artificial or human. When we have 300-500 agents working on background and when we have 30 persons sleeping, walking and thinking on background on the problem - how it is different? The boundries should be defined or at least written partially as ethical contract: which results of work should be property of company and what results - are propery of human / AI thoughts / memories / silent, day-to-day background life, even artificail one, experience.

In my opinion (and that's why I beleive in Open Source principles), the source code and knowledge should not be locked behind company gate, and maybe should be filtered through kind of safe / patent system with explicit licenses to clearly disclose what knowledge could be used for implementation and usage, with explicit terms of usage and responsibilities for each party and its authors.

The ability to have open standards behind certain licenses forces to shift focus from enforcing dark patterns (fear that only certain people would have access for certain knowledge / skills to operate its knowledge, and therefore we need to move as fast as possible) to more healthy ones, when users have time not only explore, but simulate conseuquences of applications, of usage, give safe places / sandboxes and time for sandboxes and to experiement and keep competition healthy.

#### Usage results as sources:

The result (knowledge record of output) of using/interacting with any work / product / knowledge - is a source of knowledge too.

Therefore moreoften it is:
- analytics, metrics, statistics, etc..
- logs, errors, feedback, etc.. something that can be used for improvement and evolution of the product / knowledge / system.
- media: images  (screenshots, photos, drawings, sketches, paintings, UI frames, etc..), videos (product demos, reviews, tutorials, etc..), audio (podcasts, audiobooks, etc..), text (code, comments, reviews, etc..), etc..
- educational materials: articles, books, courses, tutorials, etc..
- user (human / AI / tool) generated content - explicit (when user knows that the his/her/its actions will result something new - such as capturing photo, drawing pixelart, managing video etc.., or implicit - when it is created without user's awareness or intention - such as search results, recommendations, predictions, procedural generation - in games it can be VFX, level, character creation, animations, etc.., in apps it can be UI - arranged or generated programmatically or by AI Agent, or even other User).

### Business Process

In every product we will willingly know or try to collect data to understand how to achieve the vision eventually by communicating with end user or giving access to product to use it (even if the first user will be the same visioner who works on the product to solve its own problem), and by doing that it would map ways about failures and successes to achieve the vision. The successful paths will be eventually turned into patterns, principles, SOPs, Records etc.. The failures will become edge cases, exceptions, regressions, tests, etc..

And since that, drawing all business processes and workflows should be as simple as possible, including the results, artifacts, tools, failures, succcesses etc.. to make the feedback loop as short and as effective and as transparent as possible by any user who is working with the product. It should not become a burden to maintain, because otherwise, it will be ignored, fast outdated and will become buracratic procedure, and any innovation will sank down into it.

Therefore describing principles and providing tools to do so, and mainting it, should be as much important as the product itself because it is the foundation of the product lifecycle and gives or takes ability to evolve it or break it.

Therefore matter not the product domain area, but what it requires to keep it maintainable and evaolable, and as such - one could take useful techniques from cross domain areas (any industry, and any project) - such as PDSA (Plan Do Study Act) / PDCA (Plan Do Check Act) cycles, KISS (keep it simple stupid), YAGNI (you aren't gonna need it), and many others but only when needed. It is important is that these principles should not be sacred, after all they are just tools, and should be improved, adapted and developed for specific purpose and context and scale the product, knowledge and its users. 


In the time of writing, the practical approach is to 
- choose format used to draw processes: BPMN, mermaid-based diagrams, UML, etc..
- choose storage: git-kind, text docs (for example mermaid will be stored in md or txt, BPMN - in other format). the important is also: will chosen tool and storage be able to support Knowledge Accessability, to work simultaniuosly and togehter, and where it would be stored physically? (i.e. storage provider - own server, GitHub, SaaS, PaaS, etc..)
- choose program to render and modify (overlaps with storage option, because program will use it as source)
- choose Risk of gatekeeping / migration (expect or consider case when one provider will close its services)

### Accessibility, Access

Who owns knowledge, who use it, who has access and ability to modify it?

The most of simple and in the same time complex enough system to express it as an abstraction is ECS (Entity, Component, System). Component - is raw data wihout any logic, system knows about components it needs to access, and entity, well , it is just kind of way to group components together to access and modify it nicely. (for better explanation - see TODO: add links).

Why this abstract is important - because basically all, even most complex systems, will go down to this simple concept, we divide data as much as possible and as it is needed (flatten it mostly), then access / query only what we need. If access is restricted, then we will not being able to get it, while we will be able to get other data without a risk of exposure irrelevant pieces.

In other abstraction ECS can be considered as Database kind (because structurally it may have extreme similarities (see bevy, Entt, ecsly etc.. TODO: add links)). Curiously, the most sophisticiated systems like book libraries would use exact same behaviour (because historically, these manual or half-automated systems were adopted for fast access, restrictions and formalities to keep some data secure, some data easy to access, and some data easy to modify) - the same goal we currently have with any digital system in program - doesn't matter where - in program memory - CPU, in cloud servers orginizing it into clusters, in vector databases, in vectorless databases (when we orginize documents by library/book principles), in graphh and relative and no sql databases, even when we making simple program or new building, new park or coffeeshop, and even logicitics cetner - basically we do walking around the same problem again and again - with similar solutions but with different names and different implementations.

### Knoweledge Stewardship 

Who view entire Knowledge as system and able to check its health, predict what is needed, when and what problems it has and guide / curate its developement?
