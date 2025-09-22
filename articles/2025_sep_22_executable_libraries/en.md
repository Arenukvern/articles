# Libraries as Agentic Executables

Or how to make, install, uninstall libraries in Agentic World. (using AI - LLM powered agents)

This problem follows three part structure:

1. Why (The Problem)
2. How (The Solution)
3. Example (The Implementation)

If you want to skip to the example, you can do it by clicking [here](#example-the-implementation).

Let's start with the Why (The Problem) part.

# Why (The Problem)

In the current time and year of writing this article, for any development project (i.e. coded project), we usually use libraries or packages to reuse code effectively.

Some of the libraries, usually configurable ones, often have extensive documentation and examples not only how to install, but how to configure, use, test and uninstall it.

The common installation, configuration and usage pattern may look like this:

1. use CLI or package manager to install/find the library
2. read the documentation of what we need to do to use it.
3. analyze your codebase to see how we can integrate it.
4. try to apply the actual code from the library to your codebase and your solution (from codebase structure/architecture point of view)
5. configure the library if needed.
6. try to test (visually or using tests) to see if it works.
7. modify the code if corrections are needed.
8. add tests or configuration if needed.

Usually, most of these steps, we try to follow as humans - step by step.

However, with the rise of AI Agents - what if we will treat libraries and packages not as abstract reusable parts of code, but as the abstract executable programs, with the same ability to be installed, configured, used and uninstalled as usual programs?

If you imagined it - let's call it "Agentic Executables" (below - "AE") and dive into the how we can create / maintain them:)

# How (The Solution)

As first thing, let's establish meta rules to create and modify files of AE:

1. AE Domain Knowledge - terms, concept, principles of what is AE to give enough context for AI Agent. This file will help us to maintain the files.
2. Installation creation with three logical steps:

- 1. Installation (using CLI or package manager)
- 2. Configuration
- 3. Integration

3. Usage creation.
4. Uninstallation creation.

With all of that, let's define the principles of working with AE.

# Working principles:

The core idea is to pass meta rules to AI Agent to give him ability to:

1. maintain the library executables (basically - meta instructions)
   1.1 The basic terms & domain knowledge (what is AE and how it works) - `ae_context.md`
   GOAL: To maintain `ae_bootstrap` and `ae_usage` files
   USER: Maintainer of the library
   1.2 The drop file to maintain the library executables - `ae_bootstrap.md`.
   GOAL: To create ae files structure and maintain it.
   USER: Maintainer of the library
   1.3 The drop file to use ae files in library - `ae_usage.md`
   GOAL: To use ae files of this library.
   USER: User (in other words - developer who uses this library)
2. ability to install / uninstall / update (basically, one time to use rules)
   2.1 Installation, Configuration, Integration files - `ae_install.md`
   GOAL: To install, configure and integrate the library.
   USER: User
   2.2 Uninstallation file - `ae_uninstall.md`
   GOAL: To uninstall the library.
   USER: User
   2.3 Update file - `ae_update.md`
   GOAL: To update the library from old version to new one.
   USER: User
3. ability to use the library frequently / or depending of its usage needs. Created via `ae_use.md` file.
   3.1 Usage file - the rule, adapted to the library name. For example, for library name `go_router` and Cursor AI usage it can be a rule in the path `go_router_usage.mdc`. During installation to User Codebase , AI Agent needs to ask User what AI Agent should be used, and place / name it according to it. For example, if User wants to use Cursor AI, AI Agent should place this rule to the path `.cursor/rules/go_router_usage.mdc`.
   GOAL: To use the library frequently / or depending of its usage needs.
   USER: User

The AE files structure:

```
root/
├── ae/
│   ├── ae_context.md
│   ├── ae_bootstrap.md
│   ├── ae_use.md
```

The library AE files will be located in the `root/ai_use` folder.
At the end this would be the structure of the library AE files:

```
root/
├── ai_use/
│   ├── ae_install.md
│   ├── ae_uninstall.md
│   ├── ae_update.md
│   ├── {library_name}_use.md
```

# Example (The Implementation)

# Conclusion

Share your thoughts in the comments :-) this will help make this thread visible to others and will be great support and motivation :-)

Thank you for your time and have a good day!
