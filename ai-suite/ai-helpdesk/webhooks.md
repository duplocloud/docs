---
hidden: true
---

# Webhooks

## Webhook Integration Guide

### Overview

DuploCloud AI ServiceDesk provides powerful webhook capabilities that allow you to seamlessly integrate your ServiceDesk environment with third-party systems. Webhooks deliver real-time notifications when specific events occur in ServiceDesk, enabling you to automate workflows, synchronize data, and build custom integrations.

This document provides comprehensive information about the webhook capabilities of DuploCloud ServiceDesk, including available webhook events, payload structures, and integration best practices.

### Webhook Capabilities

ServiceDesk webhooks allow external systems to receive notifications when various ticket-related events occur. These notifications are sent as HTTP POST requests to a specified endpoint URL that you configure in your integration.

#### Supported Webhook Events

ServiceDesk supports a comprehensive set of webhook events organized by resource type. Each webhook includes the action identifier in the payload, allowing your integration to handle different events appropriately.

**Ticket Management Actions**

| Action Identifier                     | Description                                           |
| ------------------------------------- | ----------------------------------------------------- |
| `GET:Ticket/GetTicket`                | Retrieve a specific ticket by ID                      |
| `GET:Ticket/GetTicketMessages`        | Retrieve all messages for a specific ticket           |
| `GET:Ticket/ListTicket`               | List tickets based on provided filters                |
| `POST:Ticket/AddTicket`               | Create a new ticket in ServiceDesk                    |
| `POST:Ticket/SendTicketMessage`       | Add a message to an existing ticket                   |
| `POST:Ticket/StoreNextMessageContext` | Store context for the next message in a ticket thread |

**Agent Management Actions**

| Action Identifier                                   | Description                                |
| --------------------------------------------------- | ------------------------------------------ |
| `GET:AgentBuildDefinition/ListAgentBuildDefinition` | List all agent build definitions           |
| `GET:AgentDefinition/GetAgentDefinition`            | Retrieve a specific agent definition by ID |
| `GET:AgentDefinition/GetAgentRegistrations`         | Get registrations for a specific agent     |
| `GET:AgentDefinition/ListAgentDefinition`           | List all agent definitions                 |
| `PUT:AgentDefinition/UpdateAgentDefinition`         | Update an existing agent definition        |
| `GET:ServiceDeskAgents/GetAllowedAgentInstances`    | Get all agent instances allowed for a user |

**Tool Management Actions**

| Action Identifier                         | Description                               |
| ----------------------------------------- | ----------------------------------------- |
| `GET:ToolDefinition/GetToolDefinition`    | Retrieve a specific tool definition by ID |
| `GET:ToolDefinition/ListToolDefinition`   | List all tool definitions                 |
| `GET:ToolDefinition/ListToolsPackages`    | List all packages for tools               |
| `PUT:ToolDefinition/UpdateToolDefinition` | Update an existing tool definition        |

**Vector Database Actions**

| Action Identifier                           | Description                                     |
| ------------------------------------------- | ----------------------------------------------- |
| `GET:VectorDb/GetVectorDb`                  | Retrieve a specific vector database by ID       |
| `GET:VectorDb/ListVectorDb`                 | List all vector databases                       |
| `GET:VectorDb/ListVectorDbProcessedFiles`   | List all processed files in a vector database   |
| `GET:VectorDb/ListVectorDbUnprocessedFiles` | List all unprocessed files in a vector database |

**Other Actions**

| Action Identifier                                | Description                           |
| ------------------------------------------------ | ------------------------------------- |
| `GET:ChunkingBuildDefinition/ListArchivedBuilds` | List all archived chunking builds     |
| `GET:Settings/GetSettings`                       | Retrieve specific settings            |
| `GET:Settings/GetSettingsMetadata`               | Get metadata about available settings |
| `GET:Settings/ListSettings`                      | List all settings                     |

#### Webhook Payload Structure

Each webhook payload includes comprehensive information about the event that occurred. The payload is delivered as a JSON object with the following structure:

```json
{
  "Action": "POST:Ticket/AddTicket",
  "Data": {
    "RequestBody": {
      "Ticket": {
        "Name": "TICKET-12345",
        "Title": "Need help with AWS permissions",
        "CreateTime": "2025-05-25T15:30:00Z",
        "Assignee": {
          "AgentName": "aws",
          "AgentId": "agent-123456"
        },
        "TenantId": "ea73f43c-dda3-4fb5-998d-54f262238225",
        "Status": "Open"
      }
    },
    "StatusCode": 200
  }
}
```

For message events, the payload structure is similar but includes additional fields:

```json
{
  "Action": "POST:Ticket/SendTicketMessage",
  "Data": {
    "RequestBody": {
      "ticketName": "TICKET-12345",
      "message": {
        "Content": "I'm having trouble accessing the S3 bucket"
      }
    },
    "ResponseBody": {
      "Content": "Let me help you troubleshoot that access issue",
      "data": {
        "Cmds": [
          "aws s3 ls s3://my-bucket"
        ],
        "executedCmds": [
          {
            "command": "aws s3 ls s3://my-bucket",
            "result": "AccessDenied: Access Denied"
          }
        ]
      }
    },
    "StatusCode": 200
  }
}
```

#### Key Data Fields

The webhook payloads contain rich information that can be used for various integration purposes:

**Ticket Creation Event (`POST:Ticket/AddTicket`)**

| Field                                        | Description                              |
| -------------------------------------------- | ---------------------------------------- |
| `Data.RequestBody.Ticket.Name`               | Unique identifier for the ticket         |
| `Data.RequestBody.Ticket.Title`              | Title/subject of the ticket              |
| `Data.RequestBody.Ticket.CreateTime`         | Timestamp when the ticket was created    |
| `Data.RequestBody.Ticket.Assignee.AgentName` | Name of the agent assigned to the ticket |
| `Data.RequestBody.Ticket.TenantId`           | ID of the tenant the ticket belongs to   |
| `Data.RequestBody.Ticket.Status`             | Current status of the ticket             |

**Ticket Message Event (`POST:Ticket/SendTicketMessage`)**

| Field                                 | Description                                    |
| ------------------------------------- | ---------------------------------------------- |
| `Data.RequestBody.ticketName`         | Unique identifier for the ticket               |
| `Data.RequestBody.message.Content`    | Content of the message sent by the user        |
| `Data.ResponseBody.Content`           | Content of the response from the agent         |
| `Data.ResponseBody.data.Cmds`         | Commands executed by the agent (if applicable) |
| `Data.ResponseBody.data.executedCmds` | Results of executed commands (if applicable)   |
