# 🚀 Clebr API

A backend API server that provides MCP (Model Context Protocol) integration with OpenAI's GPT models for conversational AI applications.

## ✨ Features

- 🔗 **MCP Protocol Integration** - Connect to MCP servers via JSON-RPC 2.0
- 🤖 **OpenAI Integration** - GPT-powered conversational AI with tool calling
- 🌐 **RESTful API** - Clean HTTP endpoints for chat operations
- 📝 **Conversation Management** - Persistent conversation history per session
- 🔒 **CORS Support** - Configurable cross-origin resource sharing
- ⚡ **Session Management** - Multi-session support with unique identifiers

## 🚀 Quick Start

### Prerequisites
- Node.js (v18+)
- OpenAI API key
- MCP Server (optional, runs in fallback mode without it)

### Environment Setup

Create a `.env` file in the root directory:

```bash
OPENAI_API_KEY=your_openai_api_key_here
MCP_SERVER_URL=http://127.0.0.1:3000/mcp  # Optional
```

### Development

Start the development server:

```bash
npm run dev
```

Start the production server:

```bash
npm start
```

The server will be running at `http://localhost:3004`

### Available Scripts

```bash
npm start            # Start production server
npm run dev          # Start development server with nodemon
```

## 🏗️ Architecture

```
Client Application → Clebr API Server → MCP Server (optional)
                           ↓              ↓
                      OpenAI GPT    Tool Execution
                      Conversation  JSON-RPC 2.0
```

### Components

- **Backend Server** (`backend-server.js`) - Main Express.js server
- **MCP Client Manager** (`backend/modules/mcp-client-manager.js`) - Handles MCP connections
- **Conversation Manager** (`backend/modules/conversation-manager.js`) - Manages OpenAI conversations
- **Configuration** (`backend/config/config.js`) - Server configuration

## 🔧 API Endpoints

### Initialize MCP Session
```http
POST /mcp/initialize
Content-Type: application/json

{
  "mcpServerUrl": "http://127.0.0.1:3000/mcp",
  "mcpServerUrls": ["http://server1:3000/mcp", "http://server2:3000/mcp"]
}
```

### Send Chat Message
```http
POST /chat
Content-Type: application/json

{
  "message": "Hello, how can you help me?",
  "sessionId": "your-session-id"
}
```

### Get Session Info
```http
GET /mcp/session/{sessionId}
```

### Get Conversation History
```http
GET /chat/history/{sessionId}
```

### Clear Conversation
```http
DELETE /chat/history/{sessionId}
```

### Health Check
```http
GET /health
```

## 🔧 Configuration

### MCP Server Configuration
Edit `backend/config/config.js` to configure MCP server settings:

```javascript
export default {
  mcp: {
    defaultServerUrl: 'http://127.0.0.1:3000/mcp',
    // ... other MCP settings
  }
};
```

### CORS Settings
CORS is configured to allow requests from specified origins. Update the configuration as needed for your frontend applications.

## 📁 Project Structure

```
clebr-api/
├── backend-server.js                    # Main server entry point
├── backend/
│   ├── config/
│   │   └── config.js                   # Server configuration
│   └── modules/
│       ├── mcp-client-manager.js       # MCP connection management
│       └── conversation-manager.js     # OpenAI conversation handling
├── package.json                        # Dependencies and scripts
├── nodemon.json                        # Development configuration
└── README.md                           # This file
```

## 🔄 Development Workflow

1. **Clone Repository**: `git clone <repository-url>`
2. **Install Dependencies**: `npm install`
3. **Set Environment Variables**: Create `.env` file with OpenAI API key
4. **Start Development**: `npm run dev`
5. **Test API**: Use your favorite HTTP client to test endpoints

## 🚀 Production Deployment

For production deployment:

1. **Environment Variables**: Set `OPENAI_API_KEY` and other required variables
2. **MCP Server**: Configure MCP server URLs in config
3. **CORS**: Update CORS settings for your frontend domains
4. **Process Management**: Use PM2 or similar for process management
5. **Reverse Proxy**: Consider nginx or similar for load balancing

## 🔗 Integration

This backend API can be integrated with any frontend application that needs conversational AI capabilities with MCP tool integration. The API provides a clean interface for:

- Initializing MCP sessions
- Sending chat messages
- Managing conversation history
- Accessing MCP tools and capabilities

---

**Happy coding!** 🎉 