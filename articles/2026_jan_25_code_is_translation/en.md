I have experimented with spec-driven, docs-driven, and guide-driven workflows—I even tried developing "semantic intent"—and as a result, I’ve completely reimagined why these things exist in the first place.

Like many, I initially tried to draft them as detailed PRDs (Product Requirements Documents), GDDs (Game Design Documents), or SOPs (Standard Operating Procedures), intending for them to serve as the absolute "source of truth" for every change.

Under that model, the Agent’s flow looked like this:
Role (Agent + Project Rules) -> PRD -> Code Analysis -> Implementation.

However, this chain inevitably broke the moment it touched the actual logic of the code.

That led to my first "Eureka" moment: The ideal PRD is working code.

If the code works, it reflects the business logic with a level of perfection, logic, and rigor that a PRD can only aspire to.

Therefore, to develop a "perfect" PRD, one must use a format of strict logical code—whether high-level (BPMN, Mermaid diagrams) or a hand crafted/invented format.

This creates a paradox: to write code, you need a PRD; but to write a PRD, you need code.

Then came the second "Eureka":
PRDs, programming languages (VBA, Dart, Rust, etc.), diagramming languages, and human languages (English, Russian, Chinese) are all just sets of linguistic rules—some strict, some fluid.

They are tools through which we transmit or configure the transfer of knowledge and thought, embedded with the "cultural code" of the speakers. In other words, they are all just different forms of interpretation.

Think of it through these associations:

- Film = an interpretation of a book/script.
- Audio = an interpretation of emotion.
- Excel sheet = an interpretation of a data group.
- PRD or GDD = an interpretation of systems, data, and visualization.
- Design = a visual interpretation of logic and data.
- Code = an interpretation of logic and data.

Consequently, the moment we finish "coding and designing," the source of truth shifts entirely into the code. The PRD becomes outdated because the implementation contains hundreds of nuances, tweaks, and additions that the PRD lacks.

To test this theory, try this experiment:
Draft a small piece of logic in a PRD. Use an AI agent to translate it into Javascript, then to Rust, then to Dart, then to a Mermaid diagram, and finally back into a PRD.

What we can conclude from this:

- The PRD becomes redundant; it can be deleted.
- The most vital element in "translation" is cultural context. Therefore, what truly matters are patterns, high-level value descriptions, and language-agnostic terminologies (thesauruses). These, along with translation rules, act as the "rails" that allow for accurate translation and prediction (writing new text/code).
- It is more important to conduct a Pattern Review than a Code Review—to identify the "translation" tools and enrich the "cultural context" and rules.

Ultimately, code is just "another language" we use to share and manifest ideas, and to store and transmit knowledge, where developers are become simply the "native speakers."

Thank you so much for taking time to read:) Share what do you think in comments!/)

Anton

please notice: I've written the lines above initially in other language by hand, however I've used Gemini to translate it to English and then corrected it to match original text.
