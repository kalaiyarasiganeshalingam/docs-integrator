---
sidebar_position: 5
title: Test Identity & Access Management
description: Learn how to test authentication and authorization for protected AI agents and tools in WSO2 Integrator.
keywords: [wso2 integrator, ai agent, authentication, authorization, oauth2, scopes, access control]
---

# Test Identity & Access Management

This section explains how to test authentication and authorization for protected tools in WSO2 Integrator.

## Reduce access token expiry time

For testing purposes, reduce the access token expiry time to force token regeneration quickly.

1. Open the created application in Asgardeo.
2. Navigate to **Protocol**.
3. Update **User Access Token Expiry Time** to 60.
4. Save the configuration.

## Test authorized access

1. Open the **Tracing** view.
2. Click **Chat**.
3. Ask the following query:
   ```text
   Should I go for a walk in Colombo now?
   ```
4. Verify that the protected tool invocation succeeds and the response is returned successfully.
![Authorized Access](/img/genai/develop/agents/36-identity.png)  

## Test unauthorized access

1. Open the Asgardeo console.
2. Navigate to **User Management** > **Roles**.
3. Open the assigned role.
4. Go to the **Permissions** section.
5. Remove the **read_current_weather** scope from Permissions (Scopes).
6. Save the changes.
7. Return to the agent chat and ask the same query again:
   ```text
   Should I go for a walk in Colombo now?
   ```
8. Verify that the request fails because the required scope is no longer authorized.

![Unauthorized Access](/img/genai/develop/agents/37-unauthorized-access.png)

9. Click **View Trace** and inspect the error trace.

![Agent tracing](/img/genai/develop/agents/38-agent-trace.png)
