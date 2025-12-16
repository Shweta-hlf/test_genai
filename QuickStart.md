# Quick Start Guide

## Log Analyzer GenAI - Complete Setup and Usage

This guide will get you up and running with the Log Analyzer GenAI system in under 10 minutes.

### Prerequisites

- Python 3.8 or higher
- OpenAI API key
- At least 4GB RAM
- 1GB disk space

### Step 1: Setup

1. **Navigate to project directory:**
   ```bash
   cd log_analyzer_genai
   ```

2. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Configure environment:**
   ```bash
   # Copy environment template
   copy .env.example .env
   
   # Edit .env file with your OpenAI API key
   # OPENAI_API_KEY=your_actual_api_key_here
   ```

### Step 2: Run the Demo

**Complete End-to-End Demo:**
```bash
python main.py --demo
```

This will:
- Create sample log files
- Ingest and process them
- Perform sample analyses
- Generate health reports
- Show incident summaries

### Step 3: Basic Usage Examples

**Process your own log files:**
```bash
# Ingest a log file
python main.py --ingest C:\path\to\your\logfile.log

# Analyze an incident
python main.py --analyze "database connection errors"

# Search for specific patterns
python main.py --search "authentication failed" --limit 10

# Generate health report
python main.py --health-report --hours 24

# Check system status
python main.py --status
```

**Time-based analysis:**
```bash
# Analyze specific time range
python main.py --analyze "memory errors" --start-time "2024-12-16T10:00:00" --end-time "2024-12-16T11:00:00"

# Recent anomaly detection
python main.py --detect-anomalies --hours 6
```

### Step 4: Understanding the Output

The system provides several types of analysis:

1. **Incident Analysis** - Comprehensive incident reports with root cause analysis
2. **Health Reports** - System health scoring with recommendations
3. **Anomaly Detection** - Automatic detection of unusual patterns
4. **Semantic Search** - Find relevant log entries using natural language

### Sample Output

```
INCIDENT ANALYSIS
=================
Time Period: 2024-12-16 10:30:00 - 10:45:00
Severity: HIGH

Root Cause Analysis:
- Database connection pool exhaustion at 10:32:15
- Cascading failures in authentication service
- Memory pressure leading to application restart

Impact Assessment:
- 1,247 users affected
- 15-minute service degradation
- Critical payment processing interrupted

Recommended Actions:
1. Increase database connection pool size
2. Implement circuit breaker pattern
3. Add connection health monitoring
```

### Advanced Configuration

Edit `.env` file to customize:
- `CHUNK_SIZE=500` - Size of log chunks for analysis
- `MAX_RETRIEVAL_RESULTS=15` - Number of results to analyze
- `LLM_MODEL=gpt-4o-mini` - OpenAI model for analysis

### Troubleshooting

**Common Issues:**

1. **"OpenAI API key not found"**
   - Ensure `.env` file has `OPENAI_API_KEY=your_key`

2. **"No relevant log data found"**
   - Check log files are properly formatted
   - Try broader search terms

3. **"Out of memory"**
   - Reduce `CHUNK_SIZE` in `.env`
   - Process smaller log files

**Getting Help:**
- Check the comprehensive README.md
- Review sample log formats in `sample_data/`
- Run with `--verbose` for detailed logging

### File Structure

```
log_analyzer_genai/
├── main.py                 # Main entry point
├── src/                    # Core modules
│   ├── config.py          # Configuration management
│   ├── log_processor.py   # Log ingestion and parsing
│   ├── vector_store.py    # Vector storage and retrieval
│   └── agent.py           # AI analysis engine
├── sample_data/           # Sample log files
├── vector_db/             # Vector database (created automatically)
└── requirements.txt       # Dependencies
```

### Next Steps

1. **Try with your own logs** - Use `--ingest` with real log files
2. **Customize analysis** - Modify prompts in `agent.py`
3. **Scale up** - Process larger datasets with batch operations
4. **Integrate** - Use as a library in your own applications

### Support

For issues or questions:
1. Check the troubleshooting section in README.md
2. Review configuration options in `src/config.py`
3. Run with `--verbose` for detailed debugging information

---

**Congratulations! Your log analysis system is ready to use.**
