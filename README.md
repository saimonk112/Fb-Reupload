# Fb-Reupload
Below is an example of how to structure your API documentation using Markdown for the app you provided:

```markdown
# Facebook and TikTok Video Upload API

This API allows users to upload videos to Facebook Reels and download TikTok videos using various endpoints. It uses Flask as the web server and integrates with Facebook using undetected ChromeDriver.

## Table of Contents

- [Setup](#setup)
- [Environment Variables](#environment-variables)
- [Endpoints](#endpoints)
  - [Set Cookies](#set-cookies)
  - [TikTok Download](#tiktok-download)
  - [Upload Video](#upload-video)
  - [Upload Video by URL](#upload-video-by-url)
- [Error Handling](#error-handling)
- [Dependencies](#dependencies)

## Setup

### Prerequisites

- Python 3.7+
- Google Chrome
- `chromedriver` executable compatible with your Chrome version

### Installation

1. Clone the repository:
   
   ```bash
   git clone <repository-url>
   cd <repository-directory>
   ```

2. Install the dependencies:
   
   ```bash
   pip install -r requirements.txt
   ```

3. Make sure `chromedriver` is in your system's PATH.

### Running the App

Start the Flask server:

```bash
python app.py
```

## Environment Variables

Create an `.env` file in the root directory and set the following variables:

```env
API_ID=your_api_id
API_HASH=your_api_hash
BOT_TOKEN=your_bot_token
```

## Endpoints

### Set Cookies

**Endpoint:** `/set_cookie`  
**Method:** `POST`  
**Content-Type:** `application/json` or `multipart/form-data`

Sets cookies for Facebook authentication. Cookies are saved on the server for future video uploads.

#### Request Parameters (JSON)

- `unique_id` (optional, `string`): A unique ID to associate with the user's cookies. If not provided, a random ID will be generated.
- `file` (`object`): JSON object containing Facebook cookies.

#### Request Parameters (Multipart Form-Data)

- `file` (`file`): A JSON file containing Facebook cookies.

#### Response

```json
{
  "message": "Hello [Username]! Your cookies are valid.",
  "unique_id": "[unique_id]"
}
```

#### Example

```bash
curl -X POST http://localhost:5000/set_cookie \
  -H "Content-Type: application/json" \
  -d '{
        "unique_id": "user123",
        "file": { ...cookies_data... }
      }'
```

### TikTok Download

**Endpoint:** `/tiktok`  
**Method:** `POST` or `GET`

Downloads a TikTok video and uploads it to Facebook Reels.

#### Request Parameters

**POST**

- `url` (`string`): The TikTok video URL.
- `unique_id` (`string`): A unique ID to use for accessing saved cookies.
- `title` (optional, `string`): The title for the uploaded Facebook video.

**GET**

- `url` (`string`): The TikTok video URL.
- `unique_id` (`string`): A unique ID to use for accessing saved cookies.
- `title` (optional, `string`): The title for the uploaded Facebook video.

#### Response

**Success**

```json
{
  "message": "Video uploaded successfully! Reel ID: [reel_id]"
}
```

**Error**

```json
{
  "error": "Failed to upload video: [error_message]"
}
```

#### Example

```bash
curl -X POST http://localhost:5000/tiktok \
  -F "url=https://www.tiktok.com/example-video-url" \
  -F "unique_id=user123"
```

### Upload Video

**Endpoint:** `/upload`  
**Method:** `POST` or `GET`

Uploads a user-provided video to Facebook Reels.

#### Request Parameters (POST)

- `unique_id` (`string`): A unique ID to use for accessing saved cookies.
- `title` (optional, `string`): The title for the uploaded Facebook video.
- `file` (`file`): An MP4 video file to upload.

#### Response

**Success**

```json
{
  "message": "Video uploaded successfully! Reel ID: [reel_id]"
}
```

**Error**

```json
{
  "error": "Failed to upload video: [error_message]"
}
```

#### Example

```bash
curl -X POST http://localhost:5000/upload \
  -F "unique_id=user123" \
  -F "file=@/path/to/video.mp4"
```

### Upload Video by URL

**Endpoint:** `/upload-by-link`  
**Method:** `POST` or `GET`

Uploads a video to Facebook Reels using a URL.

#### Request Parameters (POST or GET)

- `unique_id` (`string`): A unique ID to use for accessing saved cookies.
- `title` (optional, `string`): The title for the uploaded Facebook video.
- `url` (`string`): The URL of the video to download and upload.

#### Response

**Success**

```json
{
  "message": "Video uploaded successfully! Reel ID: [reel_id]"
}
```

**Error**

```json
{
  "error": "Failed to upload video: [error_message]"
}
```

#### Example

```bash
curl -X POST http://localhost:5000/upload-by-link \
  -F "unique_id=user123" \
  -F "url=https://example.com/video.mp4"
```

## Error Handling

All endpoints return a standard error response when a request fails.

**Error Response Format**

```json
{
  "error": "Error message describing the problem."
}
```

## Dependencies

- Flask: A lightweight web framework for Python.
- undetected-chromedriver: A ChromeDriver wrapper to bypass bot detection.
- Selenium: A tool for web browser automation.
- pyrogram: Telegram bot API framework for Python.
- moviepy: A Python library for video editing.
- requests: A simple HTTP library for Python.
- `chromedriver`: Required for Selenium to control Google Chrome.

Install dependencies with:

```bash
pip install Flask undetected-chromedriver selenium pyrogram moviepy requests
```

## License

MIT License.
```

This documentation provides a structured overview of the API, including setup instructions, environment variables, endpoint specifications, and examples for how to use each endpoint. Feel free to adjust the content as needed!
