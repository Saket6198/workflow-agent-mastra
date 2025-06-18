# Mastra Weather Workflow 🌦️

[![Node.js Version](https://img.shields.io/badge/Node.js-%3E%3D20.9.0-brightgreen.svg)](https://nodejs.org/)
[![License: ISC](https://img.shields.io/badge/License-ISC-blue.svg)](https://opensource.org/licenses/ISC)

![alt text](image.png)
A powerful weather assistant and activity planner powered by Mastra and AI-SDK. This project demonstrates how to build AI workflows with agents, tools, and steps in Mastra.

![Mastra Workflow Demo](https://via.placeholder.com/800x400?text=Mastra+Weather+Workflow)

## ✨ Features

- 🌡️ **Weather Forecasts**: Get accurate weather data for any location
- 🏄‍♂️ **Activity Planning**: Receive tailored activity recommendations based on weather conditions
- 🧠 **Intelligent Agent**: Interact with a helpful AI assistant for weather information
- 🔧 **Custom Tools**: Extensible weather utilities built with Mastra's tool system
- 🔄 **Workflow Management**: Orchestrate complex AI workflows with minimal code

## 📋 Prerequisites

- Node.js >= 20.9.0
- pnpm (recommended) or npm

## 🚀 Installation

1. **Clone the repository**

```bash
git clone https://github.com/yourusername/mastra-workflow.git
cd mastra-workflow
```

2. **Install dependencies**

```bash
pnpm install
```

3. **Configure environment** (optional)

If you want to persist data, make sure to update the LibSQLStore URL in both the index.ts and weather-agent.ts files.

## 💻 Usage

### Development

Start the development server:

```bash
pnpm dev
```

### Build

Build the project for production:

```bash
pnpm build
```

### Start Production Server

Run the built project:

```bash
pnpm start
```

## 🏗️ Project Structure

```
mastra-workflow/
├── package.json          # Project dependencies and scripts
├── src/                  # Source code
│   └── mastra/           # Mastra specific code
│       ├── index.ts      # Main entry point
│       ├── agents/       # AI agents
│       │   └── weather-agent.ts
│       ├── tools/        # Custom tools
│       │   └── weather-tool.ts
│       └── workflows/    # Workflow definitions
│           └── weather-workflow.ts
└── README.md             # This file
```

## 🧩 Core Components

### Workflows

Workflows in Mastra are composed of steps that process data in sequence. Each step has input/output schemas and execution logic.

```typescript
// Example of creating a workflow
const myWorkflow = createWorkflow({
  id: "my-workflow",
  inputSchema: z.object({
    // Define input schema using Zod
  }),
  outputSchema: z.object({
    // Define output schema using Zod
  }),
})
  .then(firstStep)
  .then(secondStep);

myWorkflow.commit();
```

### Agents

Agents are AI assistants powered by language models, with specific instructions and capabilities.

```typescript
// Example of creating an agent
const myAgent = new Agent({
  name: "My Assistant",
  instructions: `
    // Instructions for the agent
  `,
  model: google("gemini-1.5-pro-latest"), // Using Google's Gemini model
  tools: { myTool }, // Optional tools
  memory: new Memory({
    /* config */
  }), // Optional memory
});
```

### Tools

Tools extend agent capabilities, allowing them to perform specific tasks.

```typescript
// Example of creating a tool
const myTool = createTool({
  id: "my-tool",
  description: "Does something useful",
  inputSchema: z.object({
    // Define input schema using Zod
  }),
  outputSchema: z.object({
    // Define output schema using Zod
  }),
  execute: async ({ context }) => {
    // Tool implementation
    return { result: "success" };
  },
});
```

### Steps

Steps are the building blocks of workflows, performing specific operations.

```typescript
// Example of creating a step
const myStep = createStep({
  id: "my-step",
  description: "Processes some data",
  inputSchema: z.object({
    // Define input schema using Zod
  }),
  outputSchema: z.object({
    // Define output schema using Zod
  }),
  execute: async ({ inputData }) => {
    // Step implementation
    return { result: "processed" };
  },
});
```

## 📝 Examples

### Using the Weather Agent

```typescript
import { mastra } from './src/mastra';

// Create a conversation with the weather agent
const conversation = await mastra.createConversation({
  agentId: 'weatherAgent',
});

// Send a message to the agent
const response = await conversation.sendMessage('What's the weather like in Tokyo?');
console.log(response.content);
```

### Running the Weather Workflow

```typescript
import { mastra } from "./src/mastra";

// Execute the weather workflow
const result = await mastra.executeWorkflow("weatherWorkflow", {
  city: "New York",
});

console.log(result.activities);
```

## 🔄 Extending the Project

### Adding a New Tool

1. Create a new file in the `tools` directory
2. Define your tool using the `createTool` function
3. Export the tool
4. Add it to an agent in `agents/your-agent.ts`

### Creating a New Agent

1. Create a new file in the `agents` directory
2. Define your agent using the `Agent` class
3. Export the agent
4. Add it to the Mastra instance in `index.ts`

### Building a New Workflow

1. Create a new file in the `workflows` directory
2. Define your workflow steps using the `createStep` function
3. Create the workflow using the `createWorkflow` function
4. Connect steps with the `.then()` method
5. Call `.commit()` on the workflow
6. Export the workflow
7. Add it to the Mastra instance in `index.ts`

## 📚 Resources

- [Mastra Documentation](https://docs.mastra.ai)
- [AI-SDK Documentation](https://ai-sdk.dev)
- [Zod Documentation](https://zod.dev)

## 📄 License

This project is licensed under the ISC License - see the LICENSE file for details.

## 🙏 Acknowledgments

- [Open-Meteo API](https://open-meteo.com/) for providing free weather data
- [Google Gemini](https://ai.google.dev/) for the LLM capabilities
