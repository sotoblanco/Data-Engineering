## Week 3: Data architecture

Definition: the design of systems **to support change in an enterprise**, achieved by flexible and reversible decisions reached through a careful evaluation of trade-offs

![image](https://github.com/user-attachments/assets/46a76537-fa10-4954-9710-d0987148cbc0)

The data architecture falls in the domain of enterprise architecture. 

The decision making approach have two type of decision, one-way door and two-way door. One way door do not allow to undo the decision while two-way door decision does allow to change

![image](https://github.com/user-attachments/assets/1836c7f5-0b9b-46cc-9c1b-973c242bde24)

Taking this as example we can select S3 standard in AWS and change our mind to S3 glacier later depending on our requirements.

### Principles of Good data architecture

![image](https://github.com/user-attachments/assets/700393ec-22ee-4f80-a495-e3d4123fb297)

Choose common componentes wisely

An example of those components are:

- Object storage
- Version control systems
- Observability & monitoring systems
- Processing engines

Choosing systems that reflects the team goal is key

![image](https://github.com/user-attachments/assets/2531a746-22ea-4d36-a01c-143348bfe7e2)

### When your systems fail

Plan for failure: practical and quantity approach

System metrics: 

- Availability: percentage of time an IT service or a component is expected to be in an operable state
    
![image](https://github.com/user-attachments/assets/ea8cd83f-338f-4da9-adba-63d9ee7b9433)
    
- Reliability: The probability of a particular service or component performing as intended function during a particular time interval
- Durability: The ability of a storage system to withstand data loss due to hardware failure, software errors, or natural disasters.

Prioritize security: create authentication for every action that requires access to sensitive data

Summary: To serve the needs of your organization you most plan for failure, as it is almost certain that things will go wrong at some point, having a plan in place will make the difference in the trust of your clients. This plan for failure takes into account four components:

- Availability, reliability and durability the system requirements will help in the prioritization of this three
- Security: requires to have a system that is not prone to vulnerability such as zero-trust approach that every action of sensitive data requires authentication. RTO: RPO
- RTO and RPO are important concepts in the plan for failure which helps to define the acceptable error

### Batch architectures

![image](https://github.com/user-attachments/assets/9db9e83e-f3e2-4efd-8697-b120984f4b93)

This can be the principle of ELT extracting and loading data in batches and transform your data to serve in downstream use cases.

Choose common components: if you have several end use cases you can choose common components to make your pipeline efficient.

Plan for failure

Make reversible decision: build flexibility in your system

Embrace finops: cost-benefit in your analysis

Summary: Batch processing: is a type of data ingestion that helps to serve data in block rather than one-by-one this approach is the most common in the data systems, it can be view as the first step in the ELT pipeline, when building those type of system remember to choose common components, plan for failure, make reversible decision and embrace finops. 

### Streaming architetures

All data can be categorize as a continuos stream of events. Batch data waits for accumulation of data points in series of chunks. In stream data pipeline you get the data after is produce

![image](https://github.com/user-attachments/assets/7db4f4df-f3a0-460f-ae5c-2134971fdcd6)

This is how it works:

1. Event producer: Data source. This is the event that produce the data can be clicks or sense of a device
2. Streaming broker: Which coordinates the data between producer and consumer
3. Event consumer: can be a service or application that process the data. Data lake or data warehouse
4. Downstream use cases data analytics or ML 

- **Lambda architecture**: This separates batch and streaming systems but combines their outputs in a serving layer, though it has challenges like managing different systems and codebases.
    
![image](https://github.com/user-attachments/assets/fa17d8d6-b9d6-4499-95cf-f322df6ab207)
    
- **Kappa architecture**: Proposed as an alternative, this uses stream processing as the backbone for all data handling, facilitating real-time responses and allowing for batch processing via replaying historical data. However, Kappa never gained widespread adoption.
    
![image](https://github.com/user-attachments/assets/df4480fe-cdc8-4df5-887e-d4406f95cd5c)
    

Today, technologies like **Google's Dataflow model** and **Apache Beam** aim to unify batch and streaming processing by treating all data as event streams, simplifying code. Tools like **Apache Flink** are popular for stream processing, and the philosophy of batch as a subset of streaming is more prevalent in modern architectures.

The text also emphasizes the importance of designing systems for flexibility, scalability, and compliance with regulations and organizational policies.

### Architecting for compliance

Even when we might not want to spent much time on this, it is critical to at least know that this exits and it can be a cause of system failure.

- GDPR: European regulation: Do not track and identify people and be willing to delete data if customer wants.
- HIPAA: Health insurance portability and accountability act: for health care industry
- Sarbanes oxley act in the U.S

### Summary

## Choosing the right technologies

There are many choices when it comes to select the right tool, it is important to keep in mind the end goal of your system which is **deliver high-quality data products**

The Data architecture is the what, why and when and the tools is the how

Let’s evaluate the considerations we need to make:

1. Location: On-premises, cloud or hybrid
2. Cost optimization: Build vs buy
3. Team sizes and capabilities

Monolith vs modular systems

**Monolith** has all components of an application in a single systems creating interdependency between each other, if one of them breaks the other one will break as well. There are some advantages:

- Easy to reason about and to understand
- Deal with one technology

But it is hard to maintain

**Modular creates separate components that handle different parts of the system avoiding problems when updating one piece of the software**

- Interoperability

**Cost optimization**

**Total cost of ownership (TCO):** The total estimated cost of a solution, project or initiative over its entire lifecycle.

**Direct cost:** Easy to identify cost, directly attributed to the development of a data product

- Salaries
- Cloud bills
- Software subscriptions

**Indirect cost:** Expenses that are not directly attributed to the development of a data product.

- Network downtime
- IT support
- Loss of productivity

**Capital expenses:** The payment made to purchase long-term fixed assets (on-premises)

**Operational expenses:** Expense associated with running the day-to-day operations (cloud)

**Total opportunity cost of ownership (TOCO):** The total cost of lost opportunities that you incur in choosing a particular tool or technology. You might choose the best combination of options available, but as this evolve you will have components that are not the best because a new tool might come out. In this situation you need to build flexible components that allow to change between tools which help to minimize the TOCO

### Build vs buy

Build vs buy is crucial decision node to take, and involves the business needs to make the decision.

The benefits of building vs buying are:

- Get exactly the solution you need
- Avoid licensing fees
- Avoid being at the mercy of a vendor

This is often not the recommended approach, usually you do want to build on existing solutions:

- Open-source
- Commercial open source
- Proprietary Non open-source

![image](https://github.com/user-attachments/assets/1dd6e2eb-9fca-4fa0-9160-08c5e71bf795)

### Server, Container, and serverless compute options

To host your software applications you need a server, which is essentially a computer, working on the cloud you have options that you can choose from depending on your needs

![image](https://github.com/user-attachments/assets/6017a007-6b55-460e-b008-b7f3cb2327f1)

Serverless option might work well as it allows to have an environment that doesn’t require to set-up or maintain the server, and you can focus on the application.

- **Servers**: You manage everything, including the operating system, networking, scaling, and security (e.g., Amazon EC2).
- **Containers**: A more modular solution, containers package your code and dependencies in a lightweight unit, but you still manage some setup aspects. Unlike servers, the underlying OS and networking are provided.
- **Serverless**: Although the term implies no server, the server is managed behind the scenes. Serverless abstracts the server management from the user, enabling automatic scaling, availability, and cost-efficiency with pay-as-you-go billing (e.g., AWS Lambda). This is ideal for simple, discrete tasks, though not suitable for applications with high compute or memory demands.

![image](https://github.com/user-attachments/assets/3008988d-f5e4-4b0f-8d11-05c8a9bb08b1)

**Decision Considerations:**

- **Control vs. Abstraction**: If you need full control (security, OS, networking), choose **servers**. For more abstraction and ease of use, choose **containers** or **serverless**.
- **Scalability**: **Serverless** solutions are ideal for auto-scaling based on events or usage spikes. For more complex scaling needs, like managing microservices, go with **containers**.
- **Cost**: **Serverless** is cost-effective for applications with low or irregular workloads since you only pay when the code runs. **Servers** can be more cost-efficient for high, constant workloads.
- **Complexity**: For simple, isolated tasks, **serverless** is ideal. For more complex applications with many dependencies or services, **containers** provide better orchestration options.

Serverless and containerize tools are good for most data engineering task, so you can start building there and scale up as you need more resource.

Questions:

1. When is better to use serverless options?
    1. Simple & discrete task
    2. Complex & discrete task
    3. You should always use serveless options
    4. Only if you have a single task
2. The term serverless refers to:
    1. There is no server
    2. The server is manage by other applications you need to build
    3. The server is managed behind the scenes
3. You are working for a start-up that wants to build a chatbot to answer questions to the customers, they have the prototype and wants to test to small portion of users, they hire you to provide the best option for them, what would be your suggestion to host the application?
    
    R: When you're rapidly prototyping or building a lightweight app (e.g., a chatbot, a simple web API), serverless provides scalability and cost-efficiency without the need for upfront infrastructure management.  

### How the undercurrents impact your decisions

In this section we evaluate how the six undercurrents we discuss previously affect how we make decisions in our data engineering pipeline.

**Security**: What are the security features of the tool? Use tools from reputable sources

**Data management**: How are data governance practices implement by the tool provider? This means to evaluate data breach, compliance with regulatory issues and data quality

**DataOps**: What features does the tool offer in terms of automation and monitoring?

**Data architecture**: Does the tool provide modularity and interoperability?

**Orchestration**: What tools are using? there are options such as apache airflow and prefect to say the most popular ones. 

**Software engineering**: How much do you want to do? this means evaluate your teams capabilities and business value, this lead to answer if you want to build or buy 

## Investigating your architecture on AWS

### Intro to the AWS Well-architecture framework

Set of principles and best practices that help you build:

**scalable and robust** architectures on AWS

The AWS well-architected consist on 6 pillars that allows to evaluate your architecture

![image](https://github.com/user-attachments/assets/7ed61568-f588-4daa-baf9-083075e83532)

This six principles do not imply a template to follow, instead there are set of principles and questions that help to design and operate reliable, secure , efficient, cost-effective, and sustainable systems in the cloud. This helps you to think the pros and cons of different architecture choices.

Lens: are extensions of the AWS well-architected framework that focuses on a particular area, industry, or technology stack and provide guidance that’s specific to those context

## Lab

![image](https://github.com/user-attachments/assets/aa775dcb-b3f4-48c1-ac20-0b40a40d9247)

This our architecture which is a pipeline to ingest, transform, and serve to the data analyst of the company, in this week we want to serve embedded dashboards to clients and share analytics data through third-party data sharing platforms. Our goal is to ensure that the web app is:

- Capable of scaling to meet the clients' needs
- Uses computing resources efficiently
- Designed in a secure and reliable way

We would be using AWS cloudwatch by following the principles of good architecture and the AWS well-architected framework

![image](https://github.com/user-attachments/assets/21206d8a-3b99-4443-a064-4ea0e8b999bd)

Let’s evaluate the Logic tier

We have two instance in different availability zone to ensure the reliability of the application, this instance can increase as needed.

How is the web application created? A typical way of deploying web application solutions is to use a [three-tier-architecture](https://docs.aws.amazon.com/whitepapers/latest/serverless-multi-tier-architectures-api-gateway-lambda/three-tier-architecture-overview.html) that consists of three tiers or layers:

- **Presentation tier**: this tier represents the user interface of the website (ex.: a web page) that allows clients to interact with the web application using their devices. This is where you can display the analytical dashboards for clients.
- **Logic tier**: this tier, also known as the application tier, represents the business logic that processes clients' input, queries the internal data stores and returns the results that need to be displayed on the presentation layer.
- **Data tier**: this tier is where the data associated with the web application is stored.

Here the three-tier architecture of your web application is given to you, and you’ll mainly interact with the computing resources on which the application logic is run. Here’s the architectural diagram of the web application:

![image](https://github.com/user-attachments/assets/efff2565-4320-428a-8d38-0bdad58b4711)

On the left side we have the S3 bucket which represents the data tier, on the right side users interact with the application through their devices. The other two main components are **Application Load Balancer (ALB)** and **Auto Scaling group** which both operate at the application layer:

- [Amazon EC2 Auto Scaling group](https://docs.aws.amazon.com/autoscaling/ec2/userguide/what-is-amazon-ec2-auto-scaling.html): this group consists of a collection of EC2 instances. What is an EC2 instance? This is the application server on which your application logic runs. It mainly consists of Central Processing Unit (CPU) and Random Access Memory (RAM). Think of EC2 as a computer that is provided by AWS on which you will run your code. Now why do you have more than one EC2? Each EC2 runs the same logic and they are used to increase the computing capabilities of your application. So instead of having a single EC2 that processes all inputs or requests from clients, these inputs are distributed across the EC2 instances. **Auto-scaling** means that the number of EC2 instances can increase or decrease based on the demand. In this case it is the client’s inputs or requests to the web app.
- [Application Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/userguide/what-is-load-balancing.html): The Auto Scaling group is associated with an application load balancer, which distributes incoming application traffic (clients requests’ or inputs) across the EC2 instances. The load balancer serves as the single point of contact for clients.

The VPC (virtual private cloud) is a way to isolate your resources from the outside world. There is no communication with the internet outside of the VPC. Inside your VPC you may need some resources to be public and others to be private. You can create a **public subnet** if you want to allow for outside traffic to access your resources, and you can create a **private subnet** if you don’t want to allow for outside traffic to access your resources.

Task:

### Load Balancers

1. The architecture of the web application is implemented and provided to you in this lab. Your first task is to get the address of your web application. To do so, you need to find the ALB, since it serves as the single point of contact for clients.
2. Go to EC2 in AWS and find Load Balancers copy the DNS name and paste the name in a new tab

![image](https://github.com/user-attachments/assets/a7786827-2cca-4662-9815-7e06c3a176a2)

1. The web page should display a dashboard for clients, but for brevity and simplicity's sake, you are shown a simple message. Don't worry about the details of this message, you will explore them in a later section of this lab. By having opened the webpage, you sent an HTTP request to the ALB. The HTTP request reached the ALB through port 80, which is the [default port](https://www.techopedia.com/definition/15709/port-80#:~:text=To%20make%20it%20convenient%20for,Port%2080%20should%20be%20used) for HTTP requests (if you don’t know what port means, check [here](https://www.cloudflare.com/learning/network-layer/what-is-a-computer-port/)).

In the next sections, you will learn how to monitor the computing and networking activity of your web app and you will ensure that the principles of “good” data architecture are in place. In particular, you will configure your architecture to embrace the following principles: “Prioritize security”, “Plan for failure” , and “Architect for scalability”.

### **Monitoring CPU Usage and Networking Activity**

When you share your web app with your clients, you should expect some incoming traffic to your application that needs to be processed. To ensure that your application can support the incoming demands, you would need to monitor the usage of computing resources of your web-app. To do so, you can use Amazon CloudWatch, which is the monitoring and observability service in AWS that enables you to collect and track computing and memory metrics for your web app.

Monitoring the usage of computing resources of your web-app is one of the practices of the undercurrent DataOps and the Operational Excellence pillar of [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/?wa-lens-whitepapers.sort-by=item.additionalFields.sortDate&wa-lens-whitepapers.sort-order=desc&wa-guidance-whitepapers.sort-by=item.additionalFields.sortDate&wa-guidance-whitepapers.sort-order=desc). These practices emphasize the importance of integrating automation, monitoring of systems, and adaptability into the design of cloud workloads. These practices enable your understanding of your workloads and their anticipated behaviors.

In this section, you are going to perform some stress tests to simulate traffic to your website and then monitor CPU usage and networking activity using Amazon CloudWatch.

4.1. To perform stress tests over your current architecture, you will use an open-source benchmarking tool called [Apache Benchmark](https://httpd.apache.org/docs/2.4/programs/ab.html). This tool is used to test the ability of a website to handle a large number of HTTP requests at the same time.

1. Go to cloudshell this allow to interact with your AWS resource and install the Apache Benchmark `sudo yum install httpd-tools -y`
2. Perform the stress test by typing in the cloudshell: 

`ab -n 7000 -c 50 http://<ALB-DNS>/`

Make sure you add the `/` path at the end of it. The options used in the command are used for the following purposes:

- `<ALB-DNS>` represents the DNS name you found in previous step
- Option `n` corresponds to the total number of requests that will be sent to the HTTP server.
- Option `c` corresponds to the number of concurrent (simultaneous) requests that will be done.

Q: Which resource is a browser-based shell that makes it easier to securely manage, explore, and interact with your AWS resources.

- AWS CloudShell (Correct)
- EC2 instance
- Apache Benchmark
- AWS CloudWatch

1. Go to auto scaling groups (EC2 feature) and go to the monitoring page of the created for you

### **Enhancing Security**

Now that you know how to monitor the computing resources of your application, it’s time for you to delve into the security aspect of your servers. Security should always be your priority as stated in the principle “prioritize security”. Also, the security pillar provides insights into how to leverage cloud technologies to secure data, systems, and assets, and to protect them from unauthorized access.

You were told that through port 90 of the ALB some private data is displayed, but only certain people inside your company should have access to it. In this section, you will fix this issue so that any inbound traffic is only allowed to go through port 80. In particular, you will work with adjusting the **security groups** of the ALB, which is a tool that acts as a virtual firewall, controlling inbound and outbound traffic through the ALB.

5.1. Take the `DNS Name` of your ALB and paste it into your browser search bar pointing to the port 90, as follows:

```
<ALB-DNS>:90
```

Through this port, you see a message that mimics the display of some private data. You are surprised given the security requirements that should have been implemented, so you decide to fix it now.

5.2. In the AWS console, again you search for **EC2** and then click on **Security Groups** in the left panel.

You will see a list of security groups, out of which you will work with the following ones:

- `de-c1w3-ec2-sg`: This is the security group of your EC2 instances (servers).
- `de-c1w3-alb-sg`: This is the security group of the Load Balancer.

5.3. Click on the id for the security group with the name `de-c1w3-ec2-sg`. In the **Inbound Rules** section, you will find the following rule:

- Rule with `Type: All TCP`, `Port range: 0-65535` and as source a security group id. This source is the security group of the ALB. The purpose of this security group is to ensure that servers will only receive traffic from the ALB.

5.4. Go back and click on the ID for the `de-c1w3-alb-sg` security group. Check the **Inbound Rules** to find the following rule:

- Rule with `Type: All TCP`, `Port range: 0-65535` and `Source: 0.0.0.0/0` (which means all IP addresses). This rule means that any source can access the ALB using any port, which is quite open and insecure!

5.5. Now, click on **Edit inbound rules** and delete the current rule. Then, add a new rule with the following properties:

- `Port range: 80`
- `Source: 0.0.0.0/0`

![image](https://github.com/user-attachments/assets/d34cc497-90a2-4506-810e-511871b305c8)

So now although all the internet can have access to your ALB, the traffic is only allowed through port 80, so if you go back to your browser and point to port 90 (`<ALB-DNS>:90`) you should not have access to it.

*Note*: You may still see a display of the website previously accessed through port 90 and stored in a cache. But if you refresh the webpage, it will not load.

To check if the rule was properly created, in your browser, point to port 80 (by default you can only put `<ALB-DNS>` on your browser search bar) and see if you can see the Dashboard message.

By configuring security groups, you restricted access to sensitive data presented on port 90 of the ALB to authorized personnel within the company. This was done to improve the system's overall security, following the guidelines of the AWS Well-Architected Framework's Security pillar and the principle of “Prioritize security”.

Q: What resource would you use if you want to allow outside traffic inside a Virtual Private Cloud?

- Application Load Balancer
- Public subnet (Correct)
- Private subnet
- Auto scaling group

In the inbound rules of the ALB security group What this rule means `Type: All TCP`, `Port range: 0-65535` and `Source: 0.0.0.0/0` (which means all IP addresses)?

- any source can access the ALB using any port (correct)
- You can only access to ALB using port 80
- Only the IP address can access to the ALB
- Only source from the EC2 can access to the ALB

In the inbound rules of the EC2 security group the source is a security group ID, what’s the purpose of this rule?

- To provide access to any source in the correct port
- To ensure that servers will only receive traffic from the ALB (Correct)
- Avoid typing all possible IP address you want to provide access
- To limit traffic in port 80

What principle relies on having multiple availability zones?

- Plan for failure
- Architect for scalability
- Prioritize security

### **Checking EC2 Availability**

If you check the given architecture of the web application, you notice that each EC2 instance belongs to a different **Availability Zone (AZ)**. Availability Zones are isolated data centers, each with independent power, cooling, and networking infrastructure. Designing applications to span multiple AZs enhances their fault tolerance and resilience, and provides a foundation for highly available systems. This cloud practice is related to the reliability pillar of cloud-based solutions, as well as to the principle of “Plan for failure”.

Multi-AZ deployments in AWS offer businesses a robust solution to mitigate the impact of potential failures. By distributing application components across different AZs, organizations can achieve high availability and fault tolerance. In the event of an outage or disruption in one AZ, traffic is automatically routed to healthy instances in other AZs, ensuring uninterrupted service delivery. This architectural approach minimizes downtime, enhances performance, and contributes to a seamless user experience.

### **Performing Auto Scaling**

### 7.1 - Using Resources Efficiently

The current instances are of type `t3.micro` (*t* is the family of the instance, *3* is the generation and micro represents the size of the EC2 instance). You noticed that those instances can be a bit overpowered for your infrastructure, so after reading a bit more about the [instance types](https://aws.amazon.com/ec2/instance-types/t3/) you decided to scale them down (reduce the size) and use a more suitable `t3.nano` instance. To scale the instances, you need to modify the way they are created inside the **Auto Scaling Group**, which can be done through the **Launch templates**.

7.1.1. In the AWS console, search for **EC2** service and find the **Auto Scaling Groups** section in the left panel. Select the Auto Scaling group provided to you.

7.1.2. In the **Details** tab find the **Launch template** section and click on **Edit**.

7.1.3. Find a **Version** dropdown and below a link to `Create a new launch template version` (below it). This will open a page to create a new version of the template.

7.1.4. Make sure that the checkbox **Provide guidance to help me set up a template that I can use with EC2 Auto Scaling** is **unchecked**:

In the **Instance type** section choose the `t3.nano` instance type:

Then, click on Create template version

7.1.5. Go back to your Auto Scaling group and then to **Details** > **Launch template** > **Edit**. In the **Version** drop-down, now you can select the Latest option and click on Update button at the bottom of the page.

7.1.6. Now, you need to terminate the instances so the new instances that will be launched will be of the instance type just defined. In the **EC2** service, go to **Instances** and select the two that are currently running under the name of `de-c1w3-asg`. Right-click on any of them and click on **Terminate instance**.

Given that the Auto Scaling group has a desired capacity of 2 instances, after some minutes the new instances (with the `t3.nano` instance type) should start running again. Refresh the UI every minute until it appears as running. Before moving to the next section of the lab, wait until the newly created instances have instance state `Running`.

**Performing Auto Scaling**

7.2.1. The EC2 instances in your Auto Scaling group can increase or decrease in number depending on the demand. With Auto Scaling group, you only pay for what you use. When demand decreases, AWS Auto Scaling will automatically remove any extra EC2 so you avoid overspending.

Currently, Auto Scaling is not enabled, so the Auto Scaling group will not be able to scale up or down. To enable Auto Scaling, you will need to create a scaling policy where you need to specify metrics and threshold values that invoke the scaling process.

In the AWS console, go back to **Auto Scaling Groups** section under the **EC2** service, choose your Auto Scaling group and click on the **Automatic scaling** tab.

7.2.2. Under **Dynamic scaling policies** section, click on **Create dynamic scaling policy**.

7.2.3. Create a new policy with the following properties:

- Policy type: `Target tracking scaling`
- Scaling policy name: `de-c1w3-scaling-policy`
- Metric type: `Application Load Balancer request count per target`
- Target group: `de-c1w3-ec2-tg-port80`
- Target value: `60`
- Instance warmup: `60` seconds

The meaning of those values are:

- As the Metric type is a request count per target, with a target value of 60, it means that when the HTTP (port 80) request count goes above 60 (value chosen just for the sake of simplicity in this lab), the Auto Scaling group may scale out to add more instances to handle the increased load. If the request count per target drops below 60, the Auto Scaling group will scale in by reducing the number of instances to save costs and maintain efficiency.
- A warm-up time refers to a period during which newly launched instances are allowed to receive traffic and fully initialize before being considered in-service for the Auto Scaling evaluation metrics. During the warm-up time, the Auto Scaling group monitors the health and status of the instances to ensure they are ready to handle the production workload. For the sake of simplicity in this lab, you set this value to 60 seconds, but the AWS default is 300 seconds (5 minutes).

7.2.4. Perform a more intense test with Apache Benchmark to test the scaling policy that was created. Go to **CloudShell** and run the following command (replace `ALB-DNS` with the `DNS Name` of your ALB):

```
ab -n 1000000 -c 200 http://<ALB-DNS>/
```

This test should run for some minutes, in the meantime, you can monitor your instances. Go back to the **Auto Scaling Groups** service in the AWS console and click on **Monitoring** and then on **EC2** to watch the CPU and Network metrics again. After some time (about 5 min) when those metrics start increasing, you can switch to the **Activity** tab and you will see some notifications regarding additional instances being launched to handle the traffic through the 80 port.

After the stress test finishes, you can continue monitoring the metrics and the **Activity** tab to see when the metrics go down again and even the launched instances are terminated. Take into account that there is some delay in the metrics plots in the **Monitoring** tab after you start the test. You can re-run the command for the test if you want to maintain the stress for more time.

## Summary

![image](https://github.com/user-attachments/assets/6194304d-f15f-4070-8d7d-bc5cf70a7c95)
