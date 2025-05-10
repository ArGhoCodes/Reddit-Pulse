# Reddit-Pulse
# 🧠 RedditPulse

**RedditPulse** is a scalable and cloud-integrated Reddit sentiment analysis pipeline that collects, processes, and analyzes Reddit posts in real-time. This project uses Apache Spark for distributed ETL, Flask for serving data via REST APIs, and Amazon S3 for centralized data storage. It employs advanced Natural Language Processing (NLP) techniques to detect and quantify sentiment expressed in Reddit threads.

---

## 📌 Features

- ✅ Automated data ingestion using Reddit API (PRAW)  
- ⚙️ Scalable data processing using Apache Spark  
- 🧠 NLP-based sentiment analysis with emoji-enhanced tagging  
- 🌐 REST API for retrieving processed data  
- ☁️ Cloud-based data storage with Amazon S3  

---

## 🧱 Tech Stack

| Layer             | Technology             | Role                                               |
|------------------|------------------------|----------------------------------------------------|
| **Data Ingestion** | PRAW (Reddit API)     | Scrapes Reddit threads and posts                  |
| **ETL Pipeline**  | Apache Spark           | Distributed processing and transformation of data |
| **Sentiment Analysis** | TextBlob / VADER  | Computes sentiment polarity scores                |
| **API Backend**   | Flask                  | Serves processed data via RESTful endpoints        |
| **Storage**       | Amazon S3              | Central repository for raw and processed data      |

---

## 🧠 NLP Sentiment Analysis (In-Depth)

At the core of RedditPulse is a Natural Language Processing module that evaluates the emotional tone of Reddit posts. This enables users to derive insights from public discourse.

### 🔬 Tools Used

- **TextBlob**: A Python NLP library for computing sentiment polarity.
- **VADER** *(optional)*: A social media-optimized rule-based sentiment analysis tool.

### 🧪 Methodology

Each Reddit post is assigned a **polarity score** ranging from -1.0 to 1.0:

- `> 0`: **Positive**
- `= 0`: **Neutral**
- `< 0`: **Negative**

Based on this score, the post is labeled accordingly. 

### 🧹 Text Preprocessing Steps

Before scoring, each Reddit post is cleaned using the following steps:

1. **Lowercasing** – Standardizes text for comparison  
2. **Punctuation Removal** – Strips non-alphabetic characters  
3. **Tokenization** – Splits text into words or phrases  
4. **Stopword Removal** – Removes common, uninformative words  
5. **(Optional)** Lemmatization – Converts words to base forms

### 😀 Emoji Mapping

To enhance interpretability, sentiment labels are supplemented with emojis:

| Sentiment | Emoji |
|-----------|--------|
| Positive  | 😊     |
| Neutral   | 😐     |
| Negative  | 😞     |

---


## 🚀 How It Works

1. **Collect Data**  
   Posts are fetched from Reddit using PRAW and saved as CSV to Amazon S3.

2. **Process Data**  
   Apache Spark performs scalable data transformation and sentiment tagging.

3. **Analyze Sentiment**  
   NLP is applied to compute polarity and label posts with sentiments and emojis.

4. **Serve via API**  
   A Flask-based API allows real-time retrieval of processed Reddit data.

---

## 🔧 Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/RedditPulse.git
cd RedditPulse
```

## 2. Configure AWS Credentials

```bash
aws configure
```
or set environment variables manually

```bash
export AWS_ACCESS_KEY_ID=your_key
export AWS_SECRET_ACCESS_KEY=your_secret
export AWS_DEFAULT_REGION=your_region
export S3_BUCKET_NAME=airscholar-reddit-engineering-bde
```

## 3. Run the API Server

```bash
cd api
python app.py
```

## 🌐 API Endpoints

| Method | Endpoint              | Description                            |
| ------ | --------------------- | -------------------------------------- |
| GET    | `/generate_post`      | Fetch new Reddit posts using PRAW      |
| GET    | `/get_processed_data` | Retrieve sentiment-tagged data from S3 |

## ✅ Example Workflow

1. Trigger GET /generate_post to collect new Reddit posts.

2. Run the Spark pipeline to process and score posts.

3. Access the processed sentiment data via GET /get_processed_data.

## 📃 License
This project is licensed under the MIT License.
