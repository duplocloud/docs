# AI HelpDesk

## Overview

AI HelpDesk serves as the central interface through which users engage with AI Agents in the DuploCloud ecosystem. It provides a structured, collaborative environment where DevOps tasks and infrastructure management operations can be executed with AI assistance while maintaining human oversight. The HelpDesk is designed to replicate the collaborative experience between engineers, offering visualization tools, command execution capabilities, and intuitive communication channels. This component of the AI Suite bridges the expertise gap in cloud operations by making specialized AI assistance readily available to all users regardless of their technical background.

## Tickets

Tickets form the foundation of interaction within the AI HelpDesk, establishing a dedicated communication channel between a human user and an assigned AI Agent. Each ticket represents a specific task, request, or troubleshooting session that requires attention. When creating a ticket, users can select the appropriate AI Agent based on the nature of the task (such as Kubernetes troubleshooting, observability analysis, or deployment assistance). This ticketing system maintains context throughout the conversation, allowing for continuous collaboration until resolution while preserving a complete audit trail of actions and decisions for future reference.

### Canvas

The Canvas is a dynamic, shared workspace within the HelpDesk Ticket that facilitates real-time collaboration between users and AI Agents. This interactive environment serves as a virtual "whiteboard" where both parties can visualize operations, execute commands, and share information seamlessly. This shared visual interface significantly enhances the effectiveness of human-AI interaction by providing transparency into the AI's reasoning and actions while allowing users to contribute their expertise when needed.

#### AI Suggested Commands

Within the Canvas, AI agents can analyze the current context and proactively suggest relevant terminal commands to address the task at hand. These suggested commands appear as interactive elements that users can approve, reject, ignore, or execute. This feature combines the AI's extensive knowledge of best practices with human judgment, preventing potentially harmful operations while expediting routine tasks. Each suggestion includes a brief explanation of its purpose and expected outcome, enabling users to learn while accomplishing their objectives efficiently.

#### Terminal

The Terminal component embedded within the Canvas provides users with direct command-line access to their infrastructure. When a user interacts with the Terminal, the AI Agent can observe these interactions, providing context-aware assistance, explaining unexpected outputs, or suggesting follow-up commands. This bidirectional visibility creates a seamless experience where users can freely switch between AI-guided operations and manual intervention. The Terminal maintains appropriate permission boundaries based on the user's role while providing the familiar command-line interface that DevOps professionals expect.

Users are also able to establish an interactive terminal session directly within a running application container from the HelpDesk Canvas. This capability is invaluable for troubleshooting application-specific issues, verifying configurations, or performing targeted diagnostics. The AI agent remains engaged during these application container shell sessions, offering assistance with application-specific commands and interpreting outputs in the context of the application's architecture. This deep level of access, combined with AI guidance, dramatically reduces the time required to identify and resolve application-level issues while maintaining security boundaries.
