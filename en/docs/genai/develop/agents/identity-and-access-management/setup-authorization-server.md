---
sidebar_position: 2
title: Set up an Authorization Server
description: Learn how to configure an Authorization Server for securing AI agents, tools, and APIs in WSO2 Integrator using Asgardeo and OAuth 2.0.
keywords: [wso2 integrator, ai agent, authorization server, oauth2, authentication, asgardeo, identity, access control]
---

# Set up an Authorization Server

To secure agent interactions, tools, and APIs, you must configure an Authorization Server. WSO2 Integrator supports OAuth 2.0-based authentication and authorization through external identity providers such as Asgardeo.

This guide explains how to configure Asgardeo for AI agent authentication and access control.

Before you begin, ensure you have an [Asgardeo account](https://wso2.com/asgardeo/docs/get-started/create-asgardeo-account/).

## Register an AI agent

1. Sign in to [Asgardeo Console](https://wso2.com/asgardeo/) and navigate to **Agents**.

2. Click **+ New Agent**.

3. Provide the following details:

   - **Name**: A descriptive name for your AI agent.  
     Example: `Math Assistant Agent`

   - **Description** *(optional)*: A short description of the agent’s purpose.  
     Example: `An AI agent that invokes protected MCP tools to answer math-related questions.`

4. Click **Create**.

After the agent is created, Asgardeo generates:

- **Agent ID**
- **Agent Secret**

The Agent Secret is displayed only once. Store it securely because it is required later when configuring authentication.

## Configure resources

Resources define the APIs or MCP servers that agents are allowed to access.

1. In the Asgardeo console, navigate to **Resources**.

2. Select one of the following based on your integration type:

   - **MCP Servers** for MCP-based integrations
   - **API Resources** for non-MCP services

3. Click:

   - **+ New MCP Server**, or
   - **+ New API Resource**

4. Provide the required details:

   - **Identifier**: `mcp://localhost:9090`
   - **Display Name**: `Math Operations`

5. Click **Next**.

6.  Add scopes for resource authorization.

   After filling the following fields, click **+ Add Scope**.

   Example:

   - **Scope**: `add`
   - **Display Name**: `add`
   - **Description** *(optional)*: ``

7. Click **Create**.

## Register an application

Applications allow agents to authenticate and invoke secured tools and APIs.

Depending on your integration type, configure one of the following application types:

- **Configure an MCP application** - Use this option for MCP-based integrations.
- **Configure a Non-MCP application** - Use this option for standard OAuth 2.0-protected APIs and tools.

### Configure an MCP application

Use this option when working with MCP-based integrations.

1. In the Asgardeo console, navigate to **Applications** > **New Application**.

2. Select **MCP Client Application**.

3. Provide the following details:

   - **Name**: `AgentAuthenticatorApp`
   - **Authorized Redirect URL**: `http://localhost:6274/oauth/callback`

4. Complete the wizard.

5. Open the **Advanced** tab.

6. Enable **App-Native Authentication API**.

### Configure a Non-MCP application

Use this option for standard OAuth 2.0-protected APIs and tools.

1. In the Asgardeo console, navigate to **Applications** > **New Application**.

2. Select **Standard-Based Application**.

3. Configure the application:

   - **Name**: `AgentAuthenticatorApp`
   - **Protocol**: `OAuth2.0 OpenID Connect`
   - Enable **Allow AI agents to sign into this application**

4. Click **Create**.

5. Open the **Protocol** tab and configure the following:

   - **Allowed Grant Types**: Enable **Client Credential**
   - **Authorized Redirect URLs**: `http://localhost:6274/oauth/callback`
   - **PKCE**: Enable or disable based on your requirements
   - **Access Token** > **Token Type**: `JWT`

## Authorize APIs

After creating the application, authorize the required resources and scopes.

1. Navigate to the **Authorize** tab.

2. Click **+ Authorize Resource**.

3. Configure the following:

   - **Resources**: Select the created resource
   - **Authorized Scopes**: Select the required scopes

4. Click **Finish**.

## Configure roles

Roles help manage authorization policies and permissions for agents.

1. In the Asgardeo console, navigate to **User Management** > **Roles**.

2. Click **+ New Role**.

3. Provide the following details:

   - **Role Name**: `AgentRole`
   - **Role Audience**: `Application`
   - **Assigned Application**: Select the created application

4. Click **Next**.

5. Select the created resource and assign the required permissions.

6. Click **Finish**.

7. Open the **Agents** tab.

8. Click **+ Assign Agent**.

9. Select the created agent and assign the role.

After completing these steps, your Authorization Server configuration is ready, and you can proceed with securing agents, tools, and APIs in WSO2 Integrator.

After completing these steps, your Authorization Server configuration is ready, and you can proceed with securing agents, tools, and APIs in WSO2 Integrator.

Once the setup is complete, you can obtain the following details:

- **Agent ID**
- **Agent Secret**
- **Client ID**
- **Client Secret** *(available when the application is configured as a non-public client)*
- **Redirect URI**
- **Base URL** *(To obtain the base URL, open the created application and navigate to the **Info** tab.)

## What's next

- [Define Agent Identities](define-agent-identities.md) - Create and manage identities for autonomous agents.
- [Define Access Control Policies](define-access-control-policies.md) - Configure scopes, permissions, and authorization policies for agent access.
- [Test Agent Access Control Policies](test-agent-access-control-policies.md) - Validate and test authentication and authorization flows for secured agents and tools.
