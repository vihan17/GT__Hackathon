### Transform raw CSV logs into executive-ready PDF reports — in under 30 seconds.

---

## **1. Problem Overview**
### **Real-World Context**
In AdTech workflows, Account Managers spend **4–6 hours every week** manually downloading CSVs, slicing data in Excel, and taking screenshots to prepare “Weekly Performance Reports” for clients.

### **The Pain**
- Slow  
- Boring  
- Error-prone  
- Delayed insights  

If a campaign starts burning budget or impressions drop in a key market, clients **may not know for days** because reporting is delayed.

### **My Solution**
Introducing **TrendSpotter** — an **event-driven automated reporting engine**.

Just **drop a raw CSV file** into a folder, and within **30 seconds**, TrendSpotter automatically:

- Processes the data  
- Detects anomalies  
- Generates AI-written insights  
- Produces a pixel-perfect PDF  
- Emails it directly to the user  

---

## **2. What the User Gets**
### **Simple Workflow**
**Input:** Upload or drop a CSV into the monitored folder  
**Wait:** ~30 seconds  
**Output:** A professionally formatted PDF containing:

- 📈 Week-over-week growth charts  
- 🚨 Detected anomalies (e.g., *“Traffic dropped 40% in Miami”*)  
- 🧠 AI-generated explanations  
- 🌦️ Optional external context (e.g., weather correlation)

---

## **3. Technical Architecture**
TrendSpotter is built as a **production-grade ETL + AI pipeline**.

### **🔹 1. Ingestion (Event-Driven)**
A Python Watchdog listener triggers the pipeline whenever a new CSV is added.

**Using Polars because:**
- Faster than Pandas  
- Strict schema validation  
- Low memory overhead  

---

### **🔹 2. Data Processing**
Using **Polars**, the pipeline:

- Cleans and normalizes raw logs  
- Computes week-over-week deltas  
- Builds structured metadata for ML + AI  
- Generates aggregated statistics  

---

### **🔹 3. Anomaly Detection**
Powered by **Isolation Forest (Scikit-Learn)** to automatically detect:

- Traffic drops  
- Impression spikes  
- City-level anomalies  
- CTR/CPC irregularities  

No manual rules — purely statistical.

---

### **🔹 4. Generative AI Insights**
TrendSpotter behaves like a **Senior Data Analyst**.

- Generates narratives using **Google Gemini 1.5 Pro**  
- Few-shot prompting for consistency  
- Writes insights tied to actual data trends  

**Hallucination Guardrails:**
- Strict JSON context  
- Numeric cross-validation  
- Fallback to `"Unknown"` when data is missing  

---

### **🔹 5. Report Generation**
Final PDF is produced using:

- **Plotly** → charts  
- **HTML/CSS template** → layout  
- **WeasyPrint** → PDF rendering  

Reports are emailed automatically via SMTP.

---

## **4. Tech Stack**

| Layer | Tools |
|-------|-------|
| **Language** | Python 3.11 |
| **Data Engine** | Polars |
| **ML** | Scikit-Learn (Isolation Forest) |
| **AI** | Gemini 1.5 Pro (Vertex AI) |
| **Visualization** | Plotly |
| **PDF Renderer** | WeasyPrint |
| **Orchestration** | Docker + Docker Compose |

---

## **5. Challenges & Learnings**

### **🚧 Challenge 1: AI Hallucinations**
**Problem:** Gemini occasionally invented explanations such as weather changes without weather data.  
**Solution:** Implemented a **Strict Context Prompting Framework** with numeric validation.  
This reduced hallucinations significantly.

---

### **🚧 Challenge 2: Docker Networking**
**Problem:** Python container couldn’t send outgoing emails.  
**Solution:** Configured SMTP ports + Docker networking rules in `docker-compose.yml`.

---

## **6. Visual Proof**
*(Add your screenshots here)*

- Terminal showing Isolation Forest output  
- Final PDF layout  
- Email delivery screenshot  

---

## **7. How to Run**

```bash
# 1. Clone the repository
git clone https://github.com/username/trendspotter.git
cd trendspotter

# 2. Add API key
export GEMINI_API_KEY="your_key_here"

# 3. Build and run
docker-compose up --build

# 4. Trigger pipeline
mv data/sample.csv data/input/
