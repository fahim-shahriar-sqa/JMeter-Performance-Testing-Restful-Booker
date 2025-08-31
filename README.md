# Restful Booker - Performance Testing with JMeter

This project demonstrates **performance testing** of the [Restful Booker](https://restful-booker.herokuapp.com/) API using **Apache JMeter**.  
It covers **Load Test, Endurance Test, Spike Test, Stress Test, and Volume Test** with reports and analysis.  

---

## 🛠 Tools & Technologies
- **Apache JMeter** (5.x)
- **Java** (JDK 8+)
- **Restful Booker API**
- **GitHub** (for version control and portfolio showcase)

---

## 🎯 Objectives
- Simulate real-world traffic on Restful Booker APIs
- Validate API performance under different conditions:
  - Normal load
  - Long-duration usage
  - Sudden traffic spikes
  - Increasing stress until failure
  - High data volume
- Generate detailed HTML reports for analysis

---

## 📂 Project Structure
```
restful-booker-performance-testing/
│
├── TestPlans/                  # JMeter .jmx files
│   ├── load_test.jmx
│   ├── endurance_test.jmx
│   ├── spike_test.jmx
│   ├── stress_test.jmx
│   ├── volume_test.jmx
│
├── Reports/                    # Generated HTML reports
│   ├── load_test_report/
│   ├── endurance_test_report/
│   ├── spike_test_report/
│   ├── stress_test_report/
│   ├── volume_test_report/
│
├── Screenshots/                # Screenshots of graphs & results
│   ├── load_test_summary.png
│   ├── spike_test_response_times.png
│   ├── stress_test_throughput.png
│
└── README.md                   # Project documentation
```

---

## 🔗 APIs Tested
- `POST /auth` → CreateToken  
- `GET /booking` → GetBookingIds  
- `GET /booking/{id}` → GetBooking  
- `POST /booking` → CreateBooking  
- `PUT /booking/{id}` → UpdateBooking  
- `PATCH /booking/{id}` → PartialUpdateBooking  
- `DELETE /booking/{id}` → DeleteBooking  
- `GET /ping` → HealthCheck  

---

## 📊 Test Scenarios

### 1. Load Test
- **Threads (Users):** 100  
- **Ramp-Up:** 20s  
- **Loop Count:** 10  
- ✅ Checks performance under expected normal load  

### 2. Endurance Test
- **Threads:** 50  
- **Ramp-Up:** 10s  
- **Duration:** 2 hours  
- ✅ Checks stability over long time  

### 3. Spike Test
- **Threads:** Jump from 10 → 500 in 5s  
- **Ramp-Up:** 5s  
- **Loop Count:** 5  
- ✅ Checks reaction to sudden traffic surge  

### 4. Stress Test
- **Threads:** Start at 100 → increase to 200, 400, 800  
- **Ramp-Up:** 30s each step  
- ✅ Identifies breaking point under extreme load  

### 5. Volume Test
- **Threads:** 20  
- **Ramp-Up:** 10s  
- **Loop Count:** 10  
- **Payload:** Large booking JSON (big request body)  
- ✅ Validates system behavior with heavy data  

---

## 🖥️ How to Run
Run any test plan in **non-GUI mode** (recommended for reporting):

```bash
jmeter -n -t TestPlans/load_test.jmx -l Reports/load_test.jtl -e -o Reports/load_test_report
```

- `-n` → non-GUI mode  
- `-t` → test plan file (.jmx)  
- `-l` → result log file (.jtl)  
- `-e -o` → generate HTML report  

---

## 📸 Sample Reports & Screenshots
### Load Test Report
![Load Test Summary](Screenshots/load_test_summary.png)

### Spike Test Report
![Spike Test Response Times](Screenshots/spike_test_response_times.png)

### Stress Test Throughput
![Stress Test Throughput](Screenshots/stress_test_throughput.png)

---

## 📈 Key Findings
- Average response time under load: **~200ms**  
- System stable up to **400 concurrent users** before errors appear  
- Spike traffic handled but latency increased by **x2**  
- Endurance test showed **consistent performance over 2 hours**  

---

## ✅ Conclusion
This project demonstrates **end-to-end performance testing** of a REST API using JMeter.  
It highlights different performance scenarios and how to analyze reports for insights.  

---

## 👨‍💻 Author
**Fahim Shahriar**  
- 📧 Email: 
- 🌐 LinkedIn: 
- 💻 GitHub: 
