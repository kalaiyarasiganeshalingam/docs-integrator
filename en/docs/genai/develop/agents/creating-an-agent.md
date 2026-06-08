---
sidebar_position: 2
title: Creating an Agent
description: Learn how to create and configure Chat agents and Inline agents in WSO2 Integrator.
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Creating an Agent

WSO2 Integrator supports the creation of two types of AI agents:

- Chat agents
- Inline agents

## Chat agents

Chat agents provide a chat-based interface for agents through HTTP REST APIs. They enable conversational interactions where users or external systems can send prompts, questions, or commands and receive intelligent responses powered by large language models (LLMs).

## Inline agents

These are embedded directly within integration flows, REST APIs, GraphQL resolvers, or backend service logic. They are invoked programmatically as part of workflow execution and are ideal for automation, enrichment, summarization, classification, and other AI-driven processing tasks.

Both agent types can be extended using tools and connectors provided by WSO2 Integrator. This enables them to interact with external systems such as Gmail, Google Calendar, databases, and custom APIs, allowing them to perform real-world actions in addition to generating intelligent responses.

## Launching the wizard

1. Open your integration project in WSO2 Integrator.
2. Click **+ Add Artifact** from the project view, or right-click the project tree.
3. The **Artifacts** page opens.

![Artifacts page in WSO2 Integrator showing all artifact categories.](/img/genai/develop/shared/07-artifacts-page-full.png)

## Create a chat agent

Under **AI Integration**, select **AI Chat Agent**. The wizard initially displays a single input field. The **Create** button remains disabled until a valid agent name is provided.

![The empty AI Chat Agent wizard with a Name field and a disabled Create button.](/img/genai/develop/agents/01-create-ai-chat-agent-wizard.png)

| Field | Required | Description |
|---|---|---|
| **Name** | Yes | Identifier for the agent, such as `BlogReviewer`, `SupportAssistant`, or `SalesAdvisor`. The name must start with a letter and contain only letters, numbers, and underscores. |

Enter a name (for example, `blogReviewer`) to enable the **Create** button.

After clicking **Create**, WSO2 Integrator generates the required integration artifacts and displays a progress indicator while configuring the service listener and related components.

When the wizard completes, WSO2 Integrator automatically generates the following:

- An HTTP service
- A listener endpoint
- An AI agent node
- An integration flow that handles incoming requests and generates responses

<Tabs>
<TabItem value="ui" label="Visual Designer" default>

![The AI agent canvas showing Start, an AI agent node with the agent name and an Add Memory button, and a Return node.](/img/genai/develop/agents/02-agent-flow-canvas.png)

</TabItem>

<TabItem value="code" label="Ballerina Code">

The generated Ballerina source for an agent named `blogReviewer` is similar to the following:

```ballerina
import ballerina/ai;
import ballerina/http;

// Default model provider
final ai:Wso2ModelProvider wso2ModelProvider =
    check ai:getDefaultModelProvider();

// Agent declaration
final ai:Agent blogReviewerAgent = check new (
    systemPrompt = {
        role: string `BlogReviewer`,
        instructions: string ``
    },
    model = wso2ModelProvider,
    tools = []
);

// Listener
listener ai:Listener chatAgentListener =
    new (listenOn = check http:getDefaultListener());

// Service
service /blogReviewer on chatAgentListener {

    resource function post chat(
            @http:Payload ai:ChatReqMessage request)
            returns ai:ChatRespMessage|error {

        string stringResult =
            check blogReviewerAgent.run(
                request.message,
                request.sessionId
            );

        return {message: stringResult};
    }
}
```

</TabItem>
</Tabs>

## Create an inline agent

You can add an inline agent within integration flows, REST APIs, GraphQL resolvers, or backend service logic.

1. Create or open an existing integration flow.
2. Click the **+** button in the flow to open the side panel.
3. Under the **AI** section, click **Agent**, then click **+ Add Agent** to open the agent creation panel.

![Agent creation form](/img/genai/develop/agents/39-agent-creation-form.png)

4. Configure the **Role** and **Instructions** fields to define the agent’s behavior.
5. Switch the **Query** field from `Text` mode to `Expression` mode, and provide the `query` parameter as the input.
6. Click **Save**.

<Tabs>
<TabItem value="ui" label="Visual Designer" default>

![Agent creation form](/img/genai/develop/agents/40-agent.png)

</TabItem>

<TabItem value="code" label="Ballerina Code">

```ballerina
import ballerina/ai;
import ballerina/log;

// Default model provider
final ai:Wso2ModelProvider aiWso2modelprovider =
    check ai:getDefaultModelProvider();

// Agent declaration
final ai:Agent aiAgent = check new (
    systemPrompt = {
        role: string `Task Assistant`,
        instructions: string `You are a helpful assistant for
            managing a to-do list. You can manage tasks and
            help users plan their schedules.`
    },
    model = aiWso2modelprovider
);

// Main
public function main() returns error? {
    do {
        string query = "Hi";
        string stringResult = check aiAgent.run(string `${query}`);
    } on fail error e {
        log:printError("Error occurred", 'error = e);
        return e;
    }
}
```

</TabItem>
</Tabs>

After generation, you are directed to the integration canvas where you can configure the following aspects of the agent:

- [Agent behavior, including role, instructions, query, and input/output bindings](./creating-an-agent.md#configure-agent-behavior)
- [Model provider](../components/model-providers.md)
- [Tool integration](./tools.md)
- [Memory configuration](./memory.md)
- [Observability and tracing](./observability.md)

## Configure agent behavior

Use the AI agent node configuration panel to customize how the agent behaves and responds to requests.

Click the `AI Agent` node to open the configuration panel and update the following configurations.

| Section | Required | Description |
|---|---|---|
| **Role** | Yes | Defines the primary responsibility or persona of the agent. |
| **Instructions** | Yes | Specifies the behavior guidelines and operational instructions that the agent should follow while responding. |
| **Advanced Configuration** | No | Provides additional runtime and execution settings for the agent. |
| **Result** | Yes | Defines the output or response generated by the agent after execution. |

 ### Advanced configuration
 
| Section | Required | Description |
|---|---|---|
| **Maximum Iterations** | No | Defines the maximum number of reasoning or execution cycles the agent can perform before returning a response. |
| **Verbose** | No | Enables detailed execution logs and intermediate reasoning information for debugging and observability purposes. |
| **Tool Loading Strategy** | No | Determines how tools are discovered and loaded by the agent during execution. |
| **Agent Credential** | No | Configures the credentials or authentication details used by the agent when accessing external systems or tools. |
| **Context** | No | Defines contextual information that is passed to the agent during execution. |
| **Type Descriptor** | No | Specifies the expected structure or type information for agent inputs and outputs. |

 ## What's next

- **[Tools](tools.md)** - Add tools and integrations to the agent.
- **[Memory](memory.md)** - Configure conversational and persistent memory.
- **[Identity & access management](identity-and-access-management.md)** - Secure agents, tools, and integrations using authentication and authorization.
- **[Observability](observability.md)** - Monitor traces, logs, and execution details.
- **[Evaluations](evaluations/overview.md)** - Test and evaluate agent behavior and response quality.
