# Application + Transport Layer Protocol Visualizer

An interactive, educational web dashboard that shows how everyday network activities work across the **Application Layer** and the **Transport Layer**.

Pick an activity, then step through the protocol sequence one message at a time while a synchronized **Transport Layer Inspector** shows the TCP/UDP details behind each step.

> **Note:** This is a simulation for learning. It does not capture real packets or open raw sockets. All TCP/UDP values (ports, sequence numbers, windows, etc.) are generated for teaching purposes.

**Live demo:** _add your Render link here, e.g. `https://transport-layer-viz.onrender.com`_

---

## Features

### Application Layer
- Three activities to explore:
  - **Web Browsing**: DNS query/response, then HTTP/1.1 request and response
  - **Email Client**: DNS MX lookup, then SMTP submission on port 587
  - **Media Streaming**: DNS lookup, then HTTP/HLS-style requests
- Step-by-step protocol timeline with an activity log

### Transport Layer
- TCP vs UDP identification for every event (UDP for DNS, TCP for HTTP/SMTP)
- Source and destination ports
- TCP three-way handshake: `SYN`, `SYN-ACK`, `ACK`
- Sequence and acknowledgment numbers, TCP flags, and connection states
- Receive window (flow control), MSS, and simulated congestion window
- Checksum, header length, payload size, and multi-segment indication
- Graceful four-step teardown: `FIN`, `ACK`, `FIN`, final `ACK`
- UDP datagram fields for DNS events
- Interactive **packet loss and retransmission** demonstration
- Expandable **TCP header reference**

---

## Tech Stack

- **Backend:** Python, Flask
- **Frontend:** HTML, CSS, vanilla JavaScript
- **Deployment:** Gunicorn on Render

---

## Project Structure

```
.
├── app.py                 # Flask app (home page + /api/health)
├── templates/
│   └── index.html         # Dashboard page
├── static/
│   ├── script.js          # Simulation and visualization logic
│   └── style.css          # Styling
├── requirements.txt       # Python dependencies
├── Procfile               # Process definition for hosting
├── TRANSPORT_LAYER_UPDATE.md
└── README.md
```

---

## Run Locally

```bash
# 1. Create and activate a virtual environment
python -m venv venv

# Windows (Command Prompt)
venv\Scripts\activate
# Windows (PowerShell)
venv\Scripts\Activate.ps1
# Mac / Linux
source venv/bin/activate

# 2. Install dependencies
pip install -r requirements.txt

# 3. Start the app
python app.py
```

Then open **http://127.0.0.1:5000** in your browser.

---

## Deploy on Render

1. Push this project to a GitHub repository.
2. On [render.com](https://render.com), choose **New + → Web Service** and select the repo.
3. Use these settings:
   - **Build Command:** `pip install -r requirements.txt`
   - **Start Command:** `gunicorn app:app`
   - **Instance Type:** Free
4. Click **Create Web Service**. Every push to `main` redeploys automatically.

You can confirm the service is running by opening `/api/health`, which returns a JSON status message.

---

## Learning Goals

- See how an application protocol (HTTP, SMTP, DNS) sits on top of a transport protocol (TCP or UDP)
- Understand why DNS commonly uses UDP while web and email use TCP
- Follow a TCP connection from handshake to teardown
- Understand sequence numbers, acknowledgments, flow control, and retransmission

---

## Author

**Debajeet Paul**
B.Tech CSE, Central Institute of Technology, Kokrajhar
GitHub: [@debajeetpaul955-cpu](https://github.com/debajeetpaul955-cpu)
