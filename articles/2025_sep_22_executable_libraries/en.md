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

# Example (The Implementation)

# Conclusion

Share your thoughts in the comments :-) this will help make this thread visible to others and will be great support and motivation :-)

Thank you for your time and have a good day!
