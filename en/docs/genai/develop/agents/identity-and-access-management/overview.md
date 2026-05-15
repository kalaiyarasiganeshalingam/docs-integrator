---
sidebar_position: 1
title: Identity & Access Management
description: Learn how to secure AI agents, tools, and integrations using Identity and Access Control in WSO2 Integrator.
keywords: [wso2 integrator, ai agent, identity, access control, oauth2, authorization, authentication, agent security]
---

# Identity & Access Management

AI agents interact with MCP servers, APIs, databases, and enterprise systems to perform tasks autonomously. As agents gain access to enterprise resources and external services, it becomes essential to secure and govern these interactions through proper identity and access control mechanisms.

WSO2 Integrator provides built-in support for securing agents, tools, and service integrations using authentication and authorization standards such as OAuth 2.0. In the WSO2 platform, agents are treated as first-class identities, allowing organizations to manage agent access in a secure, controlled, and traceable manner.

With Identity and Access Control, you can:

- Define and manage identities for agents and tools.
- Secure tool invocations using OAuth 2.0 authentication.
- Configure fine-grained access control policies.
- Validate and authorize incoming requests.
- Integrate with external Authorization Servers and identity providers.
- Control access to enterprise systems and protected resources.
- Monitor and govern agent interactions securely.

These capabilities help ensure that all agent activities are secure, auditable, and compliant with enterprise governance standards.

:::note
WSO2 Integrator currently supports Identity and Access Control only for autonomous agents.
:::

## What's next

- [Set up an Authorization Server](setup-authorization-server.md) - Configure Asgardeo and OAuth 2.0 authentication for agents and tools.
- [Define Agent Identity](define-agent-identity.md) - Create and manage identities for autonomous agents.
- [Define Access Control Policies](define-access-control-policies.md) - Configure scopes, permissions, and authorization policies for agent access.
- [Test Identity & Access Management](test-identity-and-access-management.md) - Validate and test authentication and authorization flows for secured agents and tools.
