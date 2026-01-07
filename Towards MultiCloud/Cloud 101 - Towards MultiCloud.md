# Towards MultiCloud


## Cloud 101
---------

> [Over half a million UniSuper members failed to access their accounts after Google Cloud accidentally deleted the private cloud account of the Australian pension fund worth $125 billion](https://www.business-standard.com/world-news/google-cloud-accidentally-deletes-125-billion-australian-pension-fund-124051800606_1.html). — [Abhijeet Kumar](https://www.business-standard.com/author/abhijeet-kumar)

Do you remember the viral story about how Google Cloud accidentally deleted a billion-dollar pension fund? Wild, right? That incident inspired me to accelerate my Multi-Cloud journey. While it’s possible to create redundant backups that span zones and regions within a single cloud provider, that alone may not be enough.

> [Why it matters: Fortunately for the $135 billion Australian pension fund’s 647,000 members, some of UniSuper’s backups on Google Cloud’s servers and elsewhere were salvageable, and the fund was able to recover its data, teaching us all a lesson about having multiple redundancies. — Hope King](https://www.axios.com/2024/05/30/google-cloud-pension-error)

It doesn’t hurt to have your workloads running across multiple vendors. Additionally, since transferring data out of the cloud can be expensive, using the analytics services of one cloud provider while storing the data in another could be a cost-effective solution. Even before defining Multi-Cloud, it already sounds like an efficient and economical backup strategy.

The Cloud Providers I Will Be Focusing On
-----------------------------------------

### Amazon Web Services (AWS):

AWS is my primary and preferred cloud provider. Honestly, its systems are so robust that Multi-Cloud feels more like an option for the other providers. As a result, my posts will primarily focus on how to run services from other clouds on AWS.

So, if you’re looking for reasons to switch to AWS or want to see how it compares to other platforms, stick around!

### Microsoft Azure (Azure)

Apparently, Microsoft Azure has been, or currently is, focused on converting its existing customers who used other services to adopt its cloud platform. Still, it’s fun to experiment with.

### Google Cloud Platform (GCP)

Google Cloud Platform may not offer a vast array of services, but it’s currently one of the top providers — so why not give it a try?

Multi-Cloud is self-explanatory, but this [**article**](https://cloud.google.com/learn/what-is-multicloud) covers everything I wanted to say, so I won’t reinvent or paraphrase the wheel, if you catch my drift.

What Is Multicloud?
-------------------

> Multicloud is when an organization uses cloud computing services from at least two cloud providers to run their applications. Instead of using a single-cloud stack, multicloud environments typically include a combination of two or more [public clouds](https://cloud.google.com/learn/what-is-public-cloud), two or more private clouds, or some combination of both. By having the freedom to create a strategy that utilizes multiple vendors, you can pick and choose the capabilities that best suit your specific business needs and minimize vendor lock-in. — Google Cloud

### Multicloud vs. hybrid cloud

> Not clear on the difference between multicloud and hybrid cloud? This simple analogy may help:
> 
> Think of a hybrid cloud like a hybrid car, which combines two different types of engines — an electric engine and a traditional combustion engine — to power your automobile.
> 
> On the other hand, a multicloud infrastructure would be using different types of transport to go to different places. For instance, you might drive your car to the mall because it’s easier to carry shopping bags home but choose to take the train to work since it saves you gas money and helps you avoid rush hour traffic.
> 
> Since workloads, instructures, and processes often vary across organizations, there’s a lot of inconsistency around what multicloud and hybrid cloud mean. In some cases they are even used interchangeably. However, these two terms actually refer to two distinct concepts.

Multicloud management
---------------------

> To get the most out of multicloud architecture, it’s important to be able to track, secure, and manage your workloads consistently across all your environments from a single interface, similar to if you were running them on a single platform.
> 
> The more cloud providers you use, the more complex the task of managing your environments becomes. Most public cloud vendors not only have different features, but also have varying tools, SLAs, and APIs for managing cloud services. While it’s possible to manage each environment separately, most IT teams lack the time and resources. — Google Cloud

Benefits of Multicloud
----------------------

> Leveraging multicloud services can offer many opportunities to increase the IT agility and flexibility of your organization. Let’s take a look at some of the most common benefits of multicloud:

### Best of each cloud

> Multicloud allows you to choose from many cloud vendors and provides the flexibility to match specific features and capabilities to optimize your workloads in the cloud based on factors like speed, performance, reliability, geographical location, and security and compliance requirements.

### Avoid vendor lock-in

> A multicloud environment allows you to build anywhere, fast. With a multicloud approach, you’re not tied to a single provider. You can choose whatever solution best suits your business needs while reducing data, interoperability, and cost issues that often arise when you become too dependent on one cloud.

### Cost efficiency

> Multicloud environments can be a good option for minimizing your IT spending. Public cloud comes with less overhead while allowing you to scale up or down according to your needs. You can lower TCO while also taking advantage of the best combination of pricing and performance across different providers.

### Innovative technology

> Cloud providers constantly invest in developing new products and services. Multicloud enables you to leverage new technologies as they emerge to improve your own offerings without being limited to the choice offered by a single cloud provider.

### Advanced security and regulatory compliance

> A multicloud strategy enables you to deploy and scale workloads while also implementing security policies and compliance technologies consistently across all of your workloads, regardless of service, vendor, or environment.

### Increased reliability and redundancy

> Multicloud reduces unplanned downtime or outages since it reduces the risk of a single point of failure. An outage in one cloud won’t necessarily impact services in other clouds, and if your cloud does go down, your computing needs can be routed to another cloud that’s ready to go.

Challenges of multicloud
------------------------

> For all its benefits, a multicloud approach does come with potential roadblocks that some organizations find difficult to navigate. Some of the most common multicloud challenges include increased management complexity, maintaining consistent security, integrating software environments, and difficulty with achieving consistent performance and reliability across clouds.
> 
> A multicloud strategy should take into consideration business requirements, design and development drivers, and any architecture constraints that may arise from existing systems. It’s vital to take the time to clearly define your goals in a vision statement that outlines the reasons you want to migrate your current computing environment, the primary metrics you want to optimize for with the public cloud, and the long-term plan for using a multicloud setup in your organization. From there, you can work to create a plan on how to [approach and implement a multicloud setup](https://cloud.google.com/architecture/hybrid-and-multi-cloud-patterns-and-practices), from assessing and prioritizing your workloads, identifying the right cloud computing environment for them, and the architecture pattern, technologies, and network topologies that will work best for your requirements.

Why use a multicloud strategy?
------------------------------

> By having the freedom to move your applications, you can directly control cost, uptime, latency, and downtime, which all directly impact your customers’ experience. On the enterprise side, using a multicloud strategy allows you to avoid vendor lock-in, allowing you to find the cloud products and services that bring the most value
> 
> If your organization cares about any of the following, you’re probably a good candidate for a multicloud strategy:
> 
> Having more flexibility and avoiding vendor lock-in
> 
> Ensuring high availability to prevent website outages
> 
> Developing a strong data protection and risk mitigation plan
> 
> Providing the best latency and load times for your customers
> 
> Acquiring competitive pricing between cloud providers
> 
> Having constant access to network performance improvements
> 
> Following region-specific compliance rules
> 
> These activities require more options and capabilities than a one-cloud strategy can provide, especially given the differing priorities, business requirements, and digital maturity across organizations.

The cost vs. value of multicloud
--------------------------------

> Many organizations often worry about the overall cost of migrating to cloud environments as well as ballooning bills that may arise from underutilized resources or lack of control over provisioning and usage. However, multicloud management tools or a multicloud management platform can be used to gain visibility and governance over cloud resources across cloud environments.
> 
> Additionally, it’s important to weigh short-term costs against the long-term value of adopting multicloud. For example, deploying applications on multiple clouds for disaster recovery or increasing reliability may increase costs but could prevent outages or failures that would cause long-term financial and reputational damage

Additional Resources
--------------------

### [What is MultiCloud](https://cloud.google.com/learn/what-is-multicloud)

> Leveraging multicloud services can offer many opportunities to increase the IT agility and flexibility of your organization.

**Concluding Remarks**
----------------------

Experimenting with multiple technologies, languages, and cloud vendors should be fun!

# The Original

**Blog:** [StudentAnalyst](https://medium.com/studentanalyst)
<br>
**Article Link:** [Towards MultiCloud](https://medium.com/studentanalyst/towards-multicloud-26ad5c69f4d5)
<br>
Originally Published by [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona) 
<br>
**30 November 2024**
