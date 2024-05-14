### Overview 

#### Why should we use rate limiters?
Rate limiting is used to control the rate of incoming requests or data flow in a system. It plays a crucial role in maintaining the stability, performance, and security of applications and services. 
- Protect Against Overload
- Ensure Fair Resource Allocation
- Prevent Abuse and DoS Attacks
- Improve Application Performance
- Manage API Usage
- Monetization and Billing
- Compliance and Legal Requirements
- Optimize Resource Utilization

#### Pros & Cons & Use cases

| Type | Pros | Cons | Use cases |
|---|---|---|---|
| Fixed Window Rate Limiting | - Simple to implement and understand.<br>- Straightforward for enforcing a specific number of requests per fixed time interval. | - Can lead to uneven distribution of requests when a new window starts.<br>- Clients might experience wait times until the next window starts if the limit is reached. | Use Case: API Rate Limiting<br>Scenario: You have a public API, and you want to enforce a fixed number of requests per minute/hour/day to prevent abuse and ensure fair usage among different API consumers. |
| Sliding Window Rate Limiting | - Smoother distribution of requests over time compared to fixed window rate limiting.<br>- More flexibility in managing request bursts. | - Slightly more complex to implement than fixed window rate limiting | Use Case: Real-Time Data Ingestion<br>Scenario: You have a high-traffic data ingestion system that needs to process data in real-time. Sliding window rate limiting allows you to smoothly control the flow of incoming data while handling bursts during peak times. |
| Token Bucket Algorithm | - Allows bursts of requests while maintaining the long-term rate limit.<br>- Provides a straightforward implementation using tokens and buckets. | - Can require fine-tuning the token refill rate and bucket size to achieve the desired behavior.<br>- Potential inconsistency when the bucket is full and requests are delayed.-  | Use Case: Video Streaming<br>Scenario: In a video streaming service, you want to allow users to watch videos at different rates based on their subscription plans. The token bucket algorithm can control the number of video streams a user can access concurrently. |
| Leaky Bucket Algorithm | - Smoother request distribution compared to the token bucket algorithm.<br>- More straightforward to implement than token bucket algorithm. | - Requires a slightly more complex implementation than fixed window rate limiting. | Use Case: Payment Gateway<br>Scenario: In a payment gateway system, you want to limit the number of requests per second from a merchant to prevent potential denial-of-service attacks or accidental high-volume requests. |
| Distributed Rate Limiting | - Ensures rate limiting across all nodes in a distributed system, preventing individual server-based bypasses.<br>- Allows for more accurate enforcement of rate limits in distributed environments. | - Can introduce additional complexity when coordinating rate limits across nodes. | Use Case: Microservices Architecture<br>Scenario: In a microservices-based system, you want to ensure that a single client's requests are rate-limited consistently across all microservices, preventing one service from being overwhelmed by a specific client. |
| Adaptive Rate Limiting | - Dynamically adjusts rate limits based on real-time conditions and client behavior.<br>- Can optimize for different situations and adapt to changing traffic patterns. | - Can be more complex to implement and require additional monitoring and feedback mechanisms. | Use Case: Application with Varying Traffic Patterns<br>Scenario: In an application with varying traffic throughout the day or during special events, adaptive rate limiting can dynamically adjust rate limits to optimize performance and prevent overload during <br>peak times. |

#### Sample Rate Limiting
- Simple Rate Limiting using Redis, Nodejs
    https://github.com/duyvu997/rate-limiter