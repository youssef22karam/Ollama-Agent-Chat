# Ollama Agent Chat

A Flask-based web application that creates personalized AI agents using Ollama models. Each agent has unique personalities, expertise areas, and communication styles, with persistent conversation history and intelligent context summarization.

## Features

- 🤖 **Custom AI Agents**: Create agents with unique personalities, roles, and expertise
- 💬 **Persistent Conversations**: Chat history is saved and maintained across sessions
- 🧠 **Smart Context Management**: Automatic conversation summarization for long-term memory
- 🎛️ **Configurable Parameters**: Adjust temperature, max tokens, and top-p for each agent
- 🌐 **Web Interface**: Clean, responsive chat interface with dark theme
- 📊 **Agent Management**: Create, edit, and delete agents through the web UI
- 🔄 **Multiple Models**: Support for any Ollama-compatible model

## Screenshots

The application provides:
- **Chat Interface**: Real-time conversations with selected agents
- **Agent Creation**: Form-based agent configuration with personality settings
- **Agent Management**: Overview and control panel for all created agents

## Prerequisites

- Python 3.7+
- [Ollama](https://ollama.ai/) installed and running locally
- At least one Ollama model downloaded (e.g., `llama3.2`, `mistral`, etc.)

## Installation

1. **Clone the repository**:
   ```bash
   git clone <repository-url>
   cd ollama-agent-chat
   ```

2. **Install dependencies**:
   ```bash
   pip install flask flask-cors requests
   ```

3. **Ensure Ollama is running**:
   ```bash
   ollama serve
   ```

4. **Download an Ollama model** (if you haven't already):
   ```bash
   ollama pull llama3.2
   # or any other model you prefer
   ```

## Usage

1. **Start the application**:
   ```bash
   python app.py
   ```

2. **Open your browser** and navigate to:
   ```
   http://localhost:5000
   ```

3. **Create your first agent**:
   - Click the "Create Agent" tab
   - Fill in the agent details (name, role, personality, expertise)
   - Configure model parameters (temperature, max tokens, etc.)
   - Click "Create Agent"

4. **Start chatting**:
   - Go to the "Chat" tab
   - Select an agent from the dropdown
   - Start your conversation!

## Configuration

### Default Settings

The application comes with these default configurations:

```python
OLLAMA_HOST = 'http://localhost:11434'  # Ollama server URL
DEFAULT_MODEL = "huihui_ai/llama3.2-abliterate"  # Default model
DEFAULT_TEMP = 0.7  # Creativity vs precision
DEFAULT_MAX_TOKENS = 500  # Response length
DEFAULT_TOP_P = 0.9  # Response diversity
```

### Agent Parameters

When creating agents, you can configure:

- **Temperature** (0.0-1.0): Controls creativity vs consistency
- **Max Tokens** (100-2000): Maximum response length
- **Top-p** (0.0-1.0): Controls response diversity
- **Model**: Any available Ollama model

## File Structure

```
ollama-agent-chat/
├── app.py                 # Main Flask application
├── agents.json           # Agent configurations (auto-generated)
├── agent_history/        # Directory for conversation histories
│   ├── agent_name_history.json
│   └── agent_name_summary.txt
└── README.md
```

## API Endpoints

The application provides a REST API:

- `GET /api/agents` - List all agents
- `POST /api/agents` - Create new agent
- `DELETE /api/agents/<name>` - Delete agent
- `GET /api/models` - List available Ollama models
- `POST /api/chat` - Send message to agent
- `GET /api/history/<name>` - Get agent conversation history
- `DELETE /api/history/<name>` - Reset agent conversation history

## How It Works

### Agent System
Each agent is defined by:
- **Personality traits** and **communication style**
- **Area of expertise** and **role**
- **Model parameters** (temperature, tokens, etc.)
- **Persistent conversation history**
- **Context summarization** for long-term memory

### Memory Management
- Conversations are automatically summarized every few messages
- Summaries capture key facts, relationships, and context
- Long conversations maintain coherence through intelligent context management
- Both detailed history and summaries are persisted to disk

### Model Integration
- Uses Ollama's chat API for generating responses
- Supports any Ollama-compatible model
- Configurable generation parameters per agent
- Automatic model availability detection

## Customization

### Adding Default Agents

The application creates two default agents on first run. You can modify the default agents in the `if __name__ == '__main__':` section:

```python
AgentManager.save_all([
    Agent.from_dict({
        'name': "Your Agent Name", 
        'role': "Agent Role", 
        'temperament': "Personality traits", 
        'expertise': "Areas of knowledge", 
        'communication_style': "How they communicate"
    })
])
```

### Changing Default Configuration

Modify the `Config` class to change default settings:

```python
class Config:
    OLLAMA_HOST = 'http://your-ollama-host:11434'
    DEFAULT_MODEL = "your-preferred-model"
    DEFAULT_TEMP = 0.8  # More creative
    # ... other settings
```

## Troubleshooting

### Common Issues

1. **"Connection refused" error**:
   - Ensure Ollama is running: `ollama serve`
   - Check if Ollama is accessible at `http://localhost:11434`

2. **"Model not found" error**:
   - Download the model: `ollama pull <model-name>`
   - Check available models: `ollama list`

3. **Empty responses**:
   - Check Ollama logs for errors
   - Try a different model
   - Reduce max_tokens if the model is struggling

4. **Port already in use**:
   - Change the port in the last line: `app.run(host='0.0.0.0', port=5001)`

### Performance Tips

- Use smaller models for faster responses
- Adjust `max_tokens` based on your needs
- Lower `temperature` for more focused responses
- Higher `temperature` for more creative responses

## Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature-name`
3. Make your changes and test them
4. Commit your changes: `git commit -am 'Add feature'`
5. Push to the branch: `git push origin feature-name`
6. Submit a pull request

## License

This project is open source and available under the [MIT License](LICENSE).

## Support

If you encounter any issues or have questions:

1. Check the troubleshooting section above
2. Review Ollama documentation: https://ollama.ai/
3. Open an issue on GitHub with details about your problem

## Roadmap

- [ ] Multi-user support with authentication
- [ ] Export/import agent configurations
- [ ] Advanced conversation analytics
- [ ] Voice input/output integration
- [ ] Custom model fine-tuning support
- [ ] Group conversations with multiple agents

---

**Note**: This application is designed for local use and development. For production deployment, consider adding proper authentication, error handling, and security measures.
