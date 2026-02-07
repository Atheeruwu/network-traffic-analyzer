# Network Traffic Analyzer


A professional network traffic analysis tool that combines real-time packet capture, machine learning anomaly detection, and an interactive dashboard for network monitoring and security analysis.

## 🔍 Features

- **Real-time Packet Analysis**: Captures and analyzes network traffic in real-time
- **Anomaly Detection**: Uses Isolation Forest ML algorithm to detect suspicious traffic
- **Port Scan Detection**: Identifies port scanning attempts in real-time
- **Interactive Dashboard**: Live visualization of network metrics and anomalies
- **Email Alerts**: Configurable alerts for high anomaly rates
- **PCAP Export**: Save captured traffic for further analysis
- **SQLite Logging**: Persistent storage of packet metadata and anomalies

## 🛠 Technology Stack

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Scapy](https://img.shields.io/badge/Scapy-2.4+-yellow)
![Dash](https://img.shields.io/badge/Dash-2.0%2B-orange)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-1.0%2B-green)
![SQLite](https://img.shields.io/badge/SQLite-3.0%2B-lightgrey)

**Core Components**:
- Packet Capture: Scapy
- Dashboard: Plotly Dash
- Machine Learning: Scikit-learn
- Database: SQLite
- Email: SMTP with TLS

## 🚀 Getting Started

### Prerequisites
- Python 3.8+
- libpcap (for packet capture)
- Network interface with promiscuous mode access

### Installation

1. Clone the repository:
```bash
git clone https://github.com/Opikadash/network-traffic-analyzer.git
cd network-traffic-analyzer
```

2. Create and activate a virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # Linux/MacOS
venv\Scripts\activate     # Windows
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

4. Set up environment variables:
```bash
cp .env .env
```
Edit the `.env` file with your email configuration (optional)

### Usage

Start the application:
```bash
python app.py
```

Access the dashboard at: http://127.0.0.1:8055/

## 🖥️ Dashboard Features

- **Real-time Protocol Distribution**: Visualize traffic by protocol
- **Anomaly Detection Rate**: See percentage of suspicious traffic
- **Time-series Analysis**: Track packet volume over time
- **Export Functionality**: Save captured packets to PCAP
- **Protocol Filtering**: Focus on specific protocols

## 🧠 What It’s Analyzing 

The app captures live network packets from your machine’s network interface and analyzes each packet in two ways:

1) **ML anomaly detection (Isolation Forest)**  
It extracts basic features from each packet (length, TCP/UDP/ICMP/DNS flags) and uses an Isolation Forest model to flag packets that look unusual compared to recent traffic.

2) **Port-scan detection**  
It watches for a single source IP contacting many different ports within a short time window (a common scan pattern).

Every packet is logged to SQLite, and summary stats are shown on the dashboard in real time.

## 🔎 What You See on the Dashboard

- **Anomaly Distribution (Pie Chart)**: Normal vs. anomaly counts
- **Protocol Packet Count (Bar Chart)**: TCP/UDP/ICMP/DNS/Other counts
- **Packet Count Over Time (Line Chart)**: How traffic volume changes
- **Protocol Filter**: View stats for a single protocol
- **Export Button**: Save all captured packets to `results/exported_packets.pcap`

## 🧩 File-by-File Explanation

- `app.py`: Main application. Starts packet capture, trains the ML model, runs the Dash dashboard, logs to SQLite, and triggers email alerts.
- `analyzer/features.py`: Converts each packet into numeric features for the ML model.
- `analyzer/filter_ml.py`: Isolation Forest model for anomaly detection (fit + predict).
- `analyzer/portscan.py`: Simple heuristic to detect port scans by tracking how many ports an IP touches in a short time window.
- `analyzer/stats.py`: Thread-safe counters and time-series data used by the dashboard.
- `results/`: Auto-created output folder for `packet_logs.db` (SQLite) and PCAP exports.
- `.env`: Optional email settings used for alerts (SMTP).
- `requirements.txt`: Python dependencies.


## 🔧 Configuration

Customize the analyzer by modifying these parameters in `app.py`:

```python
# Analysis parameters
anomaly_threshold = 10  # % threshold for email alert
alert_interval = 300    # seconds between alerts

# Capture settings
capture_count = 10      # packets per capture batch
capture_timeout = 1     # seconds
```

## 🧪 Testing the System

1. Generate test traffic while the analyzer is running:
```bash
# Linux/MacOS
ping google.com

# Windows
ping -t google.com
```

2. Simulate a port scan (requires nmap):
```bash
nmap -T4 localhost
```

3. Check the dashboard for detected anomalies

## 🌟 Professional Highlights

This project demonstrates:

1. **Real-time Data Processing**: Efficient packet handling with multi-threading
2. **ML Integration**: Anomaly detection using Isolation Forest algorithm
3. **Dashboard Development**: Interactive visualization with Plotly Dash
4. **Database Management**: SQLite for persistent storage
5. **Security Practices**: Secure SMTP communication and proper credential handling
6. **Production-grade Architecture**: Robust error handling and graceful shutdown

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request



**Professional Development Notes**:

This project was developed with a focus on:
- Clean, maintainable code architecture
- Comprehensive error handling
- Scalable design patterns
- Production-ready deployment considerations
- Security best practices
- Professional documentation

The implementation showcases full-stack development skills from low-level packet processing to high-level dashboard visualization, demonstrating expertise across multiple domains of software development.

---

## Repository Structure
```
network-traffic-analyzer/
├── analyzer/               # Core analysis modules
│   ├── features.py         # Feature extraction
│   ├── filter_ml.py        # ML anomaly detection
│   ├── portscan.py         # Port scan detection
│   └── stats.py            # Statistics tracking
├── results/                # Output directory (auto-created)
│   ├── captured_traffic.pcap
│   └── packet_logs.db
├── .env           # Environment template
├── app.py                 # Main application
├── README.md               # This file
└── requirements.txt        # Dependencies
```
#
