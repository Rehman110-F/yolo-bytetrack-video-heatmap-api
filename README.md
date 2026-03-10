# YOLO ByteTrack Video Heatmap API

A **FastAPI-based AI video processing API** that detects people in a video using **YOLOv11 + ByteTrack tracking** and generates a **dynamic movement heatmap overlay** on the video.

This project is designed to run easily in **Google Colab** and be exposed publicly using **ngrok** for testing.

## Use Cases

- Crowd analysis
- Store analytics
- Smart surveillance
- Movement pattern analysis

---

# Features

- Person detection using **YOLO**
- Multi-object tracking using **ByteTrack**
- Dynamic **movement heatmap generation**
- Video processing API with **FastAPI**
- Background video processing
- Download processed video
- Public API access using **ngrok**
- Interactive API testing using **Swagger UI**

---

# Technology Stack

- Python
- FastAPI
- YOLO (Ultralytics)
- ByteTrack
- OpenCV
- PyTorch
- Google Colab
- ngrok

---

# Running the Project in Google Colab

This project is designed to run easily in **Google Colab**.

---

# Step 1 — Open the Notebook

Upload the provided notebook to **Google Colab**.

Or create a new notebook and paste the project code.

---

# Step 2 — Install Dependencies

Run the setup cells that install all required libraries.

```bash
pip install ultralytics
pip install fastapi uvicorn pyngrok
```

Install ByteTrack dependencies as well.

---

# Step 3 — Start the FastAPI Server

Start the API server using **uvicorn**.

```bash
uvicorn app:app --host 0.0.0.0 --port 8000
```

This will start the API server inside Colab.

---

# Step 4 — Create an ngrok Account

To expose the API publicly you need **ngrok**.

Create a free account:

https://ngrok.com

After signup:

1. Copy your **Auth Token**
2. Go to **Google Colab Secrets**
3. Store the token using the name:

```python
NGROK_TOKEN
```

---

# Step 5 — Connect ngrok

Run the following code inside Colab:

```python
from pyngrok import ngrok
from google.colab import userdata

token = userdata.get('NGROK_TOKEN')
ngrok.set_auth_token(token)

public_url = ngrok.connect(8000)

print("Public URL:", public_url)
```

This will generate a public URL like:

```
https://abcd-1234.ngrok-free.app
```

---

# Step 6 — Open Swagger UI

FastAPI automatically generates API documentation.

Open the following URL in your browser:

```
https://your-ngrok-url/docs
```

Example:

```
https://abcd-1234.ngrok-free.app/docs
```

This will open the **Swagger UI interface** where you can test the API.

---

# Step 7 — Upload a Video for Processing

Inside **Swagger UI**:

Find the endpoint:

```
POST /processvideo
```

Click **Try it out**

Upload your video file and press **Execute**.

The API will return a response like:

```json
{
 "output_file": "outputs/processed_video.mp4",
 "status": "Processing started in background"
}
```

The video will now start processing.

---

# Step 8 — Download the Processed Video

Once processing finishes you can download the output video.

Use the endpoint:

```
GET /download/{filename}
```

Example:

```
/download/processed_video.mp4
```

Important note:

Swagger sometimes **cannot properly download video responses**.

Therefore it is recommended to open the download endpoint **directly in the browser**.

Example:

```
https://your-ngrok-url/download/processed_video.mp4
```

This will automatically download the processed video.

---

# How the Heatmap Works

Pipeline:

```
Video
   ↓
YOLO Person Detection
   ↓
ByteTrack Multi-object Tracking
   ↓
Track Foot Position
   ↓
Accumulate Heatmap
   ↓
Gaussian Blur
   ↓
Color Map Overlay
   ↓
Output Video
```

The heatmap highlights areas where people spend the most time.

---

# API Endpoints

## Upload Video

```
POST /processvideo
```

Upload a video file and start processing.

---

## Download Processed Video

```
GET /download/{filename}
```

Download the processed video once ready.

---

# Example Use Cases

- Retail store analytics
- Mall foot traffic analysis
- Smart city monitoring
- Event crowd analysis
- Security surveillance

---

# Future Improvements

- Real-time webcam heatmap
- Live streaming support
- Multi-class heatmaps
- Web dashboard
- GPU optimization

---

# Author

**Muhammad Rehman Ashraf**

Computer Vision Developer specializing in:

- AI Video Analytics
- 3D Computer Vision
- Object Tracking
- AR/VR Systems

---

# License

PIEAS License

---

# If you like this project

Give it a ⭐ on GitHub.
