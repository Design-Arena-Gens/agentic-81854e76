# WhatsApp Audio Transcription n8n Workflow - Setup Guide

This n8n workflow automatically transcribes WhatsApp audio messages to text using OpenAI's Whisper API and sends the transcription back to the sender.

## Features

- ✅ Receives WhatsApp webhook notifications
- ✅ Filters for audio messages only
- ✅ Downloads audio files from WhatsApp
- ✅ Transcribes audio using OpenAI Whisper
- ✅ Sends transcription back to the sender
- ✅ Handles errors gracefully

## Setup Instructions

### 1. Import the Workflow

1. Open your n8n instance
2. Click on "Workflows" → "Import from File"
3. Select `whatsapp-audio-transcription-workflow.json`
4. Click "Import"

### 2. Configure Credentials

#### WhatsApp API Token (HTTP Header Auth)

1. Create a new credential of type "HTTP Header Auth"
2. Set the header name: `Authorization`
3. Set the header value: `Bearer YOUR_WHATSAPP_ACCESS_TOKEN`
4. Name it "WhatsApp API Token"

To get your WhatsApp access token:
- Go to [Facebook Developers](https://developers.facebook.com/)
- Navigate to your WhatsApp Business app
- Copy the temporary or permanent access token

#### OpenAI API Credentials

1. Create a new credential of type "OpenAI API"
2. Enter your OpenAI API key
3. Name it "OpenAI API"

To get your OpenAI API key:
- Go to [OpenAI Platform](https://platform.openai.com/)
- Navigate to API Keys
- Create a new secret key

### 3. Set Environment Variable

Set the `WHATSAPP_PHONE_ID` environment variable in n8n:
- This is the Phone Number ID from your WhatsApp Business API setup
- Find it in Meta Business Settings → WhatsApp Business Platform

### 4. Configure WhatsApp Webhook

1. Activate the workflow in n8n
2. Copy the webhook URL from the "WhatsApp Webhook" node
3. In Meta Developer Console:
   - Go to WhatsApp → Configuration
   - Set the Callback URL to your webhook URL
   - Set the Verify Token (if using webhook verification)
   - Subscribe to the `messages` webhook field

### 5. Test the Workflow

1. Send an audio message to your WhatsApp Business number
2. The workflow will:
   - Receive the webhook
   - Download the audio
   - Transcribe it using Whisper
   - Send the transcription back to you

## Workflow Steps

1. **WhatsApp Webhook** - Receives incoming WhatsApp messages
2. **Is Audio Message?** - Checks if the message type is audio
3. **Extract Audio Data** - Extracts audio ID and metadata
4. **Get Audio URL from WhatsApp** - Retrieves the download URL
5. **Download Audio File** - Downloads the audio file
6. **Transcribe with OpenAI Whisper** - Converts speech to text
7. **Format Transcription Result** - Prepares the response
8. **Send Transcription Back** - Sends the text back to WhatsApp
9. **Webhook Response** - Responds to the webhook request

## Requirements

- n8n instance (self-hosted or n8n.cloud)
- WhatsApp Business API access
- OpenAI API account with Whisper access
- Meta Developer account

## Supported Audio Formats

OpenAI Whisper supports:
- MP3, MP4, MPEG, MPGA, M4A, WAV, WEBM
- Maximum file size: 25MB

## Cost Considerations

- OpenAI Whisper API: $0.006 per minute of audio
- WhatsApp Business API: Varies by conversation type and region

## Troubleshooting

### Workflow not triggering
- Verify webhook URL is correctly configured in Meta
- Check that the workflow is active
- Ensure webhook subscriptions include "messages"

### Audio not downloading
- Verify WhatsApp API token is valid
- Check that the token has proper permissions
- Ensure the audio file is accessible

### Transcription failing
- Verify OpenAI API key is valid
- Check that you have Whisper API access
- Ensure the audio file format is supported

### Response not sending
- Verify WHATSAPP_PHONE_ID is correctly set
- Check that the WhatsApp API token has messaging permissions
- Ensure the phone number is registered

## Customization

You can customize the workflow to:
- Store transcriptions in a database
- Add language detection
- Support multiple languages explicitly
- Forward transcriptions to other services (Slack, email, etc.)
- Add conversation context tracking
- Implement rate limiting

## Security Notes

- Store all credentials securely in n8n
- Use environment variables for sensitive data
- Validate webhook signatures (add signature verification)
- Implement rate limiting to prevent abuse
- Use HTTPS for all webhook URLs

## License

This workflow is provided as-is for demonstration purposes.
