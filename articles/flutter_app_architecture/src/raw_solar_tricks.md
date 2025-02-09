Layered Context Approach, Standardized Component Structure

```md
1. CORE_PRINCIPLES.md (50-100 lines)

   - ECS structure
   - Key simulation constants
   - Coordinate systems
   - Shader architecture

2. SYSTEMS_QUICKREF.md (1-2 lines per system)
   Example:

   - OrbitalSystem: Handles Keplerian mechanics using Δt
   - ShaderSystem: Manages star field + planetary atmosphere effects

3. COMPONENT_MATRIX.md (Table format)
   | Component | Systems Using It | Data Type | Size |
   |------------------|------------------|-----------|------|
   | OrbitalComponent | Orbital, Render | Float64[6]| 48B |
```

```md
Domain-Specific Glossary

# TERMS

- AU: Astronomical Unit (149,597,870,700m)
- 6-DOF: 6 Degrees of Freedom movement
- LOD: Level Of Detail (0-5 AU: High, 5-30 AU: Medium)
- ECS: Entity-Component-System pattern
```

Pre-Processing Steps

Generate code summaries:
Create dependency graph:
Context Sandwich Pattern:
Hash-based Context Versioning:

AI Prompt Structure

[Feature/Bug]: Camera jitter in FollowMode
[Relevant Systems]: CameraSystem (lines 45-78), PhysicsSystem (lines 120-155)
[Related Principles]: 3D Visualization §6, ECS §4
[Code Samples]:

Performance Budget

```md
| Subsystem         | Target Frame Time |
| ----------------- | ----------------- |
| OrbitalSystem     | ≤2ms              |
| StarfieldRenderer | ≤3ms              |
| AtmosphereShader  | ≤1.5ms            |
```

Context tagging system metadata

```md
---
priority: 1-5
dependencies: [file1, file2]
update_frequency: high|medium|low
scope: core|rendering|physics|controls
---
```

Automated Context Extraction: Consider using simple scripts that scan changed files (or your Git commits) and then automatically select and package relevant context snippets for the AI. This reduces manual effort and keeps the context focused.

Structured Prompts: Begin your prompts with a high-level overview—mentioning the relevant parts of the context (for example, “Based on our ECS system in ECS_PRINCPLES.md and the camera controls in 3D_CONTROLS_CONTEXT.md…”). Then discuss the issue or feature in depth.

Domain Separation: Organize your code by clearly separating concerns. For instance, isolate shader code, ECS logic, and control mechanics into dedicated modules or directories. This clarifies dependencies and makes your system more maintainable.

# Prompt Engineering Tips

## Be Specific with Context References:

Clearly indicate the exact context file(s) relevant to your question. For example:

“Based on the camera control methods in 3D_CONTROLS_CONTEXT.md and the ECS principles outlined in ECS_PRINCPLES.md, how can I improve the smoothness of transitions in the orbit mode?”

## Separate Overview and Detail:

Start with an overview of the problem and then include only the necessary code chunks or pseudocode for accuracy.

## Iterative Clarification:

Encourage follow-up questions for any ambiguity. For instance, mention:
“Please let me know if you need further context for the shader integration process detailed in DEV_TOOLS_CONTEXT.md.”

Context Management: Use an indexed, modular approach so that only the most relevant documents are provided to the AI. Automate or script extraction where possible.
Enhanced Workflow: Integrate linting, unit tests, and CI/CD practices to catch issues early and ensure smooth refactoring.
Code Quality: Keep code highly modular, well-documented, and well-separated into clear domains (ECS, shader system, controls). Optimize performance-critical parts and strengthen error handling.
Prompt Engineering: Structure your prompts methodically, include a minimal but sufficient context subset, and be open to iterative clarifications.
