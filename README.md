# test_genai# Log Analyzer GenAI System

## Overview

This project demonstrates an end-to-end GenAI system for intelligent log analysis and incident management. The system ingests large log files, processes and embeds them into a vector store, and uses an AI agent to retrieve relevant log segments and generate accurate incident summaries.

## Architecture

### System Components

1. **Log Processor** (`src/log_processor.py`)
   - Ingests large log files efficiently
   - Parses log entries with timestamps and severity levels
   - Chunks logs intelligently for optimal embedding

2. **Vector Store** (`src/vector_store.py`)
   - Manages log embeddings using FAISS/ChromaDB
   - Provides semantic search capabilities
   - Handles metadata indexing for filtering

3. **AI Agent** (`src/agent.py`)
   - Retrieves relevant log segments using vector similarity
   - Analyzes patterns and anomalies
   - Generates comprehensive incident summaries

4. **Main Orchestrator** (`main.py`)
   - Coordinates the end-to-end workflow
   - Provides command-line interface
   - Demonstrates system capabilities

### Data Flow

```
Log Files → Log Processor → Vector Store → AI Agent → Incident Summary
    ↓           ↓              ↓           ↓           ↓
Raw Logs → Parsed/Chunked → Embeddings → Retrieval → Analysis
```

## Features

- **Scalable Log Ingestion**: Handles large log files efficiently with streaming processing
- **Intelligent Chunking**: Context-aware log segmentation preserving temporal relationships
- **Semantic Search**: Vector-based retrieval for finding relevant log patterns
- **AI-Powered Analysis**: GPT-based incident detection and summarization
- **Configurable System**: Easy setup with environment-based configuration

## Prerequisites

- Python 3.8+
- OpenAI API key
- At least 4GB RAM for vector processing
- 1GB disk space for vector database

## Installation

1. **Clone and navigate to the project:**
   ```bash
   cd log_analyzer_genai
   ```

2. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Configure environment:**
   ```bash
   cp .env.example .env
   # Edit .env with your OpenAI API key
   ```

## Quick Start

### 1. Basic Usage

```bash
# Run the complete end-to-end demo
python main.py

# Process custom log files
python main.py --log-file /path/to/your/logs.log

# Generate incident summary for specific timeframe
python main.py --start-time "2024-12-16 10:00:00" --end-time "2024-12-16 11:00:00"
```

### 2. Step-by-Step Example

```python
from src.log_processor import LogProcessor
from src.vector_store import VectorStore
from src.agent import LogAnalysisAgent

# Initialize components
processor = LogProcessor()
vector_store = VectorStore()
agent = LogAnalysisAgent()

# Process logs
log_chunks = processor.process_file("sample_data/application.log")

# Store embeddings
vector_store.add_documents(log_chunks)

# Analyze incident
summary = agent.analyze_incident(
    query="Database connection errors",
    time_range=("2024-12-16 10:00:00", "2024-12-16 11:00:00")
)
```

## Configuration

### Environment Variables (.env)

```env
OPENAI_API_KEY=your_openai_api_key_here
VECTOR_DB_PATH=./vector_db
EMBEDDING_MODEL=text-embedding-3-small
LLM_MODEL=gpt-4o-mini
CHUNK_SIZE=500
CHUNK_OVERLAP=50
MAX_RETRIEVAL_RESULTS=10
```

### System Settings (src/config.py)

- **Log Parsing**: Customize timestamp formats and log levels
- **Chunking Strategy**: Adjust chunk size and overlap for your log format
- **Vector Store**: Configure embedding dimensions and similarity thresholds
- **Agent Behavior**: Set retrieval parameters and prompt templates

## Sample Data

The project includes realistic sample log files:

- `sample_data/application.log`: Web application logs with various events
- `sample_data/system.log`: System-level logs with errors and warnings
- `sample_data/database.log`: Database operation logs with performance metrics

## Use Cases

### 1. Incident Response
- Quickly identify root causes of system failures
- Generate comprehensive incident reports
- Track error patterns across time

### 2. Performance Analysis
- Analyze response time degradation
- Identify resource bottlenecks
- Monitor system health trends

### 3. Security Monitoring
- Detect suspicious access patterns
- Identify potential security breaches
- Generate security incident summaries

## Example Output

```
=== INCIDENT SUMMARY ===
Time Period: 2024-12-16 10:30:00 - 10:45:00
Severity: HIGH

Root Cause Analysis:
- Database connection pool exhaustion at 10:32:15
- Cascading failures in user authentication service
- 347 failed login attempts due to backend unavailability

Impact Assessment:
- 1,247 users affected
- 15-minute service degradation
- Critical payment processing interrupted

Recommended Actions:
1. Increase database connection pool size
2. Implement circuit breaker pattern
3. Add connection health monitoring
4. Review auto-scaling policies
```

## Architecture Decisions

### Vector Store Selection
- **FAISS**: Chosen for fast similarity search on large datasets
- **Alternative**: ChromaDB for persistent storage and metadata filtering

### Embedding Strategy
- **Model**: OpenAI text-embedding-3-small for cost-effectiveness
- **Chunking**: Overlap-based approach to maintain context
- **Metadata**: Timestamp, severity, and source system indexing

### AI Agent Design
- **Retrieval**: Hybrid approach combining vector similarity and metadata filtering
- **Analysis**: Multi-step reasoning with context aggregation
- **Output**: Structured summaries with actionable insights

## Performance Considerations

- **Memory Usage**: ~2GB for 1M log entries
- **Processing Speed**: ~1000 log entries/second
- **Query Latency**: <500ms for typical incident analysis
- **Storage**: ~10MB per 100K log entries in vector form

## Troubleshooting

### Common Issues

1. **Out of Memory**: Reduce chunk size or process in batches
2. **Slow Queries**: Check vector index optimization
3. **API Rate Limits**: Implement exponential backoff
4. **Embedding Failures**: Validate log text preprocessing

### Debug Mode

```bash
# Enable detailed logging
python main.py --debug

# Profile performance
python main.py --profile
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Add tests for new functionality
4. Submit a pull request

## License

MIT License - see LICENSE file for details

## Support

For questions and support:
- Create an issue in the repository
- Review the troubleshooting section
- Check sample configurations in the examples folder
