Towards MultiCloud
==================

Cloud 101
---------

Google Cloud Deletes a Billion-Dollar Pension Fund
--------------------------------------------------

In 2024, Google Cloud accidentally deleted the entire private cloud account of **UniSuper** an Australian pension fund managing $135 billion for over 647,000 members. For days, members couldn’t access their accounts. The fund only recovered because some backups existed _outside_ of Google Cloud.

That story stuck with me.

Not because Google messed up (every provider has incidents), but because it exposed a fundamental assumption: that redundancy within a single provider is always enough. Zones and regions protect you from hardware failures and natural disasters. They don’t protect you from a provider-level misconfiguration wiping your account.

Amazon’s AI-Assisted Code Breaks Its Own Shopping Platform
----------------------------------------------------------

Then in early 2026, Amazon’s retail platform suffered multiple high-severity outages in a single week. During one incident, users couldn’t check out, access account information, or view product prices for roughly six hours. Internal documents indicated that “GenAI-assisted changes” were a factor in a trend of incidents dating back to Q3 2025.

The context makes it worse. Amazon had cut approximately 30,000 corporate roles across late 2025 and early 2026 citing AI as the reason for “reducing roles” while simultaneously pushing remaining engineers toward AI-assisted development. Reports emerged that engineers felt pressured to ship AI-generated code faster, with fewer humans reviewing it. Amazon’s internal AI coding assistant was implicated in at least one incident where it provided inaccurate advice based on an outdated internal wiki.

Amazon disputed much of the reporting, stating it was “user error, not AI error.” But the outcome was the same: the world’s largest e-commerce platform broke for its customers, repeatedly, in a compressed timeframe. Dave Treadwell, Amazon’s SVP of eCommerce Foundation, acknowledged that “best practices and safeguards” around generative AI hadn’t been fully established and announced a 90-day safety reset requiring senior engineer sign-off on AI-assisted code changes.

The Lesson for Multicloud
-------------------------

These two stories from two different providers, two different failure modes illustrate the same point: **no single provider is immune to catastrophic failure, and the causes are getting harder to predict.**

Google’s failure was **operational:** _an account deletion_.

Amazon’s was **systemic:** _organizational pressure + immature AI tooling + reduced human oversight._

Neither was a traditional infrastructure outage that zones and regions would have caught. Both would have been survivable with workloads distributed across providers.

That’s what pushed me to take multicloud seriously _and, of course_ to write this **101-post series** documenting the journey.

So What Is Multicloud?
----------------------

Multicloud means running your workloads across two or more cloud providers. That’s it. You might run your primary application on AWS, your analytics on GCP’s BigQuery, and your identity layer on Azure’s Entra ID. Or you might mirror critical services across two providers for resilience.

It’s not about using every service from every provider. It’s about choosing the right tool from the right provider for each job and not being trapped if one of them has a bad day.

Multicloud vs. Hybrid Cloud
---------------------------

These terms get used interchangeably, but they mean different things:

### **Hybrid Cloud**

_Hybrid Cloud_ means combining private infrastructure (on-premises or private cloud) with public cloud. One organization, two deployment models working together.

### **Multicloud**

_Multicloud_ is all about using multiple public cloud providers. One organization, multiple vendors.

You can have both.

A company running on-prem servers connected to AWS (hybrid) while also using GCP for data analytics (multicloud) is doing hybrid multicloud.

Why Bother With MultiCloud Architecture?
----------------------------------------

### **Resilience Beyond A Single Provider.**

The UniSuper deletion and Amazon’s AI-induced outages are extreme cases, but even partial outages (an AWS region going down, an Azure AD issue blocking logins) can cripple a business that’s all-in on one platform. As providers increasingly rely on AI tooling internally, the risk of novel, unpredictable failure modes only grows.

### **Use Each Provider’s Strengths.**

GCP’s BigQuery is exceptional for analytics. AWS has the broadest service catalog. Azure integrates deeply with Microsoft enterprise tooling. Multicloud lets you pick winners instead of settling for “good enough” across the board.

### **Avoid Vendor Lock-In.**

The more dependent you are on proprietary services, the harder it is to negotiate pricing, switch providers, or adapt when a service gets deprecated or when a provider’s internal decisions (like mass layoffs affecting engineering quality) start impacting reliability. Multicloud keeps your options open.

### **Cost Optimization.**

Egress fees, reserved instance pricing, and spot/preemptible instance availability vary across providers. Strategic placement of workloads can reduce your bill especially for data-heavy pipelines where storing data in one cloud and processing it in another can make financial sense.

### **Compliance And Data Residency.**

Some regulations require data to stay in specific regions. Not every provider has data centers everywhere. Multicloud gives you geographic flexibility.

The Real Challenges of A MultiCloud System
------------------------------------------

I’m not going to pretend this is free. Multicloud adds complexity:

### **Operational Overhead.**

Three consoles, three billing systems, three sets of IAM policies, three CLI tools. Your team needs broader skills.

### **Networking Complexity.**

Cross-cloud communication means managing VPN tunnels, peering, or dedicated interconnects between providers. Latency and egress costs add up.

### **Inconsistent Tooling.**

Each provider names things differently, structures APIs differently, and updates on different cycles. What’s “an instance” in one is “a VM” in another.

### **Security Surface Area.**

More providers means more attack surface, more credentials to manage, and more places where a misconfiguration can expose data.

### **Cost Visibility.**

Tracking spend across providers requires unified tooling. Native dashboards won’t give you the full picture.

Multicloud isn’t a default recommendation. It’s a deliberate architectural decision that should be driven by specific business requirements — not hype.

The Three Providers in This Series
----------------------------------

### **Amazon Web Services (AWS)**

My primary cloud. Broadest service catalog, most mature ecosystem, largest community. It’s where I’m most comfortable, and honestly, its depth of services means you can go a long time before _needing_ another provider. My posts will often frame things from an AWS-first perspective. Yes, I’m featuring their outage story above and still recommending them. That’s the point. Every provider has risks. The answer isn’t to avoid AWS, it’s to not put all your eggs in one basket.

### **Microsoft Azure**

Strong enterprise play, especially if your organization already lives in the Microsoft ecosystem (Active Directory, Office 365, Teams). Its hybrid story with Azure Arc is compelling, and Entra ID is a serious identity platform.

### **Google Cloud Platform (GCP)**

Fewer services than AWS, but what it does, it often does exceptionally well. BigQuery, GKE, and its networking layer are genuinely best-in-class. Also the birthplace of Kubernetes, which matters for container-heavy architectures. And yes, they deleted a pension fund’s accountm but they’re also the only provider whose Kubernetes offering consistently benchmarks fastest.

What This Series Covers
-----------------------

Over 101 posts, we’ll walk through cloud fundamentals such as compute, storage, networking, security, serverless, containers, and more with theory followed by hands-on implementation across all three providers. The goal isn’t to make you an expert in all three. It’s to make you _comfortable_ in all three, so you can make informed decisions about where to run what.

Each topic follows a pattern:

### **1. Theory Post**

The concept, why it matters, how it works generally

### **2. AWS Post**

Hands-on implementation in AWS

### **3. GCP Post**

Hands-on implementation in GCP

### **4. Azure Post**

hands-on implementation in Azure

_Some topics also include cross-cloud posts covering federation, multi-cloud tooling, or comparative analysis._

Who This Is For
---------------

*   Developers who know one cloud and want to _understand_ the others
*   Engineers _evaluating multicloud_ for their organization
*   Anyone preparing for **cloud certifications** across _multiple providers_
*   People who watched a pension fund get deleted and an e-commerce giant break itself with AI, and thought “maybe I should have a backup plan”

Concluding Remarks
------------------

The cloud isn’t going anywhere. But blind trust in a single provider should.

Google deleted a pension fund. Amazon’s own AI tooling broke its own shopping platform. These aren’t hypothetical risks from a whitepaper. They happened to two of the most technically capable organizations on the planet, running their own infrastructure.

The point of this series isn’t to scare you off the cloud. It’s the opposite.

The cloud is incredible, and each provider brings something genuinely valuable to the table. The point is that spreading your knowledge (and eventually your workloads) across providers isn’t paranoia.

**It’s engineering maturity.**

Whether you end up running true multicloud in production or simply gain the confidence to evaluate alternatives, the skill of being fluent across AWS, GCP, and Azure will make you a better engineer and a more valuable team member. And honestly? Experimenting with different platforms, comparing how each one solves the same problem, seeing where one provider clearly outshines the others that part is just fun.

### References

**Google Cloud accidentally nukes customer account, causes two weeks of downtime**
----------------------------------------------------------------------------------

### [“Unprecedented” Google Cloud event wipes out customer account and its backups](https://arstechnica.com/gadgets/2024/05/google-cloud-accidentally-nukes-customer-account-causes-two-weeks-of-downtime/)

**Ars Technica’s detailed breakdown of how Google Cloud deleted UniSuper’s $135 billion pension fund account, including all backups stored on the service.**

> Google’s Amazon Web Services competitor accidentally deleted a giant customer account for no reason. UniSuper, an Australian pension fund that manages $135 billion worth of funds and has 647,000 members, had its entire account wiped out at Google Cloud, including all its backups that were stored on the service. **— Ron Amadeo**

**Amazon convenes ‘deep dive’ internal meeting to address outages**
-------------------------------------------------------------------

### [**Amazon convenes ‘deep dive’ internal meeting to address outages**](https://www.cnbc.com/2026/03/10/amazon-plans-deep-dive-internal-meeting-address-ai-related-outages.html)

**CNBC’s reporting on Amazon’s internal response to multiple Sev-1 retail outages, including the role of GenAI-assisted code changes and the 90-day safety reset.**

> The meeting comes after Amazon’s [online store malfunctioned](https://www.cnbc.com/2026/03/05/amazon-online-store-suffers-outage-for-some-users.html) for some users last week. For roughly six hours on Thursday, website and app users were unable to check out, access account information or view product prices. Amazon said in a statement that the issues were related to a “software code deployment.” **— Annie Palmer**

**Amazon Responds To Inaccurate Financial Times Report Linking Outages To AI**
------------------------------------------------------------------------------

### [Correcting the Financial Times report about recent Amazon.com service incidents and AI](https://www.aboutamazon.com/news/company-news/amazon-outage-ai-financial-times-correction)

**Amazon’s official statement disputing claims about AI-written code causing outages, providing their side of the story for balanced contex**

> That initial report sparked other media coverage repeating those false claims, even after the Financial Times corrected some of its initial assertions. In fact, only one of the recent incidents involved AI tools in any way, and in that case the cause was unrelated to AI and instead our systems allowed an engineering team user error to have broader impact than it should have. **— Amazon Staff**

**Multicloud Resilience Strategies Reshape Enterprise IT**
----------------------------------------------------------

### [From cloud-first to control-first: theCUBE’s SUSECON keynote analysis](https://siliconangle.com/2026/04/21/multicloud-resilience-strategies-reshape-enterprise-susecon/)

**SiliconAngle’s coverage of how nearly 9 in 10 companies now operate a multicloud strategy, with digital sovereignty and regulations shaping long-term adoption.**

> Multicloud resilience is no longer a buzzword. As enterprises wrestle with surging AI adoption and mounting compliance pressures, digital sovereignty has become the new battleground for control over infrastructure and data **— Ryan Stevens**

**What is Multicloud? Definition and Benefits**
-----------------------------------------------

### [What is multicloud?](https://cloud.google.com/learn/what-is-multicloud)

**Google Cloud’s own comprehensive explainer on multicloud definitions, benefits, challenges, and strategy considerations.**

> Multicloud is when an organization uses cloud computing services from at least two cloud providers to run their applications. Instead of using a single-cloud stack, multicloud environments typically include a combination of two or more [public clouds](https://cloud.google.com/learn/what-is-public-cloud), two or more private clouds, or some combination of both. **— Google Cloud**

UniSuper’s Entire Infrastructure Deleted by Internal Google Cloud Error
-----------------------------------------------------------------------

### [**UniSuper’s Entire Infrastructure Deleted by Internal Google Cloud Error**](https://www.infoq.com/news/2024/05/google-cloud-unisuper-outage/)

**Technical analysis of how UniSuper’s data was duplicated across two Google Cloud regions, yet both copies were lost due to a single internal error proving that regional redundancy within one provider isn’t always enough.**

> An Australian superannuation fund manager, [UniSuper](https://www.unisuper.com.au/about-us), using Google Cloud for an Infrastructure-as-a-Service (IaaS) contract, found it had no disaster recovery (DR) recourse when its entire infrastructure subscription was deleted. **— Steef-Jan Wiggers**

Proven Practices for Succeeding with a Multicloud Strategy
----------------------------------------------------------

### [**Proven Practices for Succeeding with a Multicloud Strategy**](https://aws.amazon.com/blogs/enterprise-strategy/proven-practices-for-succeeding-with-a-multicloud-strategy/)

**AWS’s own guidance on when and how to adopt multicloud, including M&A scenarios, specialized capabilities, and holding-company structures.**

> Organizations typically adopt multicloud for strategic reasons. They integrate newly acquired companies that operate on different platforms, leverage specialized capabilities from different providers, or support different cloud strategies at holding-company versus operating-company levels. **— Tom Godden**

**Introduction to Hybrid and Multicloud**
-----------------------------------------

### [Unified hybrid and multicloud operations](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/scenarios/hybrid/strategy)

**Microsoft’s framework for planning hybrid and multicloud adoption, including Azure Arc for managing resources across providers.**

> Hybrid cloud refers to a mix of on-premises/private infrastructure and public cloud services working together, while multicloud means using multiple cloud providers concurrently. Many enterprises today have siloed teams, distributed sites, and systems spread across on-premises datacenters and various clouds. The challenge is to unify these environments in a secure, well-managed way that enables modernization from cloud to edge. **— Microsoft Azure**

Why CIOs Should Challenge Conventional Cloud Wisdom
---------------------------------------------------

### [**Why CIOs Should Challenge Conventional Cloud Wisdom**](https://www.forbes.com/councils/forbestechcouncil/2025/08/28/why-cios-should-challenge-conventional-cloud-wisdom/)

**Forbes analysis of how single-vendor consolidation can lock companies into rigid ecosystems that limit flexibility, hinder innovation, and reduce returns over time.**

> Imagine one of your company’s largest technology expenses spiking by 17% each year without clear justification — and receiving little scrutiny. That likely sounds surprising, but it’s a more [common occurrence](https://www.networkworld.com/article/4029004/unexpected-costs-drive-on-premises-computing.html) than many realize with cloud costs.
> 
> As the old adage goes, ‘Nobody gets fired for buying IBM’ — a sentiment that still influences how companies choose large cloud service providers (CSPs). However, it’s worth questioning whether that conventional wisdom always leads to the best outcomes — **Thomas Robinson**

---

# The Original

**Blog:** [StudentAnalyst](https://medium.com/studentanalyst)
<br>
**Article Link:** [Towards MultiCloud](https://medium.com/studentanalyst/towards-multicloud-26ad5c69f4d5)
<br>
Originally Published by [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona) 
<br>
**30 November 2024**
