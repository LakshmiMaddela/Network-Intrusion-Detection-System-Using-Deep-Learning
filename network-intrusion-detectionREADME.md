# Network Intrusion Detection System (NIDS)

A web-based Network Intrusion Detection System powered by Deep Learning and Machine Learning models. The system classifies network traffic as **Normal** or an **Attack**, and further identifies the attack type using the KDD Cup 99 dataset.

---

## Features

- Binary classification — Normal vs Attack
- Multi-class attack type identification (DoS, Probe, R2L, U2R)
- Three input methods — Random sample, manual parameter input, CSV file upload
- Clean dark-themed web dashboard
- Real-time predictions via REST API (Flask backend)

---

## Models

| Model | Type | Status |
|-------|------|--------|
| KNN | K-Nearest Neighbors | Working |
| CNN | Convolutional Neural Network | Working |
| Random Forest | Ensemble | Unavailable (sklearn version mismatch) |
| LSTM | Recurrent Neural Network | Unavailable (Keras version mismatch) |

---

## Attack Types Detected

| Label | Description |
|-------|-------------|
| Normal | Safe, legitimate network traffic |
| DoS | Denial-of-Service — floods target to make it unreachable |
| Probe | Network scanning to discover weaknesses |
| R2L | Remote to Local — unauthorized remote access attempt |
| U2R | User to Root — privilege escalation attack |

---

## Project Structure

```
├── app.py                          # Flask backend (entry point)
├── templates/
│   └── index.html                  # Frontend UI
├── Uploaded_files/                 # Stores uploaded CSV files
├── knn_binary_class.sav            # KNN binary classification model
├── knn_multi_class.sav             # KNN multi-class model
├── latest_cnn_bin.h5               # CNN binary classification model
├── latest_cnn_multiclass.h5        # CNN multi-class model
├── fs_new validation project.csv   # Validation dataset
├── nids_random_updated.py          # Original random prediction script
├── nids_parameter_updated.py       # Original manual param script
├── nids_csv_updated.py             # Original CSV prediction script
├── HOW_TO_RUN.txt                  # Quick-start guide
└── requirements.txt                # Python dependencies
```

---

## Installation

**1. Clone the project**

```bash
git clone https://github.com/Shaik-Sohail-72/Network-Intrusion-Detection-Using-Deep-Learning.git
cd Network-Intrusion-Detection-Using-Deep-Learning-master
```

**2. Install dependencies**

```bash
pip install flask tensorflow scikit-learn pandas numpy werkzeug
```

> Requires **Python 3.13**

---

## Running the App

```bash
python app.py
```

Open your browser and go to:

```
http://127.0.0.1:5000
```

Press `CTRL + C` in the terminal to stop the server.

---

## Usage

### Tab 1 — Random Sample
Picks a random row from the validation dataset and runs KNN + CNN predictions instantly.

### Tab 2 — Manual Input
Enter all 16 network features using dropdowns and number fields. Click **Predict** to see results from both models side by side.

### Tab 3 — CSV Upload
Upload a CSV file with 16 feature columns (no label column). Select a model (KNN or CNN) and click **Analyse** to get a summary and row-by-row results table.

**Expected CSV column order:**
```
protocol_type, service, flag, logged_in, count,
srv_serror_rate, srv_rerror_rate, same_srv_rate, diff_srv_rate,
dst_host_count, dst_host_srv_count, dst_host_same_srv_rate,
dst_host_diff_srv_rate, dst_host_same_src_port_rate,
dst_host_serror_rate, dst_host_rerror_rate
```

---

## Input Features

The system uses 16 network traffic features from the KDD Cup 99 dataset:

| # | Feature | Type | Description |
|---|---------|------|-------------|
| 1 | `protocol_type` | Categorical | Network protocol (tcp, udp, icmp) |
| 2 | `service` | Categorical | Destination service (http, ftp, smtp, etc.) |
| 3 | `flag` | Categorical | Connection status flag (SF, REJ, S0, etc.) |
| 4 | `logged_in` | Binary | 1 if successfully logged in, 0 otherwise |
| 5 | `count` | Integer | Connections to same host in past 2 seconds |
| 6 | `srv_serror_rate` | Float | % of connections with SYN errors |
| 7 | `srv_rerror_rate` | Float | % of connections with REJ errors |
| 8 | `same_srv_rate` | Float | % of connections to the same service |
| 9 | `diff_srv_rate` | Float | % of connections to different services |
| 10 | `dst_host_count` | Integer | Connections to same destination host |
| 11 | `dst_host_srv_count` | Integer | Connections to same service on destination |
| 12 | `dst_host_same_srv_rate` | Float | % same service on destination host |
| 13 | `dst_host_diff_srv_rate` | Float | % different service on destination host |
| 14 | `dst_host_same_src_port_rate` | Float | % connections from same source port |
| 15 | `dst_host_serror_rate` | Float | % SYN error connections on destination host |
| 16 | `dst_host_rerror_rate` | Float | % REJ error connections on destination host |

---

## API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/` | Serves the frontend UI |
| `POST` | `/predict/random` | Random row prediction (no body required) |
| `POST` | `/predict/params` | Manual input prediction (JSON body) |
| `POST` | `/predict/csv` | CSV file prediction (multipart form data) |

---

## Dataset

Based on the **KDD Cup 1999** network intrusion detection dataset with feature selection applied.

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Backend | Python, Flask |
| ML / DL | TensorFlow / Keras, scikit-learn |
| Frontend | HTML, CSS, JavaScript (vanilla) |
| Data Processing | pandas, NumPy |
