# Course 4: **Data Modeling, Transformation, and Serving**

# Data modeling Part 1

## Week 1: Introduction to Data Modeling for Analytics

### Week 1 overview

Intuition: We want to get data in ways that can be analyse and use for different use case, that’s where data model comes in to play.

Data model: A data model organizes and standardizes data in precise structured representation to enable and guide human and machine behaviour, inform decision-making, and facilitate actions. 

Let’s break down this definition:

**Define the structure, relationships and meaning of data**: 

- What tables make up the model
- How the tables relate to one another
- What columns to choose for each table

**Structure the data in a way that connects back to the organization**:

Data is understandable & valuable → Human → if the goal is analytics

Data that is meaningful → Machine → if the goal is machine learning

![image](https://github.com/user-attachments/assets/a5f6c24b-c060-4b01-9983-2041d9227d55)

In the previous week we built a mental model on how to think about a data engineer, we understand the DE lifecycle from ingest, transform and serve and then we prepare the principle sof good data architecture.

![image](https://github.com/user-attachments/assets/e7307503-6143-4ed2-a279-17d9535e3943)

In this week we complete the mental model in which we go back to get the requirements, choose the technology and tools and implement in AWS. 

## Requirements

![image](https://github.com/user-attachments/assets/120b7aa9-4387-47a2-bd2f-5e4f4c73bbdd)

When getting the requirements you need to think about it as a hierarchy of needs. From business goals that accounts for what does success look like, stakeholder needs and system requirements.

## Conversation with CTO

The conversation is between a new data engineer and a Chief Technology Officer (CTO) at an e-commerce company, discussing business goals, challenges, and technology initiatives. Key points include:

1. **Business Challenges**:
    - Competition from smaller brands eroding market share.
    - Old legacy systems inherited from before the company became an e-commerce platform could cause costly outages, posing a risk to the brand.
2. **Technology Initiatives**:
    - **Refactoring code** to replace legacy systems, reduce risks, and improve scalability.
    - **Expanding market share** by introducing new product lines and international operations.
    - Moving from batch-based processing to **streaming technologies** like AWS Kinesis and Kafka.
3. **Role of Data Engineering**:
    - Collaborate with software teams to ensure data produced by refactored systems is analytics-friendly, minimizing post-processing needs.
    - Build expertise in Kinesis and Kafka by developing proof of concepts and supporting streaming data pipelines.
    - Support development of a **recommendation engine** by building data pipelines to process customer behavior data and product taxonomy, in collaboration with data scientists.
4. **Focus on Customer Retention**:
    - Modernizing the site to improve responsiveness and prevent downtime.
    - Creating better data infrastructure to enhance customer experience through personalized recommendations.

The CTO emphasizes teamwork and continuous learning, encouraging the new hire to grow their streaming capabilities and play a vital role in the company's technological transformation.

## Conversation with marketing

### **Summary:**

The text presents a conversation between a data engineer and a product marketing manager, focusing on gathering requirements for two initiatives: dashboards with product sales metrics and a product recommendation system. The engineer uses this interaction to clarify the current state of these projects, identify pain points, and understand the marketing team’s goals for improvement. Key takeaways include:

- **Dashboards**: The current dashboards are functional but show a 2-day lag in data. The marketing team wants real-time insights to capture short-term trends and react quickly with targeted promotions.
- **Recommendation System**: The existing recommendation system is based on weekly popular products, but the team aims to personalize recommendations based on a customer’s behavior and cart contents, similar to leading e-commerce platforms.

The data engineer commits to refining the systems to meet these requirements and anticipates following up with more questions during development.

---

### **Techniques for Requirement Gathering:**

1. **Understanding Current Systems and Issues**:
    - Asked about the existing dashboards and recommender system to assess their functionality and limitations.
    - Identified the data lag problem in the dashboards that prevents timely promotional actions.
2. **Clarifying Stakeholder Goals and Actions**:
    - Explored how the marketing team wants to leverage real-time data to act on product demand spikes.
    - Inquired about the typical duration and characteristics of demand spikes to better design real-time dashboards.
3. **Validating Requirements through Scenario Testing**:
    - Used hypothetical scenarios (e.g., 1-hour data lag) to confirm that such improvements would meet stakeholder needs.
4. **Exploring Future Plans and Dependencies**:
    - Confirmed that the team wants personalized recommendations based on customer behavior, not just general product popularity.
5. **Identifying Additional Conversations**:
    - Mentioned consulting with data scientists and other teams to ensure alignment and gather more detailed technical requirements.

The key elements of requirement gathering

- Learn what existing data systems or solutions are in place
- Learn what pain points or problems there are with the existing solutions
- Learn what actions stakeholders plan to take based on the data your serve them
- Identify any other stakeholders you’ll need to talk to if you’re still missing information

## Breaking down the conversation with marketing

![image](https://github.com/user-attachments/assets/99f3993c-5174-4b01-8eb2-dd37387536eb)

## Conversation with the Software engineer

![image](https://github.com/user-attachments/assets/6de0d380-1a30-4b14-b3fc-0f007a02ac00)

Learn about existing data systems or solutions

- Usually the might be at early stages with a rudimentary work that delivers data to data scientist

Discuss the pain points or problems there are with the existing solutions

- Data scientist teams needs more continuous access to what they are trying to do, this problem might be related to a lack of system that avoid corruptions to the database, so they might provide files to be downloaded daily.
- Schema changes
- Discuss the stability of the database

Evaluate thoughs on how to solve existing issues

- Replica of database (can this mitigate the issues?)

## Documenting non-functional requirements

This was the requirements and potential solution discussed in the conversations with the software engineer

![image](https://github.com/user-attachments/assets/ab54e9bc-2dd2-4ead-ac3e-4a81b041f4e3)

This is the process in which we broken-down the business goals, the stakeholders needs and the system requirement.

We have two functional requirement, one for the analytic dashboard and the other for the recommender system. 

### Analytics dashboard

![image](https://github.com/user-attachments/assets/3ce65385-7e4e-4425-815f-a02a755f8a62)

### Recommender system

## Summary

![image](https://github.com/user-attachments/assets/f17ae1f0-5370-4a0b-a16f-52f0e4297bf5)

![image](https://github.com/user-attachments/assets/52b746b0-40f0-4126-8771-cc142751825f)

The iron triangle allows to evaluate your projects, in which you have a timeline, the scope of the project and the cost.

![image](https://github.com/user-attachments/assets/047545b1-3e96-4699-810b-aaaec6a0c09e)

# Translating requirements to architecture

## Requirements gathering exercise

![image](https://github.com/user-attachments/assets/4cb1d6ca-1bb6-4e80-b7c0-feb9ef59d082)

The get the data in tabular format for the recommender system, they want to retrain with new batch of data to see how often they might need to retrain

How the model will be use in production

Input → Output (milliseconds)

Takeaways from conversation

> I take a set of features containing information about each product and then also a set of features containing information about each user. I then compute a vector embedding for each user and each product and look for similarities between these embeddings in order to make product recommendations to users. So the model takes user and product features as inputs and generates a list of product ids as output.
> 

> I’d like to try next is retraining the model based on a fresh batch of data to see how stable it is and try to get a sense of how often we might want to retrain and update the model in deployment.
> 

> the training data I’m using is in tabular format. Each row contains data for a single product purchase, where the columns include  a collection of user features, which are: “customer number”, “credit limit", "city", “postal code”, and "country". And then there’s also a set of product features, including “product code”, "quantity in stock", "buy price”, "msrp", "product line", and "product scale". In addition to these user and product features, there is a rating value from 1 to 5 that represents the user’s rating of that product.
> 

> I will plan to monitor the model’s output. In fact, it would be great if, in addition to serving recommendations on the platform, all the model output could be automatically saved for later analysis. And then I would plan to retrain the model if I notice any drift in performance or change in the input data. So, I guess I might want to retrain the model as frequently as once a week, but it might be less than that, like monthly or quarterly.
> 

> we would like to be able to present recommended products to the user more or less instantaneously as they are browsing through different products or during the checkout process. It usually takes a new page a second or two to render so if the recommender could work that fast it would be great.
> 

> the company currently has around 100k customers in the database, meaning that many individual customers have bought at least one item, and many of them are repeat shoppers. We’re expecting that number to grow as the company expands to new regions and product lines. So, right now, it varies a lot. Sometimes there are only a few people shopping on the platform but we can see activity spikes of up to 10k users on the platform at the same time and we could see more in the future.
> 

Recommender system that takes input from the user and items and provide a list a products

Need retrain to see the stability of the model

Tabular format data

Saved model’s output to for later analysis

Provide output instantaneously

Scale up to 10k at the same time

## Conversation takeaways
Here are the key takeaways from this conversation. You are tasked with building two data pipelines:

- A batch data pipeline that serves training data for the data scientists to train the recommender system;
- A streaming data pipeline that provides the top product recommendations to users based on their online activity. The streaming data pipeline makes use of the trained recommender system to provide the recommendations.

The recommendation system will recommend products to customers based on their user information and based on the products the customer has been browsing or that are in their cart.

**Notes:**

- The lab focuses on providing an end-to-end data pipeline example. Your main tasks will be to interact with the components of the batch and streaming pipelines.
- The lab does not focus on fine tuning the performance of the recommender model. Moreover the data that is used is the same one used in week 2, and may not contain good predictive user and product features. The goal of the lab is not to assess the performance of the recommender problem but to incorporate its computations inside the streaming pipeline.
- The recommendation model will compute two vectors -- the product embedding vector and the user embedding vector. It will then generate product recommendations based on these vectors. The product embedding is a vector that holds information about product characteristics, and the user embedding is a vector that holds information about user preferences for each of the product characteristics represented in the product embedding vector. To learn more about vector embeddings and how the recommendation system works, feel free to check out the next optional reading item.

![image](https://github.com/user-attachments/assets/96c082a6-1177-49e6-8c69-85438cbda76e)

Batch pipeline

Functional requirements

Feed the system for the train pipeline with batch of data for retrain once a week

Non functional requirements

- Latency once a week
- Scalability starting with 10k users

Stream pipeline

Functional requirements

milisecond data that display the recommendation based on the users activity and products

Nonfunctional requirements

- Latency: miliseconds
- Scale starting with 10k users

### Feedback

Feedback

**Functional requirements**

When thinking about the functional requirements of the data pipeline, consider the tasks the pipeline needs to perform (i.e. what data it needs to ingest or combine, how it should process it, and what data it needs to serve).

In this case, the data pipeline needs to serve data in a format that is suitable for training the machine learning model as shown in the figure below (i.e. tabular and containing the columns specified)

Although not explicitly discussed in the conversation, other common considerations around functional requirements that are usually discussed for machine learning models include:

- The duration the data pipeline should retain or store the training data.
- How the data pipeline should combine the old with the new dataset. Should the old dataset be discarded? If the same customer updated their rating for a given product, should you keep the last rating or compute the average?
- The file format the training data should be served in. (e.g. CSV, Parquet, etc.)

**Nonfunctional requirements**

Nonfunctional requirements are attributes or characteristics of the data pipeline that allow it to successfully meet stakeholder needs. The data scientist mentioned that they’d like to retrain the model as soon as they notice any drift in performance or change in the input data, meaning that the data pipeline needs to perform a simple transformation task only when it is needed. So, it must not require too much operational overhead to deliver the new training set.

Although not explicitly discussed in the conversation, another common consideration around nonfunctional requirements is the cost of implementing the batch pipeline. You generally want to build a cost effective pipeline.

**Here's a table that summarizes these requirements:**

| **Functional Requirements** | **Nonfunctional Requirements** |
| --- | --- |
| Provide the training data for the content-based recommender model in the following format:
• Tabular data 
• Each row in the table contains the following user and item features: “customer number”, “credit limit", "city", “postal code”, and “country”, “product code”, "quantity in stock", "buy price”, "msrp", "product line", "product scale", “product rating”. | • The data system must be easy to maintain and update, and requires less operational overhead (Irregular / on demand run schedule)
• The data system must be cost effective. |

Feedback

**Functional requirements**

The streaming data pipeline has to do the following:

- use the recommender system to find the set of products to recommend for a given user based on the user’s information and the products they interacted with online.
- stream the products to the sales platform and store them for later analysis.

**Nonfunctional requirements**

- Latency: The system should provide the recommended products to the user instantaneously as they are browsing through different products or during the checkout process. For a given user, the system must be able to ingest and extract user and product data, provide them to the recommender system, and finally serve the product recommendations to the sales platform, all in a few seconds.
- Scalability & concurrency: The system must be able to scale up to ingest, transform and serve the data volume expected with the maximum level of user activity on the platform, while staying within the latency requirements.

## AWS Services for Batch pipelines

![image](https://github.com/user-attachments/assets/72f8f360-6e6d-4245-b43a-5482cc491a00)

In our system batch pipeline seems like a good fit. We’ll get data from AWS RDS that runs on a EC2 instance, we extract the data, transform and load to serve our data team in tabular format. 

We need to decide the infrastructure we need, between serverless, container and server, when possible we should go with serverless options.

![image](https://github.com/user-attachments/assets/0cc0357c-e354-4e8c-85b7-f2f60b81f9d2)

Let’s evaluate lambda AWS, lambda has their limitations, for instance:

- There is a 15-minute timeout for each function call
- Memory and CPU allocation for each function
- Requires you to write custom code for your use case

**Serverless options tools for batch processing**

Ingestion and transformation portion of your pipelines on AWS

![image](https://github.com/user-attachments/assets/0e680ef0-4838-4ece-9973-9d664ebe51e5)

- Extra explanation between EMR and GLUE ETL
    
    ---
    
    ## **Comparison: Glue ETL vs. EMR Serverless**
    
    | Aspect | AWS Glue ETL | Amazon EMR Serverless |
    | --- | --- | --- |
    | **Purpose** | Simplified ETL and data integration | Big data analytics with control |
    | **Frameworks Supported** | Spark | Spark, Hadoop, Presto, Hive |
    | **Ease of Use** | Easy with a visual interface | Requires configuration expertise |
    | **Scalability** | Automatic scaling | User-configured scaling |
    | **Infrastructure Management** | Fully managed | Partially managed |
    | **Cost Model** | Pay per job | Pay per resource usage |
    | **Use Case Fit** | ETL pipelines, Data Lakes | Large-scale analytics, Custom frameworks |
    | **Performance Optimization** | Limited | Full control over optimization |
    
    ---
    
    ## **Which One Should You Choose?**
    
    - **Choose AWS Glue ETL** if:
        - You need a quick, simple solution to build **ETL pipelines**.
        - Your workload relies on **Spark** and doesn’t require significant customization.
        - You prefer a **fully managed, low-maintenance** option that integrates well with other AWS services.
    - **Choose Amazon EMR Serverless** if:
        - Your use case involves **large-scale analytics** or **non-Spark** frameworks.
        - You need more **control over resources and configuration** to optimize performance.
        - You have **specialized workloads** that require custom components or external libraries.
    
    ---
    
### Conclusion:

AWS Glue ETL and Amazon EMR Serverless both serve batch processing needs, but their strengths lie in different areas. **Glue ETL** excels at **convenience and simplicity**, making it ideal for smaller ETL pipelines or data lakes. **EMR Serverless** provides **greater flexibility and control**, making it the better choice for **complex, large-scale analytics**. Your choice will depend on the specific requirements of your project, such as the frameworks needed, performance goals, and the level of control you require.

The choose of the tools for load and serve portion of the pipeline depends on the downstream use-case. If you have normalize tabular data you can modelled into star schema for analytics, one option you could choose will be store in AWS RDS. If you want to run complex analytical queries on massive dataset you could choose store the data in AWS redshift.

![image](https://github.com/user-attachments/assets/18b52440-4081-433d-94d8-94d964988e31)

### AWS Services for streaming pipelines

![image](https://github.com/user-attachments/assets/f2558a79-3ae2-41ca-a62a-90068d05256c)

The streaming data can be from many different sources, we can ingest this data with an EC2 instance using scripts, then transform the data and send it to downstream where it need to go. This approach means you’re responsible for installing software, managing security, and managing cloud deployment complexity. 

Stream data can be significantly more complex than batch data, which means you shouldn’t built your own solution unless you’re 100% that it cannot be solve by existing solutions. 

### Amazong Kinesis

Amazon kinesis data stream is a popular solution to manage stream data, it gets data from different sources and store it, the minimun retention time is 24 hours but it can be increase as you needed. It’s also data agnostic, which means it can get data from any format.

![image](https://github.com/user-attachments/assets/0aeabb25-6ddc-4dda-a97f-78fbedfe9560)

### Amazon MSK

![image](https://github.com/user-attachments/assets/c08acfba-4afa-46b9-9786-3ad1f0ffdb6e)

Another popular option is Amazon Managed Streaming for Apache Kafka (Amazon MSK), it use the same principle but this time with apache kafka which is an open source tool that allow to manage stream data. MSK makes easy to run and built application that use apache kafka to process stream data. It works by:

1. Create an apache kafka cluster: MSK takes care of provisioning and operating the nodes that runs kafka
2. You interact with the kafka data plane that MSK manages for you to create topics, produce and consume data
3. Data producer and consumers connect to the cluster to send and receive messages

![image](https://github.com/user-attachments/assets/edc6785b-74d4-4766-a18d-4437b305cc31)

The choose between Amazon MSK and kinesis depends on the use case, as general rule MSK offers more control while kinesis is more convenient.

### Amazon Data firehouse

Amazon data firehouse solves the problem on having to write custom code to store the data coming from kinesis data stream and it allows to move to storage such as S3 or Redshift  

![image](https://github.com/user-attachments/assets/b5e5bd6d-9114-4e8c-b2bc-a4ccf97f4cee)


