# Neural Network Query System

A sophisticated query processing system that combines TensorFlow-based local processing with DeepSeek and OpenAI APIs for comprehensive response generation.

## System Architecture

The system processes queries through four phases:
1. Local TensorFlow neural network processing with MySQL-stored embeddings
2. DeepSeek API fallback
3. OpenAI API fallback
4. Response storage and learning

## Prerequisites

- Ubuntu Server
- Python 3.8+
- Node.js 18+
- MySQL 8.0+
- TensorFlow 2.x

## Installation

### 1. Python Backend Setup

```bash
# Navigate to the neural service directory
cd nn_service

# Install Python dependencies
pip install -r requirements.txt

# Set up MySQL database
mysql -u root -p < init_db.sql

# Configure environment variables
cp config.env.example config.env
# Edit config.env with your credentials and API keys
```

### 2. Next.js Frontend Setup

```bash
# Install Node.js dependencies
npm install

# Build the application
npm run build
```

## Configuration

### MySQL Database
- Create a database user and set permissions
- Update the credentials in `nn_service/config.env`

### API Keys
Configure the following API keys in `nn_service/config.env`:
- DeepSeek API Key
- OpenAI API Key

## Running the System

### 1. Start the Python Backend

```bash
# Navigate to the neural service directory
cd nn_service

# Start the Flask server
python nn_service.py
```

### 2. Start the Next.js Frontend

```bash
# In the project root
npm run dev
```

The application will be available at `http://localhost:8000`

## System Components

### Python Neural Service
- TensorFlow model for local processing
- MySQL database integration
- API integrations (DeepSeek, OpenAI)
- Flask REST API

### Next.js Frontend
- Modern, responsive UI
- Real-time query processing
- Error handling and loading states
- Source attribution for responses

### Database Schema
- `embeddings`: Stores text embeddings for local processing
- `query_history`: Tracks queries and responses
- `model_metrics`: Monitors system performance

## API Endpoints

### `/api/neural-query`
- Method: POST
- Body: `{ "query": "your query string" }`
- Response: `{ "response": "answer", "source": "local|deepseek|openai" }`

## Development

### Adding New Features
1. Update the TensorFlow model in `nn_service/nn_service.py`
2. Modify the database schema in `nn_service/init_db.sql`
3. Update the UI components in `src/app/page.tsx`

### Testing
- Run Python tests: `python -m pytest`
- Run Next.js tests: `npm test`

## Monitoring

The system logs important events and metrics:
- Query processing times
- API response times
- Error rates
- Model performance metrics

## Security Considerations

- API keys are stored securely in environment variables
- Database credentials are protected
- Input validation is implemented
- Rate limiting is applied to API endpoints

## Troubleshooting

### Common Issues

1. Database Connection
```bash
# Check MySQL service
sudo systemctl status mysql

# Verify database exists
mysql -u root -p -e "SHOW DATABASES;"
```

2. Python Service
```bash
# Check logs
tail -f nn_service/nn_service.log
```

3. Next.js Frontend
```bash
# Clear build cache
rm -rf .next
npm run build
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## License

MIT License - See LICENSE file for details
