# ITT440_Network-Programming

**Scalability and Performance Analysis of Web APIs Under Load Using Locust**

PREPARED BY: ISYRAQUL WALDAN UMAIRAH BT ABD RAZAK

STUDENT ID: 2025310499

GROUP: CDCS2555A

PREPARED FOR: SIR SHAHADAN BIN SAAD

- **Tools :** Locust
- **Testing Type :** Load, Stress and Spike Test
- **Target Web Application:** OWASP Juice Shop

**1.0 Introduction**

Performance testing is an important activity in system testing to evaluate how a web application behaves under different traffic conditions. It helps identify system limitations, bottlenecks, response delays, and stability issues before the system is deployed into a production environment.

In this assessment, the performance testing tool used is Locust together with OWASP Juice Shop. Locust is used to simulate user traffic and measure system performance, while OWASP Juice Shop is used to support security-related testing and traffic inspection.

Three types of performance tests were conducted:

- Load Test
- Stress Test
- Spike Test

The purpose of these tests is to evaluate:

- System responsiveness
- Maximum handling capacity
- Stability under heavy traffic
- Recovery capability after sudden traffic spikes

**2.0 Tool Selection Justification**

**2.1 Locust**

[Locust Official Website](https://locust.io/?utm_source=chatgpt.com)

Locust was selected because it is a lightweight and powerful open-source performance testing tool written in Python. It allows testers to simulate thousands of concurrent users with customizable behaviors.

**Reasons for Choosing Locust**

- Easy to install and configure
- Python-based scripting makes test scenarios flexible
- Real-time monitoring dashboard
- Supports distributed load testing
- Suitable for Load, Stress, and Spike testing
- Generates performance metrics such as:
    - Requests Per Second (RPS)
    - Response Time
    - Failures
    - Number of Users

**2.2 OWASP Juice Shop**

OWASP Juice Shop was selected because it is a free and open-source web application security testing tool. It can inspect HTTP traffic and identify security vulnerabilities while monitoring application requests.

**Reasons for Choosing OWASP Juice Shop**

- Open-source and widely used
- Supports proxy interception
- Helps monitor HTTP requests during testing
- Useful for identifying security weaknesses
- Integrates well with browser and testing environments

**3.0 Setup Procedure**

The testing environment uses Linux operating system.

**A. Install Juice Shop using Docker**

Step 1: Install Docker

If Docker isn’t installed:

sudo apt update

sudo apt install docker.io

sudo systemctl enable --now docker

Step 2: Pull Juice Shop image

sudo docker pull bkimminich/juice-shop

Step 3: Run Juice Shop

sudo docker run -d --name juice -p 3000:3000 bkimminich/juice-shop

Step 4: Verify it’s running

Open your browser:

http://localhost:3000

**B. Install Locust**

**1\. Install required packages**

sudo apt update  
sudo apt install python3-venv -y

**2\. Create a virtual environment**

Go to your project folder first:

mkdir locust-project  
cd locust-project

Create venv:

python3 -m venv venv

**3\. Activate the virtual environment**

source venv/bin/activate

After activation, your terminal should look like:

(venv) username@OS:~/locust-project$

**4\. Install Locust**

Now install normally:

pip install locust

**5\. Verify installation**

locust --version

You should see something like:

locust 2.x.x

**Run Locust**

Create a simple test file:

nano locustfile.py

Paste this:

from locust import HttpUser, task, between  
<br/>class WebsiteUser(HttpUser):  
wait_time = between(1, 3)  
<br/>@task  
def home(self):  
self.client.get("/")

Save:

- CTRL + O
- ENTER
- CTRL + X

Start Locust:

locust -H https://192.168.100.22:3000

Then open browser:

http://localhost:8089

**4.0 LOAD Test**

Load testing is performed to evaluate how the application behaves under expected normal traffic conditions. The objective is to ensure the system can maintain stable performance during regular usage.

**Test Configuration**

| **Parameter** | **Value** |
| --- | --- |
| Users | 50  |
| Spawn Rate | 5 users/sec |
| Duration | 5 minutes |

**  
Result/Outcome**

- Stable response time
- Minimal failures
- Consistent request handling
- Smooth system operation under normal load

**5.0 STRESS Test**

Stress testing is conducted to determine the maximum limit of the system by gradually increasing traffic beyond normal operating capacity.

The purpose is to observe:

- System degradation
- Performance bottlenecks
- Failure points
- Recovery capability

**Test Configuration**

| **Parameter** | **Value** |
| --- | --- |
| Users | 500 |
| Spawn Rate | 50 users/sec |
| Duration | 10 minutes |

**Result/Outcome**

- Increased response time
- Possible request failures
- System slowdown under heavy load
- Identification of maximum handling capacity

**6.0 SPIKE Test**

Spike testing evaluates how the application reacts to sudden and extreme increases in traffic within a short period.

This test determines whether the system can:

- Handle sudden traffic surges
- Maintain availability
- Recover after traffic returns to normal

**Test Configuration**

| **Stage** | **Users** |     |
| --- | --- |     |
| Normal Traffic |     | 10  |
| Sudden Spike |     | 1000 |
| Recovery |     | 10  |

**Result/Outcome**

- Temporary increase in response time
- Possible failures during spike
- Recovery after traffic decreases

**7.0 Result**

The performance testing results contain three major graphs:

**A. Total Requests per Second (RPS)**

The green line represents Requests Per Second (RPS), while the red line represents failures.

**Observation**

- During Run #1, the traffic was low and stable.
- During Run #2, the system handled approximately 150–220 requests per second consistently.
- During Run #3, the traffic fluctuated heavily due to the spike test scenario.
- Small failure spikes appeared during high traffic periods.

**Analysis**

The application was able to process requests efficiently during normal and moderate load conditions. However, during sudden spikes and high concurrency, request consistency decreased and failures began to appear.

**B. Response Times (ms)**

The purple line shows the 95th percentile response time, while the yellow line shows average response time.

**Observation**

- Response times remained low during Run #1 and Run #2.
- During Run #3, response times increased significantly.
- The 95th percentile response time reached extremely high values during traffic spikes.

**Analysis**

The results indicate that the server performance degraded under extreme load conditions. High response times suggest server resource exhaustion, processing delays, or network bottlenecks.

**C. Number of Users**

The blue line represents concurrent users.

**Observation**

- Run #1 maintained low user traffic.
- Run #2 maintained approximately 500 users steadily.
- Run #3 showed rapid increase up to around 1000 users before decreasing gradually.

**Analysis**

The graph confirms that the spike test successfully simulated sudden traffic increases. The system experienced instability when concurrent users increased rapidly.

**Overall Performance Interpretation**

| **Test Type** | **Result** |
| --- | --- |
| Load Test | Stable and acceptable |
| Stress Test | Performance degradation observed |
| Spike Test | System instability during sudden traffic surge |

**8.0 Conclusion**

The performance testing successfully evaluated the application under different traffic conditions using Locust and OWASP ZAP.

The Load Test showed that the system can handle normal user traffic with stable response times and minimal failures. During the Stress Test, the application experienced slower response times and performance degradation as the number of users increased significantly. In the Spike Test, sudden traffic surges caused instability and high latency, indicating that the server has limitations when handling abrupt increases in concurrent users.

Overall, the testing demonstrates that the system performs adequately under normal operating conditions but requires optimization for handling very high traffic loads and sudden spikes. Improvements such as server scaling, database optimization, caching mechanisms, and load balancing are recommended to improve system stability and performance under extreme conditions.
