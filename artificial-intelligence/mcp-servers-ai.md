# MCP Servers Overview

## What is Model Context Protocol (MCP)?
**MCP (Model Context Protocol)** is an open-source standard for connecting AI applications to external systems.
- MCP was developed by AI company **Anthropic** and later open-sourced. Since becoming open source in late 2024, MCP has rapidly become an industry standard, enabling more widespread use of AI agents.
- MCP is a standard way to make information available to large language models (LLMs).  
- Somewhat similar to the way an application programming interface (API) works, MCP offers a documented, standardized way for a computer program to integrate services from an external source.
- It supports agentic AI: intelligent programs that can autonomously pursue goals and take action.
- Essentially, MCP allows AI models like Claude, ChatGPT, or Gemini to connect with external resources such as data sources (e.g., local files, databases), tools (e.g., search engines, calculators), and specialized workflows. This connection enables them to go beyond their regular training data, incorporating live information and external capabilities to generate more dynamic and powerful content.


## MCP Architecture
### How does MCP work? Participants
MCP follows a client-server architecture where an **MCP host** - an AI application like Claude Code or Claude Desktop, establishes connections to one or more MCP servers. The MCP host accomplishes this by creating one MCP client for each MCP server. Each MCP client maintains a dedicated one-to-one connection with its corresponding MCP server.
The key participants in the MCP architecture are:
- **MCP Host:** The AI application that coordinates and manages one or multiple MCP clients
- **MCP Client:** A component that maintains a connection to an MCP server and obtains context from an MCP server for the MCP host to use
- **MCP Server:** A program that provides context to MCP clients

For example, **Cursor IDE** acts as an MCP host. When Cursor establishes a connection to an MCP server, such as the **Chrome DevTools MCP server**, the Cursor runtime instantiates an MCP client object that maintains the connection to that server. When Cursor subsequently connects to another MCP server, such as an **Angular MCP server**, the Cursor runtime instantiates an additional MCP client object to maintain this new connection. This maintains a one-to-one relationship of MCP clients to MCP servers within the host application.

### Layers
MCP consists of two layers:  
- **Data layer:** Defines the JSON-RPC based protocol for client-server communication, including lifecycle management, and core primitives, such as tools, resources, prompts and notifications.  
- **Transport layer:** Defines the communication mechanisms and channels that enable data exchange between clients and servers, including transport-specific connection establishment, message framing, and authorization.  

Conceptually the data layer is the inner layer, while the transport layer is the outer layer.

#### Data layer
The **data layer** implements a **JSON-RPC 2.0** based exchange protocol that defines the message structure and semantics. This layer includes:

- **Lifecycle management**: Handles connection initialization, capability negotiation, and connection termination between clients and servers.
- **Server features**: Enables servers to provide core functionality including tools for AI actions, resources for context data, and prompts for interaction templates from and to the client.
- **Client features**: Enables servers to ask the client to get a response from the main AI, request input from the user, and show messages to the client.
- **Utility features**: Supports additional capabilities like notifications for real-time updates and progress tracking for long-running operations.

#### Transport layer
The **transport layer** manages communication channels and authentication between clients and servers. It handles connection establishment, message framing, and secure communication between MCP participants.

MCP supports two transport mechanisms:   
- **Stdio transport**: Uses standard input/output streams for direct communication between local processes on the same machine. This provides optimal performance with no network overhead.
- **Streamable HTTP transport**: Uses HTTP `POST` for client-to-server messages with optional Server-Sent Events for streaming capabilities. This transport enables remote server communication and supports standard HTTP authentication methods, including bearer tokens, API keys, and custom headers. MCP recommends using OAuth to obtain authentication tokens.

The transport layer abstracts communication details from the protocol layer, enabling the same JSON-RPC 2.0 message format to be used across all transport mechanisms.


## MCP Servers
**MCP servers** are programs that expose specific capabilities to AI applications through standardized MCP protocol interfaces.   

Common examples include:
- **File system servers** for document access
- **Database servers** for data queries
- **GitHub servers** for code management
- **Slack servers** for team communication
- **Calendar servers** for scheduling
- **Chrome DevTools server** for controlling, inspecting, and automating a live browser session directly from your IDE


### Core Server Features
MCP Servers provide functionality through three building blocks:

| Feature       | Explanation                                                                                                                                                                             | Examples                                                       | Who controls it |
|:--------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------|:----------------|
| **Tools**     | Functions that your LLM can actively call, and decides when to use them based on user requests. Tools can write to databases, call external APIs, modify files, or trigger other logic. | Search flights<br>Send messages<br>Create calendar events      | Model           |
| **Resources** | Passive data sources that provide read-only access to information for context, such as file contents, database schemas, or API documentation.                                           | Retrieve documents<br>Access knowledge bases<br>Read calendars | Application     |
| **Prompts**   | Pre-built instruction templates that tell the model to work with specific tools and resources.                                                                                          | Plan a vacation<br>Summarize my meetings<br>Draft an email     | User            |


## MCP Clients
**MCP clients** are instantiated by **host applications** to communicate with particular **MCP servers**. The host application, like Claude.ai or an IDE, manages the overall user experience and coordinates multiple clients. Each client handles one direct communication with one server.

Understanding the distinction is important: the **host** is the application users interact with, while **clients** are the protocol-level components that enable server connections.

### Core Client Features
In addition to making use of context provided by servers, clients may provide several features to servers. These client features allow server authors to build richer interactions.

| Feature | Explanation | Example |
| :--- | :--- | :--- |
| **Sampling** | Sampling allows servers to request LLM completions through the client, enabling an agentic workflow. This approach puts the client in complete control of user permissions and security measures. | A server for booking travel may send a list of flights to an LLM and request that the LLM pick the best flight for the user. |
| **Roots** | Roots allow clients to specify which directories servers should focus on, communicating intended scope through a coordination mechanism. | A server for booking travel may be given access to a specific directory, from which it can read a user’s calendar. |
| **Elicitation**| Elicitation enables servers to request specific information from users during interactions, providing a structured way for servers to gather information on demand. | A server booking travel may ask for the user’s preferences on airplane seats, room type or their contact number to finalise a booking. |

## Is MCP Secure?

- MCP **does not have authentication, authorization, or encryption natively built in**, so developers have to implement that themselves or use a service that assists with implementation.
- MCP **does not require the use of HTTPS** - instead running over HTTP in many implementations. It can therefore lack encryption and authentication unless developers proactively implement Transport Layer Security (TLS). Like any networking protocol, MCP can be vulnerable to impersonation or on-path attacks if TLS is not used.
- Because MCP **offers similar functionality to an API** (external parties requesting data and services), many of the major API security considerations also apply to MCP implementations.
- Organizations making MCP servers available **must ensure that relevant security measures are in place**:
    - Confidential data is not exposed.
    - Resources are protected.
    - Excessive requests are stopped by rate limiting.
    - AI agents do not have excessive permissions.
    - Inputs are validated and sanitized.

## Useful MCP Servers for Engineering
- [Chrome Devtools MCP Server](chrome-devtools-mcp-server-ai.md)
- [Angular MCP Servers](angular-mcp-servers-ai.md)
- [React MCP Servers](react-mcp-servers-ai.md)


## AI Vocabulary
- **LLM or Large Language Model:** It is a type of artificial intelligence trained on massive datasets to understand, generate, and manipulate human language. 
- **AI agents:** AI programs built on top of LLMs. They use LLM information-processing capabilities to obtain data, make decisions, and take actions on behalf of human users.  
  MCP is one way for AI agents to find the information they need and to take actions. It helps connect AI agents to the "outside world," so to speak - the world beyond the LLM's training data.


## Documentation and Recourses
Below are official resources and sources to find trusted MCP servers:
- [MCP Servers: Official Registry](https://github.com/mcp)
- [Model Context Protocol servers](https://github.com/modelcontextprotocol/servers)   
  This repository is a collection of reference implementations for the Model Context Protocol (MCP), as well as references to community-built servers and additional resources.
- [Find Awesome MCP Servers and Clients](https://mcp.so/)
- [Awesome MCP Servers](https://mcpservers.org/)
- [MCP Server Directory](https://www.pulsemcp.com/servers)
- [Official Documentation on Model Context Protocol (MCP)](https://modelcontextprotocol.io/docs/getting-started/intro)
- [What is the Model Context Protocol (MCP)? by Cloudflare](https://www.cloudflare.com/learning/ai/what-is-model-context-protocol-mcp/)