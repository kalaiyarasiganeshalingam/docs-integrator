---
sidebar_position: 3
title: Defining Agent Identies
description: Create AI agent evaluations in WSO2 Integrator. Fill the AI Evaluation form, pick an evalset to score against, and refine the checks in the visual designer.
keywords: [wso2 integrator, ai agent, evaluation, visual designer, llm-as-judge]
---

# Defining Agent Identies

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

- Click on **Agent** to open the configuration form. Then, go to **Advanced Configuration** and expand it.

![AI Chat Agent canvas with the Tracing toggle in the top-right showing 'Tracing: Off'.](/img/genai/develop/agents/30-advence-configuration.png)


- Update the credentials by providing the **Agent ID** and **Agent Secret** obtained from the authorization server.

![AI Chat Agent canvas with the Tracing toggle in the top-right showing 'Tracing: Off'.](/img/genai/develop/agents/31-add-credential.png)

## What's next

- [Define Access Control Policies](define-access-control-policies.md) - Configure scopes, permissions, and authorization policies for agent access.
- [Test Agent Access Control Policies](test-agent-access-control-policies.md) - Validate and test authentication and authorization flows for secured agents and tools.


