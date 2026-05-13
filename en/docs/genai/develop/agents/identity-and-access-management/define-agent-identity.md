---
sidebar_position: 3
title: Defining Agent Identity
description: Learn how to define and manage Identity for autonomous AI agents in WSO2 Integrator using Agent ID and Agent Secret for secure authentication.
keywords: [wso2 integrator, ai agent, agent identity, authentication, agent id, agent secret, credentials, oauth2]
---

# Defining Agent Identity

Agent identities are used to authenticate autonomous AI agents before they access protected tools, APIs, MCP servers, and enterprise resources.

In WSO2 Integrator, authentication and authorization are handled separately to provide secure and fine-grained access control.

- Agents are authenticated using:
  - Agent ID
  - Agent Secret

- Tools are authorized using:
  - OAuth scopes
  - OAuth client credentials

This separation enables secure agent authentication while allowing tools to independently enforce authorization policies and scope-based access control.

With this model, only authenticated agents with the required permissions can invoke protected tools and resources.

## Add credential to Agent

1. In the visual designer, click on your **Agent** to open the configuration form. Then, go to **Advanced Configuration** and expand it.

   ![Advanced Configuration panel expanded on the Agent configuration form.](/img/genai/develop/agents/30-advence-configuration.png)

2. Update the credentials by providing the **Agent ID** and **Agent Secret** obtained from the authorization server.

   ![Credential input fields showing Agent ID and Agent Secret fields.](/img/genai/develop/agents/31-add-credential.png)

## What's next

- [Define Access Control Policies](define-access-control-policies.md) - Configure scopes, permissions, and authorization policies for agent access.
- [Test Identity & Access Management](test-identity-and-access-management.md) - Validate and test authentication and authorization flows for secured agents and tools.


