---
sidebar_position: 5
title: Test Agent Identity & Access Control
description: Learn how to test authentication and authorization for protected AI agents and tools in WSO2 Integrator.
keywords: [wso2 integrator, ai agent, authentication, authorization, oauth2, scopes, access control]
---

# Test Agent Identity & Access Control

This section explains how to test authentication and authorization for protected tools in WSO2 Integrator.

## Reduce access token expiry time

For testing purposes, reduce the access token expiry time to force token regeneration quickly.

- Open the created application in Asgardeo.
- Navigate to **Protocol**.
- Update **User Access Token Expiry Time** to 60.
- Save the configuration.

## Test authorized access

- Open the **Tracing** view.
- Click **Chat**.
- Ask the following query:
   ```text
   Should I go for a walk in Colombo now?
   ```
- Verify that the protected tool invocation succeeds and the response is returned successfully.
![Authorized Access](/img/genai/develop/agents/36-agant-identity.png)  

## Test unauthorized access
- Open the Asgardeo console.
- Navigate to **User Management** > **Roles**.
- Open the assigned role.
- Go to the **Permissions** section.
- Remove the **read_current_weather** scope from Permissions (Scopes).
- Save the changes.

## Test access again

- Return to the agent chat.
- Ask the same query again:
       ```text
       Should I go for a walk in Colombo now?
       ```
- Verify that the request fails because the required scope is no longer authorized.

![Unauthorized Access ](/img/genai/develop/agents/37-unauthorized-access.png) 

- Click **View Trace** and inspect the error trace.

![Agent tracing ](/img/genai/develop/agents/38-agent-trace.png)
