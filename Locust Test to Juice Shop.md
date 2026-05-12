
```markdown
# 📊 Scalability and Performance Analysis of Web APIs Under Load Using Locust

![Python](https://img.shields.io/badge/Python-3.10-blue?logo=python&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Enabled-2496ED?logo=docker&logoColor=white)
![Locust](https://img.shields.io/badge/Locust-Performance_Testing-green?logo=python&logoColor=white)
![OWASP Juice Shop](https://img.shields.io/badge/OWASP-Juice_Shop-orange?logo=owasp&logoColor=white)

**Prepared by:** ISYRAQUL WALDAN UMAIRAH BT ABD RAZAK  
**Student ID:** 2025310499  
**Group:** CDCS2555A  
**Prepared for:** SIR SHAHADAN BIN SAAD  

---

## 🔗 1.0 Introduction
Performance testing is an important activity in system testing to evaluate how a web application behaves under different traffic conditions. It helps identify:
- System limitations  
- Bottlenecks  
- Response delays  
- Stability issues  

In this assessment, the performance testing tool used is **Locust** together with **OWASP Juice Shop**.  

Three types of performance tests were conducted:  
- Load Test 📌  
- Stress Test 🧪  
- Spike Test ⚡  

---

## ⚡ 2.0 Tool Selection Justification

### 🖥️ Locust
Chosen because it is lightweight, Python-based, and open-source.  
- Easy to install/configure  
- Flexible Python scripting  
- Real-time monitoring dashboard  
- Distributed load testing  
- Metrics: RPS, Response Time, Failures, Users  

### 🔒 OWASP Juice Shop
Chosen because it is free, open-source, and security-focused.  
- Proxy interception for HTTP traffic  
- Identifies vulnerabilities  
- Integrates with browsers/testing environments  

---

## 📌 3.0 Setup Procedure

### 🐳 Install Juice Shop (Docker)
```bash
sudo apt update
sudo apt install docker.io
sudo docker pull bkimminich/juice-shop
sudo docker run -d --name juice -p 3000:3000 bkimminich/juice-shop
```
Access: `http://localhost:3000`

### 🐍 Install Locust
```bash
sudo apt update
sudo apt install python3-venv -y
python3 -m venv venv
source venv/bin/activate
pip install locust
```
Run Locust:  
```bash
locust -H https://192.168.100.22:3000
```
Dashboard: `http://localhost:8089`

---

## 📊 4.0 Load Test
**Config:** 50 users, 5 users/sec, 5 min  
**Outcome:** Stable response, minimal failures, smooth operation  

---

## 🧪 5.0 Stress Test
**Config:** 500 users, 50 users/sec, 10 min  
**Outcome:** Increased response time, request failures, system slowdown  

---

## ⚡ 6.0 Spike Test
**Config:** Normal (10 users) → Spike (1000 users) → Recovery (10 users)  
**Outcome:** Temporary latency, failures during spike, recovery after traffic drop  

---

## 📈 7.0 Results

### 🔹 Requests per Second (RPS)
- Stable at normal load  
- 150–220 RPS under stress  
- Fluctuations during spike  

### 🔹 Response Times
- Low during normal/stress  
- High latency during spike  

### 🔹 Concurrent Users
- 500 steady in stress test  
- 1000 spike → instability  

| Test Type   | Result |
|-------------|--------|
| Load Test | Stable ✅ |
| Stress Test | Degradation ⚠️ |
| Spike Test | Instability ❌ |

---

## 📌 8.0 Conclusion
- Load Test → Stable under normal traffic  
- Stress Test → Performance degradation at high load  
- Spike Test → Instability during sudden surges  

**Recommendations:**  
- Server scaling  
- Database optimization  
- Caching mechanisms  
- Load balancing  
```

