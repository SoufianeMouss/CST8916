# Assignment 2: Cloud Service Providers Comparison Report

## **1. Executive Summary**
As organizations increasingly adopt cloud technologies to handle their data engineering needs, selecting the right cloud platform becomes critical. Amazon Web Services (AWS), Microsoft Azure, and Google Cloud Platform (GCP) are three leading players in the cloud market, each offering robust and diverse services 
such as remote data access and real-time applications. 
These capabilities are increasingly critical for modern systems such as IoT platforms, live dashboards, streaming pipelines, and interactive web applications. The goal of this report is to evaluate how each cloud provider enables RESTful APIs, GraphQL, WebSockets, data streaming, and real-time analytics, and to identify the most suitable platform for different real-world scenarios.
The analysis shows that AWS offers the most mature and comprehensive suite of real-time and event-driven services, particularly through Amazon API Gateway, AppSync, Kinesis, and Kinesis Data Analytics. Azure provides strong enterprise-ready tooling with robust integration features and managed services such as Azure API Management, Web PubSub, Event Hubs, and Stream Analytics, making it an excellent choice for organizations already invested in the Microsoft ecosystem. GCP stands out with its highly scalable and developer friendly services—especially Pub/Sub and Dataflow, but lacks native GraphQL support and has fewer out of the box real-time communication tools compared to AWS and Azure.

## **2. Introduction**
As modern systems increasingly rely on low-latency communication, event-driven processing, and continuous data streaming, understanding how each cloud provider supports these capabilities is essential for selecting the right platform. This comparison evaluates the strengths, limitations, and architectural differences across several categories, including RESTful APIs, GraphQL services, WebSockets, data streaming, and real-time analytics.

This analysis focuses on the three leading cloud providers, each offering a broad ecosystem of managed services:

* **Amazon Web Services (AWS):** The largest and most mature cloud platform, known for its wide range of services, strong event-driven architecture tools, and high flexibility across application types.
* **Microsoft Azure:** A cloud platform tightly integrated with Microsoft’s enterprise tools and ecosystem, providing strong capabilities in identity, integration, and data analytics, particularly for organizations using existing Microsoft technologies.
* **Google Cloud Platform (GCP):** A developer-centric cloud provider emphasizing high scalability, strong data processing capabilities, and efficient real-time streaming services, backed by Google’s expertise in distributed systems.

## **3. Service Comparison**
In this section we compare AWS, Azure, and GCP across five key categories relevant to remote data and real-time applications: RESTful APIs, GraphQL services, WebSocket communication, data streaming, and stream analytics. Each subsection highlights equivalent services, architectural differences, scalability considerations, and pricing models

### **3.1 RESTful API Services**

| Feature        | AWS                                    | Azure                                      | GCP                                          |
| -------------- | -------------------------------------- | ------------------------------------------ | -------------------------------------------- |
| Main Service   | Amazon API Gateway                     | Azure API Management                       | Google Cloud API Gateway                     |
| Deployment     | Fully managed                          | Fully managed, includes policies           | Managed + Cloud Endpoints                    |
| Authentication | IAM, Cognito, Lambda auth              | OAuth2, AD, Managed Identity               | IAM, OpenAPI                                 |
| Pricing Model  | Per million requests + data transfer   | Fixed tier + per-call                      | Per million requests                         |
| Strengths      | Mature, integrates with Lambda easily  | Strong policy engine & enterprise features | Simple, lightweight, great for microservices |
| Weaknesses     | Pricing can stack in high-traffic apps | More complex setup for beginners           | Fewer features than AWS/APIM                 |

AWS offers the most mature API gateway. Azure provides deep enterprise policy control. GCP focuses on simplicity and speed.


### **3.2 GraphQL Services**

| Feature             | AWS                        | Azure                         | GCP                         |
| ------------------- | -------------------------- | ----------------------------- | --------------------------- |
| Native GraphQL      | **Yes (AWS AppSync)**      | **No native service**         | **No native service**       |
| Third-Party Options | Apollo, Hasura             | Apollo, Hasura, App Service   | Apollo, Hasura on Cloud Run |
| Real-Time           | Subscriptions (WebSockets) | Requires external integration | Supported via Cloud Run     |
| Ease of Setup       | Very easy                  | Moderate                      | Moderate                    |

AWS is the clear leader because AppSync is fully managed, supports resolvers, caching, and subscriptions. Azure and GCP require external GraphQL solutions.


### **3.3 WebSocket Services**

| Feature          | AWS                       | Azure                              | GCP                   |
| ---------------- | ------------------------- | ---------------------------------- | --------------------- |
| Service          | API Gateway WebSocket API | Azure Web PubSub                   | Cloud Run WebSockets  |
| Supports Pub/Sub | Yes, via Lambda           | Yes, built-in                      | Through Pub/Sub       |
| Scalability      | High, auto-scaling        | High, optimized for real-time apps | Good, container-based |
| Use Cases        | Chat apps, notifications  | Multiplayer apps, dashboards       | Custom WebSocket apps |


Azure Web PubSub is specifically optimized for high-scale real-time apps; AWS is flexible; GCP requires building around Cloud Run.

### **3.4 Data Streaming Services**

| Feature       | AWS             | Azure                       | GCP                           |
| ------------- | --------------- | --------------------------- | ----------------------------- |
| Main Service  | Amazon Kinesis  | Azure Event Hubs            | Google Pub/Sub                |
| Throughput    | Very high       | Very high                   | Extremely high (Google-scale) |
| Latency       | Low             | Low                         | Very low                      |
| Integration   | Lambda, S3, EMR | Functions, Stream Analytics | Dataflow, BigQuery            |
| Pricing Model | Per shard       | Per throughput unit         | Per message volume            |


GCP Pub/Sub offers the best global scaling, AWS Kinesis has the richest ecosystem, Azure Event Hubs is optimal for enterprise pipelines.

### **3.5 Stream Analytics**

| Feature              | AWS                                    | Azure                  | GCP                           |
| -------------------- | -------------------------------------- | ---------------------- | ----------------------------- |
| Service              | Kinesis Data Analytics / Managed Flink | Azure Stream Analytics | Dataflow (Apache Beam)        |
| Real-Time Processing | Yes                                    | Yes                    | Yes                           |
| Complexity           | Medium                                 | Low                    | High (Beam model)             |
| Integration          | Kinesis ecosystem                      | Event Hub, IoT Hub     | Pub/Sub, BigQuery             |
| Strengths            | Flexible, Flink support                | Easiest to use         | Extremely powerful & scalable |

We can conclude that Azure Stream Analytics is the easiest for simple real-time queries. GCP Dataflow is the most powerful. AWS provides deep control through Apache Flink.


## **4. Use Case Analysis**
### Use Case: Real-Time Financial Trading and Intraday Risk Management
**Scenario:**
In modern capital markets, trading activity moves far too quickly for end-of-day risk assessment to remain effective. Market exposure can shift in milliseconds, as seen during crises like the Bear Stearns collapse in 2008. To remain competitive and financially secure, banks and financial institutions are shifting toward **intraday Value at Risk (VaR)** calculations that continuously update based on market conditions and live portfolio changes. This requires ingesting real-time market data streams, recalculating risk exposure instantly, and triggering automated responses to mitigate volatility.

Streaming analytics plays a critical role in this transformation. A real-time analytics platform can continuously listen to market price feeds, monitor portfolio movements, and compute risk metrics on the fly. This provides traders with a low-latency, high-performance system capable of identifying threats earlier, reducing exposure to sudden market swings, and enabling smarter, data-driven decision-making. The architecture demands ultra-fast message ingestion, time-series analysis pipelines, and highly scalable compute resources that can process large volumes of data with minimal delay.

Based on the scenario above the suitable cloud provider for our case will be Amazon Web Services, because it performs more in the following: 

* **Ultra-low-latency streaming ingestion:** Amazon Kinesis is optimized for high-throughput financial data streams and can reliably process millions of events per second.
* **Real-time analytics capabilities:** Kinesis Data Analytics (Managed Apache Flink) supports fast, stateful event processing ideal for continuous VaR calculations.
* **Event-driven architecture:** AWS Lambda and Step Functions enable automated risk responses based on real-time market triggers.
* **High-performance computing options:** AWS offers scalable EC2 compute fleets, including HPC instances suitable for complex financial risk models.
* **Enterprise-grade security and compliance:** AWS provides advanced IAM, encryption, audit controls, and compliance frameworks required in banking.
* **Global reliability:** Financial institutions benefit from AWS’s global infrastructure, multi-region redundancy, and low-latency connectivity.

Overall, AWS is the strongest choice for real-time financial trading analytics due to its mature event-driven ecosystem, HPC capabilities, and robust streaming analytics services.
### Use Case: Real-Time Predictive Maintenance for Industrial Equipment
Here is your **Predictive Maintenance** use case rewritten cleanly, expanded to fit academic requirements, and optimized specifically as a **strong Azure use case**.

**Scenario:**
In industrial environments, unexpected equipment failures can result in costly downtime, production delays, and safety risks. Predictive maintenance addresses this challenge by continuously analyzing real-time data from sensors embedded in machinery. These sensors stream information such as temperature, vibration, pressure, and motor current to the cloud. By processing this data instantly, organizations can detect anomalies early and anticipate mechanical failures before they occur. This enables proactive maintenance scheduling, reduced operational costs, and improved equipment reliability.

A predictive maintenance system requires a real-time data ingestion pipeline, scalable analytics, and machine learning capabilities to identify patterns associated with equipment degradation. It must also integrate seamlessly with enterprise systems used by maintenance teams and provide intuitive dashboards for monitoring equipment health.

Based on the scenario above, the most suitable cloud provider for this use case is Microsoft Azure, as it outweighs the alternatives in the following areas:

* **Specialized IoT services:** Azure IoT Hub provides secure, bi-directional communication with industrial sensors and machinery, enabling seamless ingestion of IoT telemetry at scale.
* **Stream analytics optimized for anomaly detection:** Azure Stream Analytics can evaluate sensor data in real time using SQL-like queries, making it ideal for detecting irregular patterns or deviations.
* **Built-in industrial analytics tools:** Azure Digital Twins and Time Series Insights offer deep contextual modeling and historical trend analysis for equipment behavior.
* **Strong machine learning integration:** Azure Machine Learning enables training, deploying, and updating predictive models directly from streaming data.
* **Enterprise integration:** Azure naturally connects with on-premises systems, Active Directory, and enterprise resource management tools often used in industrial environments.
* **Scalability and reliability:** Azure supports high-throughput IoT deployments with low-latency processing, ensuring predictions are made in time for corrective action.

In general, Azure provides a complete end to end ecosystem specifically built for industrial IoT and real-time predictive maintenance, making it the most suitable platform for this scenario.

## **5. Conclusion**
Choosing the right cloud platform for real-time applications depends on factors such as latency requirements, scalability needs, existing system architecture, and the level of integration required across services. AWS, Azure, and GCP all provide strong real-time processing, messaging, and analytics capabilities, but each platform offers distinct advantages. AWS excels with its mature event-driven ecosystem and highly scalable real-time streaming tools. Azure is strongest in enterprise environments, offering seamless integration with IoT devices, analytics platforms, and on-premises systems. GCP, on the other hand, is known for its low-latency global infrastructure and industry-leading streaming analytics and machine learning tools, making it ideal for high-volume, data-intensive real-time workloads.

## **6. References**
- https://www.geeksforgeeks.org/data-engineering/data-engineering-in-the-cloud-comparing-aws-azure-and-google-cloud-platform/
- https://www.datacamp.com/blog/aws-vs-azure-vs-gcp
- https://callminer.com/blog/25-use-cases-and-examples-of-real-time-analytics
- https://www.instaclustr.com/education/real-time-streaming/real-time-data-streaming-4-use-cases-5-components-and-6-best-practices/

## AI Usage Disclosure
AI was used for rewriting ideas from the websites and organizing this README file.
Also, it was used for the comparison.