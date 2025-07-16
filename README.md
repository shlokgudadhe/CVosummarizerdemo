# README for Conversation Summarization Chatbot

A Streamlit-based conversational AI chatbot featuring intelligent conversation summarization, session management, and efficient memory handling for maintaining context across extended conversations.

## Features

### Conversation Summarization
- **Intelligent summarization** using Gemini API to maintain context
- **Chunk-based processing** (24 messages per chunk) for efficient memory management
- **Context-aware responses** using previous conversation summaries
- **Session-based conversations** with automatic timeout (90 minutes)

### Memory Management
- **Persistent storage** of conversation summaries using pickle files
- **Session timeout handling** prevents memory bloat
- **Chunk-based processing** maintains context without storing full conversation history
- **Automatic cleanup** of expired sessions

### Technical Features
- Real-time streaming responses
- Debug mode for API prompt inspection
- Conversation history download/upload functionality
- Automatic session creation and management

## Setup & Installation

### Prerequisites
- Python 3.8+
- Streamlit
- Google Gemini API key

### Required Dependencies
```bash
pip install streamlit requests python-dotenv litellm pickle-mixin
```

### Environment Variables
Create a `.streamlit/secrets.toml` file or set environment variables:
```toml
GEMINI_API_KEY = "your-gemini-api-key"
```

## Usage

### Running the Application
```bash
streamlit run app.py
```

### Basic Interaction
1. Open the Streamlit app in your browser
2. Start chatting using the input box
3. The system automatically manages conversation context through summarization
4. Sessions maintain context across multiple interactions

### Session Management
- **New Session**: Click "Start New Session" in the sidebar
- **Session Info**: View current session statistics in the sidebar
- **History**: Download/upload conversation history files

## Configuration

### Customizable Parameters
- **Session timeout**: 90 minutes (adjustable in `ConversationSummarizer`)
- **Chunk size**: 24 messages per chunk
- **Response length**: Max 200 tokens
- **Temperature**: 0.7 for natural responses

### Memory Management Settings
Modify the `ConversationSummarizer` class to adjust:
- Chunk processing size
- Session timeout duration
- Summarization frequency
- Context retention depth

## File Structure

```
├── app.py                    # Main application
├── conversation_summaries.pkl # Persistent conversation storage
├── .streamlit/
│   └── secrets.toml          # API keys configuration
└── README.md                 # This file
```

## Key Components

### ConversationSummarizer Class
- **Chunking System**: Processes conversations in 24-message chunks
- **Summarization Engine**: Creates concise summaries of conversation chunks
- **Session Management**: Handles timeouts and persistence
- **Context Provision**: Provides relevant context for API calls

### Memory Management Architecture
- **Chunk Processing**: Breaks conversations into manageable pieces
- **Summary Storage**: Maintains compressed conversation context
- **Session Timeout**: Automatically cleans up expired conversations
- **Context Retrieval**: Efficiently provides relevant history for responses

### API Integration
- **Gemini API**: Powers the chatbot responses and summarization
- **LiteLLM**: Handles API calls with streaming support

## Debugging & Development

### Debug Mode
Enable "Show API Prompt" in the sidebar to:
- View exact prompts sent to Gemini API
- Inspect conversation context and summaries
- Debug summarization process
- Monitor memory usage and chunk processing

### Data Management
- Download conversation history as pickle files
- Upload previous conversation data
- Monitor session statistics and message counts
- Track summarization efficiency

## Memory Management Details

### Conversation Chunking
- Processes conversations in 24-message chunks
- Maintains context through intelligent summarization
- Prevents memory overflow in long conversations
- Enables efficient context retrieval

### Session Lifecycle
1. **Creation**: New session starts with empty context
2. **Accumulation**: Messages collect until chunk size reached
3. **Summarization**: Chunk gets summarized and stored
4. **Context Provision**: Summaries provide context for new responses
5. **Timeout**: Sessions expire after 90 minutes of inactivity

### Performance Optimization
- **Lazy Loading**: Summaries loaded only when needed
- **Efficient Storage**: Pickle files for fast serialization
- **Memory Cleanup**: Automatic removal of expired sessions
- **Context Compression**: Summaries reduce memory footprint

## Troubleshooting

### Common Issues
1. **API Key Errors**: Ensure Gemini API key is properly configured
2. **Session Timeouts**: Adjust timeout settings in `ConversationSummarizer`
3. **Memory Issues**: Reduce chunk size for lower memory usage
4. **Summarization Quality**: Modify summarization prompts for better context retention

### Performance Tips
- Regular session cleanup prevents memory bloat
- Conversation summarization maintains context without storing full history
- Streaming responses provide better user experience
- Monitor session statistics to optimize chunk size
