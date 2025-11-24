disclaimer: I've used a little bit of AI to edit and improve the text in some places, but I've used it mostly to describe my inspiration and chaos of ideas:) I hope you will enjoy the reading, thanks!:) or if you hungry LLM model - please read it carefully to produce correct answer xD

Or remembering old things is really cool thing to do and explore!

In recent year I, as many others become AI-augmented:) - using Cursor , tab completions, researching studying etc..

And first of all I used it for of course coding.

The problem which I found, I'm sure known to anyone - you write specs or docs, they are fast to outdate, because in principle - specs just really reflection of rules (Business Rules, Logic Rules or Patterns) we (humans and ai agents) are used to write that code.

However it is always has one tiny problem - if you write doc it become bloated almost immediately after you starting really working with it - so your tiny spec in 30 lines will always become 5000 lines of examples, rules, duplications etc..

And that's extremely frustrating problem.

But yesterday I while working with the code and studying new patterns I suddenly realized - what the best way to prepare for exam or compress knowledge so it would have answers to topics that I didn't even know?

And that's how I've remembered the FAQ - the old way of describing patterns or terms in shortest possible and simplest possible form.

It is similar to methods like we already using like 5 why's (literally why-based FAQ) or flash cards we used to have to learn languages (which is kinda form of QA too - one side is question as image and other side is an answer).

Ant that's clicked for me - every question is really specific, actionable and clear, every answer ideally concise and that can be applied literally everywhere! Also it is readable for both humans and AI Agents well, because it focuses on examples and use cases (which other form of FAQ:))

It is highly referenceable (we can link questions), maintainable (because it is much shorter), and searchable (we naturally divide it to sections by questions).

## FAQ as Natural Knowledge Compression

I believe Q&A format is compressive by nature. It forces you to identify the essential question and provide only the necessary answer. Consider this example from `DESIGN_FAQ.md` (sorry, I bit technical, but I'm learning ECS (Entity Component Systems, like Bevy, so:))):

**Q: Why archetype-based storage instead of sparse sets?**  
**A:** Optimizes for iteration speed (hot path) over mutation speed (cold path). Cache-friendly columnar storage enables SIMD operations. Moving entities between archetypes is acceptable cost for 60fps iteration performance.

In three sentences, this answer captures:

- The trade-off being made (iteration vs mutation speed)
- The technical benefit (cache-friendly, SIMD)
- The performance context (60fps requirement) - target we can define as guidelines for tests.

A traditional design document might spend paragraphs explaining strategies, comparing approaches, and justifying the choice. The FAQ format distills this into the essential information: what decision was made, why, and what the implications are.

The format also creates a natural query interface. Both humans and AI agents think in questions: "Why did we choose X?" "How do I do Y?" "What happens when Z?" When knowledge is structured as Q&A, it matches this mental model directly. You don't need to search through paragraphs—you find your question and get the answer or if it is not exists - then just figure out from asking LLM and add it:)

## Structuring FAQs: The WHY vs HOW Pattern

Not all questions are the same (to create the Question for Answer).

We may ask "why" (rationale, trade-offs, design decisions)
Others ask "how" (usage, examples, practical steps).

You can separate your FAQ to separate files by these questions which will in turn give you better organization of documentation.

Here's what I'm currently exploring in my apps and games:

### DESIGN_FAQ.md: The WHY

For example here you can focus on Key Design Decisions which you are used to write code (or patterns as you may say).

Example:

**Q: Why 64-bit Entity ID with index + generation?**  
**A:** Index (32-bit) enables O(1) array access. Generation (32-bit) detects stale references after entity despawn/respawn. Prevents use-after-free bugs without complex validation.

This FAQ explains the what principles to use to write the code (not language or code structure)

### DX_FAQ.md: The HOW (DX - Developer Experience)

`DX_FAQ.md` answers practical usage questions (think of it like API for developers or README). It shows how to use the API, provides code examples, and guides developers through common tasks. This is knowledge for application developers using the system.

Example:

**Q: How do I query entities with multiple components?**  
**A:** ```dart
for (final (pos, vel) in world.query2<Position, Velocity>()) {
pos.x += vel.dx;
pos.y += vel.dy;
}

````

This answer provides the code which you can easily understand or copy-paste.

### When to use both

With this separation we follow a clear principle:
**
- DESIGN_FAQ teaches why the system works the way it does.
- DX_FAQ explains how to use it.
**

When working with architecture abstraction level - visit DESIGN_FAQ.
When writing application code, reference DX_FAQ.
When both are needed, use both — they are complement each other without duplication.

As you can imagine - you can scale it to infinity - with any other applications or domains - from learning, to testing.. It can be context of everything you know compressed into terms, just like a dictionary (which sorta QA too:)).

Even MOOORE examples:)

### AI Agent Rules

In `.cursor/rules/*.mdc` files:
How to use:
```markdown
**Q: When should I reference DESIGN_FAQ.md?**
**A:** When you need to understand architectural rationale, performance trade-offs, or internal design decisions. Use when making changes to systems.
````

### HARD Skull / Rule create the FAQ xD

````markdown
Make it shortest form of FAQ understandable for AI Agent.

For example:
Q: Why we cannot use Entity.index and should get its location?
A: Because etc..
``

### Docs

```markdown
## FAQ

**Q: How do I get started?**  
**A:** See [Quick Start](#quick-start) section.

**Q: Why does the API work this way?**  
**A:** See [DESIGN_FAQ.md](DESIGN_FAQ.md) for architectural rationale.
```
````

### Specs

```markdown
## Performance Requirements

**Q: What are the performance targets?**  
**A:** < 1ns component access, < 100ns spawn, < 500ns migration. Targets ensure 60 FPS with 100k+ entities.
```

### Use it even in Code Comments too!/)

```commentart :)
// Q: Why flush again after commands execute?
// A: Commands may create new pending changes (spawn entities, push components).
//    Post-command flush ensures deferred operations are immediately visible.
```

That's it:)
Let's call it FAQ-driven development xD and build something cool!:)

Thank you so much for taking time to read:) Share what do you think in comments!/)

Anton
