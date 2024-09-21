## Week 1: Introduction to Data Engineering

If you land a job at small or even some mid-size companies as data scientist usually you can find that some of them wants data solution without data, making a data science job impossible without building a good infrastructure and architecture to work in the first place, many data engineers came from a data science background in which instead of doing actual data science job they had to move around and adapt to the organization needs and build the data system. 

This course is meant to prepare you for a data engineering role, however many job description for Data scientist or Machine Learning Engineering describe a lot of tools used in this course as a requirement for the job. Having this set of tools and the knowledge of a data engineer not only will help you in your application but it will also help you in your daily job.

In the first week, is all about think like a data engineer, which is the first step in the roadmap to become a senior level engineer.

Let’s start by defining what data engineering is:

Data engineering is the development, implementation, and maintenance of systems and processes that take in raw data and produce high-quality, consistent information that supports downstream use cases, such as analysis and machine learning. Data engineering is the intersection of security, data management, DataOps, data architecture, orchestration, and software engineering.

![image](https://github.com/user-attachments/assets/3d42d668-d7a2-47c9-a7eb-ec0e401168fc)

When you build your data pipeline the goal is to support downstream use cases which will be used by stakeholder, those can be from wide variety of knowledge and needs, for example, we can have analysts, data scientist, machine learning engineers, salespeople among other that required our data. 

To serve this requirement there are some questions that we need to have a clear understanding before delivering data. 

- How often do they need to retrieve each query?
- What information do you need to retrieve in each query? →  With this, you could be thinking about whether there are certain joins between data tables or other aggregations that would be helpful for you to run ahead of their queries to make things run faster for them.
- How much latency they can tolerate in their metrics? →  Like is it acceptable to be looking at data that is an hour old or a day old? Or do they need something closer to real time?

In addition to Upstream stakeholders are those people responsible for the development maintenance of the source systems you ingest raw data from. Your upstream stakeholders are often the software engineers who build the source system you're working with. And these might be software engineers within your company, or they could be the developers responsible for a third-party source you're ingesting data from.

![image](https://github.com/user-attachments/assets/7239b970-cd92-4ac9-8f8e-44c2845e73bf)

Let’s talk about how to bring value to the company or people that you work, the business value depends on many factors, the most straightforward way is to increase revenue, however this won’t always be the case at least in direct way. There are common path for you as data engineer delivering value to the organization, which is understand the requirements at different levels.

![image](https://github.com/user-attachments/assets/2f0cdcb9-4eb2-44e1-9c52-c3f48fc312d1)

As we can see the requirements came from different levels and this is a critical thing to understand in the first week of our work, with a intuitive sense based on the interview process we took. The faster you get this information the better will be. 

**Functional requirements**: **What** system needs to be able to do

- Provide regular updates to a database
- Alert a user about an anomaly in the data

**Non-functional requirements**: **How** the system accomplishes what it needs to do

- Technical specifications of an ingestion or orchestration or storage approach
- How you’ll meet the end user’s needs

![image](https://github.com/user-attachments/assets/cf492539-543a-4326-a199-dcc80cf6ce38)

You first week requires to gather the requirements of your company, usually this information came from stakeholders, but they won’t provide the requirements in terms of data engineer, instead they have high level goals and needs and your first job is to translate into requirements for your system. 

The requirement gathering step also should incorporate audience understanding, this help to achieve goals and reach a high level of satisfaction for everyone involve. Understand how business operates is key for data engineers to help you when you are engineering you’re building towards the operation of the business. 

How your first week as data person looks like?

The first week of a data person in any role starts with business understanding, you need to gather the requirements of your system from downstream stakeholders (the ones that receive your end product and use in their operation) however they usually have high level goals and requirements, your first job is to translate this into system requirements, you also need to get as much information as possible about the business and end user to understand how the business operates. 

## Requirements gathering

To get the best information on your first week you need to understand the business and people working on it. There is a masterclass that can help you to develop this skill, I highly recommend you to evaluate this information. 

[MasterClass | Chris Voss Teaches the Art of Negotiation](https://www.masterclass.com/classes/chris-voss-teaches-the-art-of-negotiation)

The conversation start by providing a goal/requirement from the marketing team and addressing a problem of a data analyst point of view:

Goal: Real time analysis of product sales by region

Methdology: Get information from production database, manually having to pull the data (software engineering team → you might break something)

Problem: Getting a lot information that they don’t need → 90% of the time navigating through data that is not needed cause delays in the workflow

Marketing needs real time → updates provided within 2 days

As the software engineering team is providing data once a day and the data processing takes a lot of time and many time the scripts to clean the data crash due to unexpected formats

Now, we move to understand the marketing team needs, most of us stop at understand the data requirements, but going beyond and understand the downstream user for this data analyst helps to understand the real needs

### Key elements of requirements gathering

💽 Learn what existing data systems or solution are in place

⚠️ Learn what pain points or problems there are with the existing solutions

🎯 Learn what actions stakeholders plan to take with the data (tip: repeat what you leaned back to your stakeholders)

🩺 Identify any other stakeholder you’ll need to talk if you’re still missing information

**Conversation with Data scientist**

- Marketing needs real-time analysis of product sales, but I am only getting daily data dump from the software team
- Problems with schema changes and other anomalies in the data →
    - Build in automatic checks on the ingested data
    - Know about changes or disruptions before they happen
- Lots of data cleaning and processing
- Marketing needs data in real-time

*Real-time means different things for different people. You can apply a key tactic by asking: What action they plan to take with the data?

Conversation with Source owners

- What’s a better ingestion solution?
- What kind of disruptions or changes can I expect
- How can I anticipate these changes?

Functional requirement

- Ingest, transform, & serve data in the format required

Non-functional requirement

- Make data available some time after it is recorded

## Thinking like a data engineer

![image](https://github.com/user-attachments/assets/eca680e6-0ec1-440b-933f-e199b6326a34)

This is actually a cycle in which you iterate over each step several times as you are working in a team.

## Data engineering on the cloud: AWS

There are 5 different categories of resources that you can use

### Compute

Compute: Amazon Elastic Compute Cloud (EC2) → Virtual machines: computers or severs where you can run any OS and applications. Besides EC2 there are other services that you can run such as AWS lambda → run code based on triggers or events. Amazon elastic container service (ECS) and Amazon Elastic Kubernets Service (EKS)

### Network

Amazon virtual private network: private network you can create and place resources into.

![image](https://github.com/user-attachments/assets/dd7a4a48-a562-4ed5-a9b6-ac136b1742d2)

### Storage

There are three main types of storage to be aware off. 

- Object storage: Most often used for storing unstructured data (Amazon Simple Storage Service (S3))
- Block storage: Used for database storage, virtual machine file systems, and other low-latency environment: Amazon Elastic Block Store (EBS)
- File storage: Data is organized into files and directories in a hierarchical structure: Amazon Elastic File System (EFS)

### Databases

This is a form of storage but it provides some other functionalities to work on

- Amazon Relational Database Service (RDS): A cloud relational database service
- Amazon Redshift: A data warehouse service that allows you store, transform, and serve data for end use cases
