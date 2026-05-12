<img width="1882" height="809" alt="LogoUiTM" src="https://github.com/user-attachments/assets/3ba6de3b-4be6-4400-b304-70f445571cdd" />

# 📊 Scalability and Performance Analysis of Web APIs Under Load Using Locust

**Prepared by:** ISYRAQUL WALDAN UMAIRAH BT ABD RAZAK  
**Student ID:** 2025310499  
**Group:** CDCS2555A  
**Prepared for:** SIR SHAHADAN BIN SAAD  

---

## 🖥️ Tools Used
- **Locust** ⚡  
<img width="400" height="96" alt="Locust-logo" src="https://github.com/user-attachments/assets/3b1451ea-9025-427d-b5f7-adb70c6c4dae" />

- **OWASP Juice Shop** 🔒  
<img width="205" height="246" alt="images" src="https://github.com/user-attachments/assets/1072c6d5-c0a1-4961-bec3-0a66f2df35f7" />


Testing Types:  
- Load Test 📌  
- Stress Test 🧪  
- Spike Test ⚡  

Target Application: **OWASP Juice Shop**

---

## 🔗 1.0 Introduction
Performance testing is an important activity in system testing to evaluate how a web application behaves under different traffic conditions. It helps identify system limitations, bottlenecks, response delays, and stability issues before the system is deployed into a production environment.
In this assessment, the performance testing tool used is Locust together with OWASP Juice Shop. Locust is used to simulate user traffic and measure system performance, while OWASP Juice Shop is used to support security-related testing and traffic inspection.

Three types of performance tests were conducted:
•	Load Test
•	Stress Test
•	Spike Test

The purpose of these tests is to evaluate:
•	System responsiveness
•	Maximum handling capacity
•	Stability under heavy traffic
•	Recovery capability after sudden traffic spikes

---

## ⚡ 2.0 Tool Selection Justification

### 🖥️ Locust (https://locust.io)
Locust was selected because it is a lightweight and powerful open-source performance testing tool written in Python. It allows testers to simulate thousands of concurrent users with customizable behaviors.

- Lightweight, Python-based, open-source  
- Simulates thousands of concurrent users  
- Real-time monitoring dashboard  
- Distributed load testing support  
- Metrics: RPS, Response Time, Failures, Users  

### 🔒 OWASP Juice Shop (https://owasp.org/www-project-juice-shop/)
OWASP Juice Shop was selected because it is a free and open-source web application security testing tool. It can inspect HTTP traffic and identify security vulnerabilities while monitoring application requests.

- Free, open-source  
- Proxy interception for HTTP traffic  
- Identifies vulnerabilities  
- Integrates with browsers/testing environments  

---

## 📌 3.0 Setup Procedure

### 🐳 Install Juice Shop (Docker)
```bash
sudo apt update
sudo apt install docker.io
sudo systemctl enable --now docker
sudo docker pull bkimminich/juice-shop
sudo docker run -d --name juice -p 3000:3000 bkimminich/juice-shop
```
Access: `http://localhost:3000`

### 🐍 Install Locust
Create a simple test file:
```bash
nano locustfile.py
```
Paste this:
```bash
from locust import HttpUser, task, between

class WebsiteUser(HttpUser):
    wait_time = between(1, 3)

    @task
    def home(self):
        self.client.get("/")
```
Save:

CTRL + O
ENTER
CTRL + X
```bash
sudo apt install python3-locust
locust -f locustfile.py --host=http://192.168.100.22:3000
sudo apt install python3-venv -y
mkdir locust
cd locust
python3 -m venv venv
source venv/bin/activate
pip install locust
locust --version
```
Run Locust:  
```bash
locust -H https://192.168.100.22:3000
```
Dashboard: `http://localhost:8089`

---

## 📊 4.0 Load Test
Load testing is performed to evaluate how the application behaves under expected normal traffic conditions. The objective is to ensure the system can maintain stable performance during regular usage.

**Test Configuration**
| Parameter	| Value |
|----------|----------|
| Users	| 50 |
| Spawn Rate	| 5 users/sec |
| Duration	| 5 minutes |

**Result/Outcome** 
•	Stable response time
•	Minimal failures
•	Consistent request handling
•	Smooth system operation under normal load
 

---

## 🧪 5.0 Stress Test
Stress testing is conducted to determine the maximum limit of the system by gradually increasing traffic beyond normal operating capacity.
The purpose is to observe:
•	System degradation
•	Performance bottlenecks
•	Failure points
•	Recovery capability

**Test Configuration**
| Parameter	| Value |
|----------|----------|
| Users	| 500 |
| Spawn Rate	| 50 users/sec |
| Duration	| 10 minutes | 

**Result/Outcome** 
•	Increased response time
•	Possible request failures
•	System slowdown under heavy load
•	Identification of maximum handling capacity


---

## ⚡ 6.0 Spike Test
Spike testing evaluates how the application reacts to sudden and extreme increases in traffic within a short period.
This test determines whether the system can:
•	Handle sudden traffic surges
•	Maintain availability
•	Recover after traffic returns to normal

**Test Configuration**
| Stage	| Users |
|----------|----------|
| Normal Traffic	| 10 |
| Sudden Spike	| 1000 |
| Recovery | 10 | 

**Result/Outcome** 
•	Temporary increase in response time
•	Possible failures during spike
•	Recovery after traffic decreases


---

## 📈 7.0 Results

 

| Test Type   | Result |
|-------------|--------|
| Load Test | Stable ✅ |
| Stress Test | Degradation ⚠️ |
| Spike Test | Instability ❌ |

---


## 📌 8.0 Conclusion & Recommendation
The performance testing successfully evaluated the application under different traffic conditions using Locust and OWASP ZAP.
The Load Test showed that the system can handle normal user traffic with stable response times and minimal failures. During the Stress Test, the application experienced slower response times and performance degradation as the number of users increased significantly. In the Spike Test, sudden traffic surges caused instability and high latency, indicating that the server has limitations when handling abrupt increases in concurrent users.
Overall, the testing demonstrates that the system performs adequately under normal operating conditions but requires optimization for handling very high traffic loads and sudden spikes. Improvements such as server scaling, database optimization, caching mechanisms, and load balancing are recommended to improve system stability and performance under extreme conditions.


