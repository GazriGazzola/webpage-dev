# Safe Coastal Dog Walks (Serverless AWS Dashboard)

A fully serverless, event-driven cloud dashboard built to monitor coastal weather, marine tides, and live harbor conditions in Cork, Ireland. Because getting a husky and a wolf-dog stuck in pitch-black mudflats—or swept away by a rogue swell—is a terrible way to spend an evening.

This project was built as a hands-on transition into cloud engineering, strictly adhering to serverless best practices. It runs on a compute footprint of absolute zero when idle, keeping AWS billing at exactly €0.00 a month. Jeff Bezos will have to fund his next rocket ship without me.

## Cloud Architecture

This application utilizes a Backend-for-Frontend (BFF) pattern to aggregate multiple external APIs into a single lightweight JSON payload, eliminating frontend CORS issues and minimizing client-side processing.

*   **Frontend Storage:** AWS S3 (Static Website Hosting)
*   **Edge Network & Security:** AWS CloudFront (CDN routing and HTTPS termination)
*   **Compute:** AWS Lambda (Python 3.x backend)
*   **External APIs:** Open-Meteo (Weather & Marine Sea Level data)
*   **Source Control:** Git & GitHub

## Key Features

*   **Dynamic Tide Mathematics:** Scrapes 24-hour mean sea level (MSL) projections, mathematically filters the absolute highest and lowest tide marks, and outputs exact time windows for hard-sand beach walking.
*   **Breed-Specific Environmental Warnings:** Custom logic block that warns of hot sand temperatures (>18°C) specifically tailored for thick-coated double-breed dogs, alongside gales and rain alerts.
*   **Live Direct-Feed Webcams:** Utilizes custom HTML/CSS iframe guillotine techniques to bypass clunky third-party mobile web players, stripping raw video streams of Cobh and Cork Harbour directly to the dashboard.
*   **Daylight Boundary Tracking:** Automatically parses daily sunrise and sunset bounds to ensure the pack gets off the beach before visibility drops to zero.

## Deployment Instructions

### 1. The Backend (AWS Lambda)
1. Create a new Lambda function in your AWS Console using the Python 3.x runtime.
2. Enable a **Function URL** with `NONE` for Auth type and configure CORS to allow your frontend domain (or `*` for local testing).
3. Paste the provided `lambda_function.py` code into the editor and deploy. 
4. Copy the generated Function URL.

### 2. The Frontend (S3 & CloudFront)
1. Update `WEATHER_API_ENDPOINT` in `index.html` with your new Lambda Function URL.
2. Upload `index.html` to an AWS S3 bucket configured for static hosting.
3. Put an AWS CloudFront distribution in front of the bucket. Force HTTPS and point the origin to the S3 bucket using Origin Access Control (OAC).
4. Update the S3 bucket policy to only accept traffic from the CloudFront distribution.

## Future Roadmap

Because a cloud engineer's work is never truly finished until they break production:
- [ ] **Marine Swell Alerts:** Integrate Open-Meteo wave height parameters to detect rogue sneaker waves.
- [ ] **Data Visualization:** Replace the static tide table with a Chart.js 24-hour waveform graph.
- [ ] **Twitch/YouTube Webhook:** Add a live-status ping to display an "IRL Stream Live" badge when broadcasting the walk.

---
*Built for the pack. Hosted in the cloud.*
