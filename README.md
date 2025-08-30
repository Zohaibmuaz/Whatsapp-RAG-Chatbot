# UAF WhatsApp Admissions Assistant

A WhatsApp chatbot built with FastAPI, Twilio, and Google Gemini API that serves as a university admissions assistant for the University of Agriculture, Faisalabad. The chatbot uses Retrieval-Augmented Generation (RAG) to provide accurate information about degree programs based on local data.

## Features

- **WhatsApp Integration**: Receives and responds to messages via Twilio WhatsApp API
- **RAG Implementation**: Retrieves relevant program information and generates contextual responses
- **University Program Database**: Access to comprehensive information about all degree programs
- **Intelligent Search**: Finds relevant programs based on user queries
- **AI-Powered Responses**: Uses Google Gemini API for natural language generation

## Project Structure

```
├── main.py              # FastAPI application with chatbot logic
├── requirements.txt     # Python dependencies
├── data.json           # University program database
├── .env                # Environment variables (create this file)
└── README.md           # This file
```

## Setup Instructions

### 1. Install Dependencies

```bash
pip install -r requirements.txt
```

### 2. Environment Variables

Create a `.env` file in the project root with the following variables:

```env
# Twilio Configuration
TWILIO_ACCOUNT_SID=ACxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
TWILIO_AUTH_TOKEN=your_auth_token_here
TWILIO_WHATSAPP_NUMBER=whatsapp:+14155238886

# Google Gemini API Configuration
GOOGLE_API_KEY=your_gemini_api_key_here
```

### 3. Get API Keys

#### Twilio Setup
1. Sign up at [Twilio](https://www.twilio.com/)
2. Get your Account SID and Auth Token from the Twilio Console
3. Set up WhatsApp Sandbox or Business API
4. Note your WhatsApp number

#### Google Gemini API
1. Go to [Google AI Studio](https://makersuite.google.com/app/apikey)
2. Create an API key for Gemini
3. Copy the API key to your `.env` file

### 4. Run the Application

```bash
python main.py
```

Or using uvicorn directly:

```bash
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```

The application will be available at `http://localhost:8000`

## API Endpoints

- `GET /` - Health check and status
- `GET /health` - Detailed health information
- `POST /whatsapp` - Twilio WhatsApp webhook endpoint

## How It Works

### RAG Implementation

1. **Retrieval**: When a user sends a message, the system searches through the `data.json` file to find relevant programs
2. **Augmentation**: Relevant program information is formatted into a structured context
3. **Generation**: The context and user question are sent to Gemini API to generate a helpful response

### Message Flow

1. User sends WhatsApp message
2. Twilio webhook sends message to `/whatsapp` endpoint
3. System searches for relevant programs
4. Context is formatted and sent to Gemini API
5. Generated response is sent back via Twilio
6. User receives helpful information about university programs

## Testing

### Local Testing
You can test the endpoints locally:

```bash
# Health check
curl http://localhost:8000/health

# Root endpoint
curl http://localhost:8000/
```

### WhatsApp Testing
1. Configure your Twilio webhook URL to point to your server's `/whatsapp` endpoint
2. Send a message to your Twilio WhatsApp number
3. The chatbot will respond with relevant program information

## Example Queries

- "Tell me about BS Computer Science"
- "What are the requirements for BBA?"
- "I'm interested in agriculture programs"
- "What programs are available in the Faculty of Sciences?"

## Error Handling

The system includes comprehensive error handling:
- Graceful fallbacks when API calls fail
- Logging for debugging
- User-friendly error messages
- TwiML fallback responses

## Logging

The application logs all incoming messages, search results, and API responses for debugging purposes. Check the console output for detailed information.

## Security Notes

- Keep your `.env` file secure and never commit it to version control
- Use HTTPS in production
- Validate incoming webhook requests from Twilio
- Monitor API usage and costs

## Troubleshooting

### Common Issues

1. **Environment Variables Not Loaded**: Ensure `.env` file exists and contains all required variables
2. **Twilio Authentication Failed**: Verify Account SID and Auth Token
3. **Gemini API Errors**: Check API key and quota limits
4. **Data Not Loading**: Ensure `data.json` file is in the correct location

### Debug Mode

Enable debug logging by modifying the logging level in `main.py`:

```python
logging.basicConfig(level=logging.DEBUG)
```

## Support

For issues or questions:
1. Check the logs for error messages
2. Verify all environment variables are set correctly
3. Test individual API endpoints
4. Ensure all dependencies are installed correctly

## License

This project is for educational and demonstration purposes.
