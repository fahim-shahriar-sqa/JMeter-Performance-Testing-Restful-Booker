
# Restful Booker - Performance Testing with JMeter

This project demonstrates performance testing of the [Restful Booker](https://restful-booker.herokuapp.com/) API using **Apache JMeter**.  
It covers **Load Test, Endurance Test, Spike Test, Stress Test, and Volume Test** with reports and analysis.  

---

## Tools & Technologies
- Apache JMeter (5.x)  
- Java (JDK 8+)  
- Restful Booker API  
- GitHub (for version control and portfolio showcase)  

---

## Objectives
- Simulate real-world traffic on Restful Booker APIs  
- Validate API performance under different conditions:  
  - Normal load  
  - Long-duration usage  
  - Increasing stress until failure  
- Generate detailed HTML reports for analysis  

---

## Project Structure
```
restful-booker-performance-testing/
│
├── TestPlans/                  # JMeter .jmx files
│   ├── load_test.jmx
│   ├── endurance_test.jmx
│   ├── stress_test.jmx

│
├── Reports/                    # Generated HTML reports
│   ├── load_test_report/
│   ├── endurance_test_report/
│   ├── stress_test_report/
│
├── Screenshots/                # Screenshots of graphs & results
│   ├── load_test_summary.png
│   ├── endurance_test_response_.png
│   ├── stress_test_throughput.png
│
└── README.md                   # Project documentation
```

---

## APIs Tested
- `POST /auth` → CreateToken  
- `GET /booking` → GetBookingIds  
- `GET /booking/{id}` → GetBooking  
- `POST /booking` → CreateBooking  
- `PUT /booking/{id}` → UpdateBooking  
- `PATCH /booking/{id}` → PartialUpdateBooking  
- `DELETE /booking/{id}` → DeleteBooking  
- `GET /ping` → HealthCheck  

---

## Test Scenarios

### 1. Load Test

**Purpose:** Measure API performance under increasing concurrent load.  
**Environment:** Apache JMeter  
**Execution:** Defined threads (users) with loop counts.  

**Summary Table**

| Threads | Loop | Total Requests | Avg TPS | Errors | Error Rate |
|---------|------|----------------|---------|--------|------------|
| 300     | 10   | 15,000         | 151/s   | 0      | 0%         |
| 400     | 10   | 20,000         | 194/s   | 134    | 0.67%      |

**Observations**
- At 300 users, system handled 15,000 requests smoothly with 0% error rate.  
- At 400 users, throughput increased to 194 TPS, but 134 requests failed (0.67% errors).  
- System shows signs of nearing its performance threshold beyond 400 concurrent users.  

---

### 2. Endurance Test

**Purpose:** Verify stability under continuous moderate load.  

**Configuration**
- Threads (Users): 100  
- Ramp-Up Time: 20 seconds  
- Duration: 6 minutes  

**Results**
- Total Requests: 113,243  
- Error Rate: 0.17%  
- Throughput: 314 TPS  
- Average TPS: 309  
- Peak TPS: 311  

**Response Times**
- Average: 309 ms  
- 90th Percentile: 314 ms  
- 95th Percentile: 320 ms  
- Minimum: 268 ms  
- Maximum: 6,946 ms  

**Observations**
- Server sustained 100 concurrent users over 6 minutes with minimal errors.  
- Average response time ~309 ms, stable with occasional spikes.  
- Throughput remained consistent.  
- No significant degradation or instability observed.  

---

### 3. Stress Test

**Purpose:** Identify limits and performance degradation points under extreme load.  

**Configuration**

| Test File | Threads | Ramp-Up Time (s) | Loop Count |
|-----------|---------|------------------|------------|
| restful_booker_stress_T1500_R20_L10.jmx | 1500 | 20 | 10 |
| restful_booker_stress_T2500_R20_L10.jmx | 2500 | 20 | 10 |

**Results – 1500 Users**
- Average TPS: 645.5  
- Avg Response Time: 1503 ms  
- 90th Percentile: 3554 ms  
- 95th Percentile: 3731 ms  
- Min: 267 ms  
- Max: 7040 ms  
- Errors: Not fully available  

**Results – 2500 Users**
- Average TPS: 578.8  
- Avg Response Time: 2616 ms  
- 90th Percentile: 5424 ms  
- 95th Percentile: 7763 ms  
- Min: 266 ms  
- Max: 41,255 ms  
- Errors: 1.69%  

**Observations**
- Stable up to ~1500 users with acceptable response times (<4s for 95%).  
- Beyond 2000 users, significant degradation: higher latencies, error rates, and instability.  

---

## How to Run

Run tests in non-GUI mode (recommended):

```bash
jmeter -n -t TestPlans/load_test.jmx -l Reports/load_test.jtl -e -o Reports/load_test_report
```

- `-n` → non-GUI mode  
- `-t` → test plan file (.jmx)  
- `-l` → result log file (.jtl)  
- `-e -o` → generate HTML report  

---

## Sample Reports & Screenshots
## 📊 Screenshots

### 🔹 Load Test
- **300 Threads**
  
  ![Load Test - T300 R100 L10](https://drive.google.com/uc?export=view&id=1QwiFtvfaa_5cFHM5EDGmDp5XBHNlCuQ-)

- **400 Threads**
  
  ![Load Test - T400 R100 L10](https://drive.google.com/uc?export=view&id=1XbYKayS-j1lIHdBrD5-G4G-t6nAmWWgI)

---

### 🔹 Endurance Test
- **Summary Report**
  
  ![Endurance Summary Report](https://drive.google.com/uc?export=view&id=1HlBnvsVvGyDF_TSqSleAu4frS2eIo85K)

---

### 🔹 Stress Test
- **1500 Threads**
  
  ![Stress Test - T1500 R20 L10 Summary Table](https://drive.google.com/uc?export=view&id=1eWzE0VXajOUjzRQKR2uFzi2ouQdfHGJ6)

- **2500 Threads**
  
  ![Stress Test - T2500 R20 L10 Summary Table](https://drive.google.com/uc?export=view&id=1IWoVbIPYv9e4zi-A5QKywxFYQzkPrrpj)


---

## Key Findings
- Average response time under load: ~200 ms  
- System stable up to 400 concurrent users before errors appear  
- Spike traffic doubled latency but system remained functional  
- Endurance test showed consistent performance over 6 minutes  

---

## Conclusion
This project demonstrates end-to-end performance testing of a REST API using Apache JMeter.  
It highlights test design, execution, reporting, and analysis across multiple performance scenarios.  

--- 
