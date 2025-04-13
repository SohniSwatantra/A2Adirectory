
# A2ADirectory: Your Hub for the Agent2Agent (A2A) Protocol

[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](CONTRIBUTING.md)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE) **Welcome to A2ADirectory! This repository serves as a community-curated collection of resources, implementations, tools, and examples related to Google's Agent2Agent (A2A) protocol, designed to foster interoperability between diverse AI agents.**

---

## Table of Contents

1.  [Introduction to A2A](#introduction-to-a2a)
    * [What is it?](#what-is-it)
    * [Why is it important?](#why-is-it-important)
    * [Guiding Principles](#guiding-principles)
2.  [Understanding the Protocol](#understanding-the-protocol)
    * [Core Components](#core-components)
    * [Communication Flow (Simplified)](#communication-flow-simplified)
3.  [The Directory: A2A Resources](#the-directory-a2a-resources)
    * [Official Documentation & Specifications](#official-documentation--specifications)
    * [Implementations & Libraries](#implementations--libraries)
        * [Official Code Samples](#official-code-samples)
        * [Community Contributions](#community-contributions)
    * [Tools & Utilities](#tools--utilities)
    * [Demonstrations & Use Cases](#demonstrations--use-cases)
    * [Learning Materials](#learning-materials)
    * [Related Technologies](#related-technologies)
4.  [Community & Getting Involved](#community--getting-involved)
    * [Official Channels](#official-channels)
    * [Contribute to this Directory](#contribute-to-this-directory)
5.  [Project Vision](#project-vision)

---

## Introduction to A2A

### What is it?

Agent2Agent (A2A) is an **open protocol** initiated by Google and its partners. Its primary goal is to enable **different AI agents**, potentially built using various frameworks or operated by different vendors, to **communicate securely and effectively**. Think of it as a common language for AI agents to collaborate on tasks.

### Why is it important?

Modern AI often exists in silos. A2A aims to break these down, allowing for:

* **Enhanced Automation:** Agents can delegate sub-tasks to other specialized agents.
* **Cross-Application Workflows:** Create more powerful applications by combining the strengths of multiple AI systems.
* **Interoperability:** Avoid vendor lock-in and promote a healthier ecosystem.
* **Complex Task Handling:** Tackle problems that require diverse capabilities or long-running processes.

### Guiding Principles

The design of A2A follows several key principles:

* **Simplicity:** Leverages well-established standards like HTTP, JSON-RPC 2.0, and Server-Sent Events (SSE).
* **Enterprise-Grade:** Built with considerations for Authentication, Security, Privacy, and Monitoring from the ground up.
* **Asynchronous by Design:** Natively supports long-running operations and workflows that might require human intervention.
* **Flexible Data Handling:** Supports various data types (modalities) including text, files, structured forms, streams, etc.
* **Opaque Interaction:** Agents can interact based on defined capabilities without needing to know each other's internal workings or tools.

---

## Understanding the Protocol

### Core Components

* **Agent Card:** A JSON file published by an agent describing its capabilities, API endpoint, required authentication, and other metadata. This is key for discovery.
* **Task:** Represents the work request sent from a client agent to a server agent.
* **Message:** Contained within a Task or Artifact, holding the actual content being exchanged.
* **Part:** A component of a Message or Artifact, representing a piece of data (e.g., text, a file URI, structured data). Allows for multi-modal communication.
* **Artifact:** Represents the result or output generated by an agent after processing a Task. Like Messages, they contain Parts.

### Communication Flow (Simplified)

1.  **Discovery:** A *Client Agent* finds the *Agent Card* of a *Remote Agent (Server)* it wants to interact with.
2.  **Request:** The Client sends a *Task* (containing a *Message* with *Parts*) via an HTTP POST request using JSON-RPC 2.0 to the Server's endpoint.
3.  **Processing:** The Server Agent receives the Task, validates it, and begins processing. It updates the Task's `status` internally.
4.  **Response:** Once processing is complete (or an error occurs), the Server sends a JSON-RPC response containing the final `status` and any resulting *Artifacts* (which contain *Parts*).
5.  **Streaming Updates (Optional):** For long-running tasks, the Server can push `TaskStatusUpdateEvent` or `TaskArtifactUpdateEvent` updates to the Client via Server-Sent Events (SSE) or use Push Notifications.

*For the definitive technical details, refer to the [Official Technical Documentation](https://google.github.io/A2A/#/documentation).*

---

## The Directory: A2A Resources

This section aims to list valuable resources for learning, building, and deploying A2A-enabled agents.

### Official Documentation & Specifications

* **[A2A Protocol Website](https://google.github.io/A2A)**: The central hub for official documentation.
* **[A2A GitHub Repository (google/A2A)](https://github.com/google/A2A)**: Source for documentation, specifications, and official sample code.
* **[Technical Documentation](https://google.github.io/A2A/#/documentation)**: Detailed breakdown of the protocol, actors, transport, auth, and core objects.
* **[JSON Schema Specification](https://github.com/google/A2A/tree/main/specification/json)**: The raw schema definitions for A2A data structures.
* **[Announcement Blog Post](https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/)**: Context and motivation behind the protocol.

### Implementations & Libraries

#### Official Code Samples

*(Found within the [google/A2A repository](https://github.com/google/A2A/tree/main/samples))*

* **Python:**
    * `common`: Core library for HTTP/JSON-RPC/SSE. ([Link](https://github.com/google/A2A/tree/main/samples/python/common))
    * `hosts/cli`: Example command-line client. ([Link](https://github.com/google/A2A/tree/main/samples/python/hosts/cli))
    * `agents/langgraph`: LangGraph agent sample (currency conversion). ([Link](https://github.com/google/A2A/tree/main/samples/python/agents/langgraph))
    * `agents/crewai`: CrewAI agent sample (image generation). ([Link](https://github.com/google/A2A/tree/main/samples/python/agents/crewai))
    * `agents/google_adk`: Google ADK agent sample (expense report). ([Link](https://github.com/google/A2A/tree/main/samples/python/agents/google_adk))
* **JavaScript/TypeScript:**
    * `server`: Core server implementation (Express-based). ([Link](https://github.com/google/A2A/tree/main/samples/js/src/server))
    * `client`: Client implementation library. ([Link](https://github.com/google/A2A/tree/main/samples/js/src/client))
    * `agents`: Genkit agent sample (movie info/code gen). ([Link](https://github.com/google/A2A/tree/main/samples/js/src/agents))

#### Community Contributions

* *Looking for libraries, SDKs, or integrations for other languages and frameworks! Add yours via a Pull Request.*
    * [Your Library/SDK Name] - [Link] - Brief description (e.g., "Rust server implementation").

### Tools & Utilities

* *Help build this section! Add tools for validation, discovery, monitoring, etc.*
    * [Tool Name] - [Link] - Description (e.g., "A2A Agent Card Validator").

### Demonstrations & Use Cases

* **[Official Multi-Agent Web App Demo](https://github.com/google/A2A/tree/main/demo)**: Python/Mesop demo showcasing an orchestrator agent interacting with multiple A2A agents.
* **[Official Demo Video](https://storage.googleapis.com/gweb-developer-goog-blog-assets/original_videos/A2A_demo_v4.mp4)**: Video walkthrough of the protocol in action.
* *[Your Project Demo]* - [Link] - Description.

### Learning Materials

* *[Article/Tutorial Title]* - [Link] - Description (e.g., "Building your first A2A agent with Framework X").

### Related Technologies

* **[Model Context Protocol (MCP)](https://github.com/modelcontextprotocol/servers)**: A complementary protocol focused on providing tools and context *to* agents. See [A2A and MCP Relationship](https://google.github.io/A2A/#/topics/a2a_and_mcp.md).

---

## Community & Getting Involved

### Official Channels

* **[google/A2A GitHub Issues](https://github.com/google/A2A/issues)**: Report bugs or propose changes to the official protocol specification or samples.
* **[google/A2A GitHub Discussions](https://github.com/google/A2A/discussions/)**: Ask questions, share ideas, and discuss A2A with the community and maintainers.
* **[Private Feedback Form](https://docs.google.com/forms/d/e/1FAIpQLScS23OMSKnVFmYeqS2dP7dxY3eTyT7lmtGLUa8OJZfP4RTijQ/viewform)**: For feedback you prefer to share privately with the Google team.

### Contribute to this Directory

**This repository thrives on community contributions! If you know of a resource, tool, implementation, or example that isn't listed here, please help us add it:**

1.  **Check the [Issues](https://github.com/YOUR_USERNAME/A2ADirectory/issues)**: See if someone else has already suggested it.
2.  **Create an Issue:** If not, create a new issue to suggest the addition.
3.  **Submit a Pull Request:** Fork the repository, add your resource to the appropriate section in this README, and submit a PR! Please follow the guidelines in [CONTRIBUTING.md](CONTRIBUTING.md).

---

## Project Vision

The goal of `A2ADirectory` is to become the go-to, community-driven index for navigating the Agent2Agent protocol ecosystem. We aim to keep it up-to-date, well-organized, and genuinely useful for developers, researchers, and anyone interested in AI agent interoperability. Your contributions are vital to achieving this vision!

---
