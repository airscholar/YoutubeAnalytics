# Real-Time YouTube Analytics Streamed to Telegram

This Python-based project aims to fetch real-time YouTube metrics like likes, views, comments, and favorites, and then streams this data via Kafka. 
Also, KSqlDB was used for stream processing and the processed data is then sent to a Telegram bot for real-time notifications.

## Table of Contents

1. [System Architecture](#system-architecture)
2. [Requirements](#requirements)
3. [Getting Started](#getting-started)
4. [Configuration](#configuration)
5. [Running the Code](#running-the-code)
6. [How It Works](#how-it-works)
7. [Contributing](#contributing)
8. [Video](https://youtu.be/2Q4QX6Z3QZo)

## System Architecture
![YoutubeAnalytics architecture.png](assets%2FYoutubeAnalytics%20architecture.png)

## Requirements

- Python 3.10 (minimum)
- Kafka
- Telegram API
- Docker
- Confluent Containers (Zookeeper, Kafka, Schema Registry, Connect, ksqlDB, Control Center)

## Getting Started

1. Clone the repository.
   ```bash
   git clone https://github.com/airscholar/YoutubeAnalytics.git
   ```

2. Install Python dependencies.
   ```bash
   pip install -r requirements.txt
   ```

3. Make sure you have Docker and Confluent containers set up.

## Configuration

1. Open `config/config.local` and set the following:
    - `YOUTUBE_API_KEY`: Your YouTube API Key
    - `PLAYLIST_ID`: The YouTube playlist ID you want to track

2. Set up your Kafka server address in the main script, by default, it's set to `localhost:9092`.

## Running the Code

1. Start your Kafka and other Confluent services on Docker with
   ```bash
   docker compose up -d
   ``` 
2. Run the Python script.
    ```bash
    python YoutubeAnalytics.py
    ```

## How It Works

1. Fetches data from YouTube API using the given playlist ID.
2. Sends this data to Kafka.
3. You should have another component (not included here but in the video) that reads from this Kafka topic and performs real-time analytics using ksqlDB.
4. The analytics results are then sent to Telegram for real-time notifications.

## Contributing

Pull requests are welcome! For major changes, please open an issue first to discuss what you would like to change.

## Video

[![YoutubeAnalytics](https://img.youtube.com/vi/0aqSjJ3-4NI/0.jpg)](https://youtu.be/0aqSjJ3-4NI)