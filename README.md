

# Fb-Reupload API Documentation

Welcome to the **Fb-Reupload API**! This API allows users to interact with TikTok videos, upload them to Facebook Reels, and perform related operations using Flask and an undetected ChromeDriver. Below is a detailed guide for making requests to the API.

## **Base URL**

```
https://oxdevapi.sbs/
```

## **Endpoints**

### 1. **Set Cookies**

#### **Endpoint**
```
POST /set_cookie
```

#### **Description**
Uploads user authentication cookies for validation.

#### **Request**
- **Method**: `POST`
- **Content-Type**: `multipart/form-data`
- **Parameters**:
  - `file`: A `.json` file containing cookies.

#### **Example Request**
```python
import requests

response = requests.post(
    'https://oxdevapi.sbs/set_cookie', 
    files={'file': open('cookies.json', 'rb')}
)
print(response.text)
```

#### **Response**
```json
{
  "message": "Hello [id]! Your cookies are valid.",
  "unique_id": "8da89c00ede85a4571629e4fbb58c2c6"
}
```

### 2. **Download and Upload TikTok Video**

#### **Endpoint**
```
GET /tiktok
```

#### **Description**
Downloads a TikTok video using a provided URL and uploads it to Facebook Reels.

#### **Request**
- **Method**: `GET`
- **Parameters**:
  - `unique_id`: The unique ID obtained after setting cookies.
  - `url`: The URL of the TikTok video.

#### **Example Request**
```python
import requests

unique_id = '8da89c00ede85a4571629e4fbb58c2c6'
response = requests.get(
    'https://oxdevapi.sbs/tiktok', 
    params={'unique_id': unique_id, 'url': 'https://vt.tiktok.com/ZSjRTtVay/'}
)
print(response.text)
```

#### **Response**
```json
{
  "message": "Video uploaded successfully! Reel ID: 1450875635595502"
}
```

### 3. **Upload Video from File**

#### **Endpoint**
```
POST /upload
```

#### **Description**
Uploads a video file to Facebook Reels.

#### **Request**
- **Method**: `POST`
- **Content-Type**: `multipart/form-data`
- **Parameters**:
  - `unique_id`: The unique ID obtained after setting cookies.
  - `title`: The title of the video.
  - `file`: The video file to be uploaded.

#### **Example Request**
```python
import requests

response = requests.post(
    'https://oxdevapi.sbs/upload', 
    data={"unique_id": "8da89c00ede85a4571629e4fbb58c2c6", "title": "test"},
    files={'file': open('downloads/cc2777f237726ac867df19bda825b8cb/7429019439460289793.mp4', 'rb')}
)
print(response.text)
```

#### **Response**
```json
{
  "message": "Video uploaded successfully! Reel ID: 957146053100392"
}
```

### 4. **Upload Video by URL**

#### **Endpoint**
```
GET /upload-by-link
```

#### **Description**
Uploads a video to Facebook Reels using a direct download URL.

#### **Request**
- **Method**: `GET`
- **Parameters**:
  - `unique_id`: The unique ID obtained after setting cookies.
  - `title`: The title of the video.
  - `url`: The direct download URL of the video.

#### **Example Request**
```python
import requests

response = requests.get(
    'https://oxdevapi.sbs/upload-by-link', 
    params={
        "unique_id": "8da89c00ede85a4571629e4fbb58c2c6",
        "title": "test",
        "url": "http://159.65.148.212:8080/dl/671a843fbf141f79b394bbe6"
    }
)
print(response.text)
```

#### **Response**
```json
{
  "message": "Video uploaded successfully! Reel ID: 957146053100392"
}
```

### 5. **Upload Video by URL (POST Method)**

#### **Endpoint**
```
POST /upload-by-link
```

#### **Description**
Similar to the `GET` method, but using a `POST` request to upload a video via a direct download URL.

#### **Request**
- **Method**: `POST`
- **Content-Type**: `application/x-www-form-urlencoded`
- **Parameters**:
  - `unique_id`: The unique ID obtained after setting cookies.
  - `title`: The title of the video.
  - `url`: The direct download URL of the video.

#### **Example Request**
```python
import requests

response = requests.post(
    'https://oxdevapi.sbs/upload-by-link', 
    data={
        "unique_id": "8da89c00ede85a4571629e4fbb58c2c6",
        "title": "test",
        "url": "http://159.65.148.212:8080/dl/671a843fbf141f79b394bbe6"
    }
)
print(response.text)
```

#### **Response**
```json
{
  "message": "Video uploaded successfully! Reel ID: 957146053100392"
}
```

## **Error Handling**

### **Common Errors**
- **400 Bad Request**: Missing or invalid parameters.
- **401 Unauthorized**: Invalid or missing `unique_id`.
- **500 Internal Server Error**: An unexpected error occurred.

## **Usage Tips**
- Ensure your cookies are correctly set before uploading any videos.
- Use the unique ID generated after setting cookies for all authenticated requests.
- Double-check URLs for any typos or errors to avoid failed uploads.

