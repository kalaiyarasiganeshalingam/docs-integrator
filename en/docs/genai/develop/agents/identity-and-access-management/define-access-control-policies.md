---
sidebar_position: 4
title: Defining Access Control Policies
description: Create AI agent evaluations in WSO2 Integrator. Fill the AI Evaluation form, pick an evalset to score against, and refine the checks in the visual designer.
keywords: [wso2 integrator, ai agent, evaluation, visual designer, llm-as-judge]
---

# Defining Access Control Policies

Access control policies define what protected tools, APIs, MCP servers, and enterprise resources an agent can access.

In WSO2 Integrator, access control is enforced using OAuth 2.0 scopes and client credentials configured for tools. These policies ensure that only authorized agents can invoke secured operations.

Authentication and authorization are handled separately:

- Agents authenticate using:
  - Agent ID
  - Agent Secret

- Tools authorize access using:
  - OAuth scopes
  - OAuth client credentials

This separation enables fine-grained and secure authorization management.

## Why access control policies are important

Access control policies help you:

- Restrict access to protected tools and APIs.
- Prevent unauthorized operations.
- Apply fine-grained authorization rules.
- Control permissions using scopes.
- Secure enterprise integrations.
- Govern and audit agent interactions.

## Access control model in WSO2 Integrator

Access to a protected tool is granted only when:

1. The agent identity is valid.
2. The OAuth application is authenticated.
3. The required scopes are authorized.

## Configure tool authorization

### Configure MCP tool

1. Click on the **MCP Toolkit** to open the configuration form.


2. In the **Auth Configuration Panel**, select the authentication type as **AgentIdAuthConfig** and update the values obtained from the authorization server:

     - **baseAuthUrl**  
        The base URL of the authorization server. This is used to initiate OAuth2 flows such as token generation and authorization.  
         Eg: `https://api.asgardeo.io/t/{tenant}/oauth2`

     - **clientId**  
        The unique identifier of the application registered in the authorization server. This is used to identify the agent during authentication.

     - **clientSecret**  
        The secret associated with the client ID. It is used to authenticate the client when requesting tokens.  
        Required only for **confidential clients** (not needed if PKCE is used with public clients).

     - **redirectUri**  
        The callback URL where the authorization server redirects after successful authentication. This must match the URL configured in the application.

     - **isPkceEnabled**  
        Indicates whether **PKCE (Proof Key for Code Exchange)** is enabled:

          - **true**: Recommended for public clients (more secure); set this to `true` if PKCE is enabled in the Asgardeo application
          - **false**: Used with client secret (confidential clients)

     - **scopes**  
         A list of permissions requested by the agent. These define what resources the agent can access.  
         If the tool does not define specific scopes, these scopes are used when generating the access token.

     - **secureSocket**  
         Configuration for SSL/TLS settings when communicating with secure endpoints.

3. In the same form, go to **Tools to Include** and select **Selected**.

4. Navigate to **Available Tools**, select the required tools, and click on the **Secure Access (Shield) icon** of the specific tool to add scopes.


### Configure Non-MCP tool

1. Click on the **3-dot menu** and then click **Edit**.  
   

2. Go to the **Advanced Configuration** and click **Expand**.

3. Fill the form with the values obtained from the authorization server.

4. Click **Save**.


## What's next

- [Test Agent Access Control Policies](test-agent-access-control-policies.md) - Validate and test authentication and authorization flows for secured agents and tools.
