Multicloud Management
=====================

The Complexity Of Multicloud Architecture
-----------------------------------------

### The Problem Multicloud Creates

In [Towards MultiCloud](https://medium.com/studentanalyst/towards-multicloud-26ad5c69f4d5), I made the case for _why_ multicloud matters :

1.  Resilience
2.  Best-of-breed services
3.  Avoiding lock-in.

But…The instant you adopt a second cloud provider, your operational **complexity** doesn’t double. It _multiplies._

You now have:

*   Two consoles with different UIs, different terminology, different navigation
*   Two identity systems with different permission models
*   Two billing dashboards measuring costs in different units and cycles
*   Two sets of CLI tools, SDKs, and APIs
*   Two monitoring systems that don’t talk to each other by default

Scale that to three providers and you start to understand why **multicloud management** isn’t just a topic in this series. It’s arguably _the_ topic. Getting the architecture right means nothing if you can’t operate it.

What Is Multicloud Management?
------------------------------

Multicloud management is the practice of tracking, securing, governing, and optimizing workloads consistently across all your cloud environments. Ideally from a unified interface, as if everything were running on a single platform.

It covers several domains:

### **Visibility & Observability**

**Can you see what’s running, where, and how it’s performing across all providers?**

Native tools like AWS CloudWatch, GCP Cloud Monitoring, and Azure Monitor each give you a partial view.

_Multicloud management means stitching those views together._

### **Governance & Policy**

**Are your security policies, tagging standards, and compliance requirements enforced consistently?**

A misconfigured S3 bucket on AWS is just as dangerous as a misconfigured Cloud Storage bucket on GCP.

_Your governance shouldn’t have blind spots based on which provider hosts the resource._

### **Cost Management**

**Can you track total cloud spend across providers, identify waste, and optimize reserved capacity?**

Each provider’s native cost tools only show their own slice.

_Unified FinOps tooling gives you the full picture._

### **Security & Compliance**

**Are identities, encryption, network policies, and audit trails managed cohesively?**

Or does each cloud have its own security posture that nobody’s comparing?

### **Provisioning & Automation**

Can you deploy infrastructure consistently across providers using shared tooling like Terraform or are you maintaining separate CloudFormation, Deployment Manager, and Bicep templates?

The “Single Pane of Glass” Promise
----------------------------------

The industry loves the phrase **single pane of glass:** one dashboard to rule them all. The reality is more nuanced.

According to research, 85% of enterprise IT leaders report that achieving true unified observability remains elusive despite substantial investments. Organizations average five different tools to manage their multicloud environments.

The goal isn’t necessarily one tool that does everything. It’s reducing the cognitive overhead of context-switching between providers and ensuring nothing falls through the cracks between them.

How Each Provider Approaches Multicloud Management
--------------------------------------------------

Each major cloud provider has built tooling that extends their management plane beyond their own borders. The motivations are obvious.

They want to be your _primary_ cloud, the one you manage everything from. But the tools are genuinely useful regardless of which provider you prefer.

### Azure Arc

Microsoft’s play for multicloud management. I first heard about Azure Arc at a [Microsoft Migration Summit](https://ntombizakhona.medium.com/microsoft-migration-summit-da3f872dc361?postPublishedType=repub) five years ago — I think, and I haven’t really stopped thinking about it.

Azure Arc projects resources from _any_ environment, on-premises servers, AWS, GCP, edge locations into the Azure control plane. Once projected, you can apply Azure Policy, use Azure Monitor, and manage them as if they were native Azure resources.

**What It Manages Across Clouds:**

*   Servers (any OS, any location)
*   Kubernetes clusters (EKS, GKE, self-managed)
*   SQL Server instances
*   Data services

**The Pitch:** _If your organization already lives in the Microsoft ecosystem, Arc lets you extend that familiarity everywhere without learning new management tools for each provider._

### Google Cloud’s Distributed Cloud (formerly Anthos)

Google’s approach centers on Kubernetes as the universal abstraction layer. You can register EKS clusters on AWS, AKS clusters on Azure, or self-managed clusters anywhere, then manage them all from the Google Cloud Console with consistent policies, security, and observability.

**What It Manages Across Clouds:**

*   Kubernetes clusters (anywhere)
*   Service mesh (Istio-based)
*   Policy enforcement (Config Management)
*   Observability (Cloud Monitoring across registered clusters)

**The Pitch:** _If your workloads are containerized and you want Kubernetes done right everywhere, GKE Enterprise gives you Google’s operational expertise applied to clusters running on competitors’ infrastructure._

### AWS (The Pragmatic Approach)

AWS has historically been less aggressive about managing _other_ clouds. Their multicloud story is more about being so comprehensive that you don’t need to leave. That said:

*   **AWS Systems Manager** can manage on-premises and hybrid resources
*   **EKS Anywhere** runs EKS-compatible clusters outside AWS
*   **AWS Outposts** brings AWS hardware to your data center

AWS also publishes [prescriptive guidance on multicloud strategy](https://docs.aws.amazon.com/prescriptive-guidance/latest/strategy-multicloud/introduction.html), acknowledging that multicloud is a reality for many organizations particularly through M&A, specialized capabilities, or regulatory requirements.

> You shouldn’t have to rebuild everything when you add capabilities from another provider.
> 
> Your cloud should help you connect, secure, and manage workloads across environments without forcing you to become an expert in every platform.
> 
> AWS builds connection points directly into its services to help you operate effectively, whether your strategy is to use AWS exclusively or to follow a selective multicloud approach.

**The Pitch:** _AWS won’t manage your GCP resources for you, but they’ll give you the broadest single-cloud catalog so you need fewer reasons to go elsewhere._

Third-Party Multicloud Management Tools
---------------------------------------

Beyond the hyperscalers’ own offerings, a rich ecosystem of independent tools exists:

### **Infrastructure as Code**

*   **Terraform** (HashiCorp/OpenTofu): The de facto standard for multicloud IaC. Write once, deploy to any provider.
*   **Pulumi:** IaC using real programming languages (TypeScript, Python, Go) instead of HCL.

### **Observability**

*   **Datadog:** Unified monitoring, logging, and APM across all major clouds.
*   **Grafana Cloud:** Open-source-friendly observability stack with multi-provider support.
*   **Dynatrace:** AI-powered full-stack observability with automatic discovery across clouds

### **Cost Management (FinOps)**

*   **Flexera:** The industry’s most-cited cloud cost management platform.
*   **CloudHealth (VMware):** Multicloud governance and cost optimization.
*   **Spot by NetApp:** Automated cost optimization across providers.

### **Security & Compliance**

*   **Prisma Cloud (Palo Alto):** Cloud security posture management across AWS, GCP, Azure.
*   **Wiz:** Agentless cloud security scanning across all major providers.

### **Kubernetes Management**

*   **Rancher:** Manage Kubernetes clusters across any provider from one UI.
*   **Crossplane:** Compose cloud infrastructure from Kubernetes using provider-agnostic APIs.

The Maturity Spectrum
---------------------

Not every organization needs the same level of multicloud management. Here’s a rough maturity model:

### **Level 1**

**Separate Silos**
Each cloud is managed independently by different teams with different tools. Common in organizations that adopted multicloud through acquisition rather than strategy.

### **Level 2**

**Unified Visibility**
A single observability layer (Datadog, Grafana) gives you cross-cloud dashboards, but provisioning and governance are still per-provider.

### **Level 3**

**Consistent Governance**
Shared IaC (Terraform), unified security policies, and cross-cloud tagging standards. Teams can work across providers with consistent guardrails.

### **Level 4**

**Abstracted Operations**
Kubernetes or serverless abstractions mean workloads are portable. The underlying provider is an implementation detail, not an operational concern.

_Most organizations are somewhere between Level 1 and Level 2. Level 4 is aspirational for all but the most mature platform teams._

Practical Advice for Getting Started
------------------------------------

### **1. Start With Observability.**

**You can’t manage what you can’t see.** Get a unified monitoring solution before worrying about unified provisioning.

### **2. Standardize on Terraform Early.**

Even if you’re only on one cloud today, writing IaC in Terraform (rather than CloudFormation or Bicep) keeps your options open.

### **3. Unify Identity Where Possible.**

Federate identities across providers so your team isn’t managing three separate sets of credentials. SAML/OIDC federation is your friend.

### **4. Don’t Boil The Ocean.**

You don’t need Level 4 maturity on day one. Pick the domain that causes the most pain (usually cost visibility or security posture) and unify that first.

### **5. Accept Some Duplication.**

Not everything needs to be abstracted. It’s okay to use CloudWatch for AWS-specific operational alerts while using Datadog for cross-cloud business metrics.

### A Somewhat Hands-On Journey Across AWS, GCP, and Azure

🏗️ MultiCloud Management Tutorial
----------------------------------

1.  Create free-tier accounts on **IBM Cloud**, **AWS**, **GCP**, and **Azure**
2.  Provision a **comparable virtual machine** on each of the three major providers
3.  Connect all three environments to **IBM Turbonomic** for unified multicloud visibility
4.  Observe and compare our resources from a single dashboard

By the end, you’ll have _identical-ish_ Linux VMs running across three clouds

**Let’s observe the complexity of multicloud management.**

Part I | Creating Your Free-Tier Accounts
-----------------------------------------

### [A] IBM Cloud Account

IBM Cloud is our management layer.

Turbonomic runs here.

**Step [A]01:** Go to [https://cloud.ibm.com/registration](https://cloud.ibm.com/registration)

**Step [A]02:** Enter your email address, full name, and country

**Step [A]03:** Check your inbox for a verification code and enter it

**Step [A]04:** Create a password (minimum 8 characters, mixed case + number)

**Step [A]05:** Accept the terms and data privacy policy

**Step [A]06:** Add a credit card to activate Pay-as-you-go

💡**The Turbonomic trial is free for 30 days.**

> **💸 _Cost:_** _$0. IBM Cloud’s Pay-as-you-go account gives you access to 50+ free-tier products._
> 
> _Your card won’t be charged unless you explicitly provision paid services._

⚠️**Verify:** Log in at [cloud.ibm.com](https://cloud.ibm.com/) and confirm you see the IBM Cloud dashboard.

### [B] AWS Account

**Step [B]01:** Go to [https://aws.amazon.com/free](https://aws.amazon.com/free)

**Step [B]02:** Click **“Create a Free Account”**

**Step [B]03:** Enter your email and choose an account name

**Step [B]04:** Verify your email with the code sent to your inbox

**Step [B]05:** Set your root password

**Step [B]06:** Choose **“Personal”** account type

**Step [B]07:** Enter your billing information (credit card required)

**Step [B]08:** Verify your identity via phone (SMS or voice call)

**Step [B]09:** Select the **“Basic Support — Free”** plan

**💡Complete the activities in this article to earn the credits:** [**Amazon Web Services**](https://ntombizakhona.medium.com/amazon-web-services-a8e57a9c6084)

> **💸 _Cost:_** _$0 for our use case._
> 
> _New AWS accounts (created after July 15, 2025) receive up to_ **_$200_** _in free credits valid for 6 months._
> 
> _Older accounts get 12 months of free-tier access including 750 hours/month of t2.micro or t3.micro EC2._

⚠️**Verify:** Log in at [console.aws.amazon.com](https://console.aws.amazon.com/) and confirm you reach the AWS Management Console.

### [C] Google Cloud Platform Account

**Step [C]01:** Go to [https://cloud.google.com/free](https://cloud.google.com/free)

**Step [C]02:** Click **“Get started for free”**

**Step [C]03:** Sign in with your Google account (or create one)

**Step [C]04:** Accept the terms of service

**Step [C]05:** Choose your country and organization type (Individual)

**Step [C]06:** Add a credit card for identity verification

**💡 You’ll receive $300 in free credits valid for 90 days.**

> **💸 _Cost:_** _$0._
> 
> _Beyond the $300 trial credit, GCP offers an “Always Free” tier that includes one e2-micro VM instance per month in select US regions which is permanently free._

⚠️**Verify:** Go to [console.cloud.google.com](https://console.cloud.google.com/) and confirm you see the GCP Console.

**Step [C]07:** Create a new project called `multicloud`

### [D] Microsoft Azure Account

**Step [D]01:** Go to [https://azure.microsoft.com/free](https://azure.microsoft.com/free)

**Step [D]02:** Click **“Start free”**

**Step [D]03:** Sign in with your Microsoft account (or create one)

**Step [D]04:** Verify your identity via phone

**Step [D]05:** Add a credit card for verification

**Step [D]06:** Accept the agreement and click **“Sign up”**

**💡 You’ll receive $200 in free credits valid for 30 days**

> **💸 _Cost:_** _$0 for our use case._
> 
> _After the $200 credit expires, you still get 12 months of select free services (including 750 hours/month of a B-series VM with Linux)._

⚠️**Verify:** Go to [portal.azure.com](https://portal.azure.com/) and confirm you see the Azure Portal.

Part II | Provisioning Comparable VMs Across All Three Clouds
-------------------------------------------------------------

We’ll create a small Linux VM on each provider. The goal is to have similar workloads so we can compare them side-by-side in Turbonomic.

### Target Spec For Each VM

```
**Attribute**  | Target
-----------|-----------------------------
**OS **        | Ubuntu 22.04 LTS (or 24.04)
**vCPUs**      | 1
**RAM**        | ~1 GB
**Storage**    | 10–30 GB SSD
**Cost**       | Free tier / trial credits
```

### [A] Generate a Single SSH Key Pair

Instead of managing three separate key pairs, we’ll generate one and reuse it everywhere.

**Step [A]01:** On your local machine (Linux/Mac/WSL):

```
ssh-keygen -t ed25519 -C "multicloud" -f ~/.ssh/multicloud
```

**Step [A]02:** When prompted for a passphrase, either set one (recommended) or press Enter for none.

**💡** This creates two files:

1.  Your **private** key (never share this): `~/.ssh/multicloud`
2.  Your **public** key (this goes on each cloud): `~/.ssh/multicloud.pub`

**Step [A]03:** On Windows (PowerShell, no WSL):

⚠️ **First, make sure the `.ssh` folder exists** (Windows won’t create it automatically):

```
New-Item -ItemType Directory -Force -Path $env:USERPROFILE\.ssh
```

**Step [A]04: Then generate the key**

```
ssh-keygen -t ed25519 -C "multicloud" -f $env:USERPROFILE\.ssh\multicloud
```

> **_❓Why one key pair?_**
> 
> _It’s simpler to manage, demonstrates that SSH keys are cloud-agnostic, and reinforces that compute access is a standard, not a proprietary feature._
> 
> _You’ll SSH into all three VMs with the same command, just different IP addresses._

**Step [A]05:** Copy your public key contents for the next steps

```
cat ~/.ssh/multicloud.pub
```

⚠️ **Keep this output handy.** You’ll paste it into AWS, GCP, and Azure.

### [B] AWS EC2 Instance

First, import your shared key pair into AWS

**Step [B]01:** Go to **EC2**

**Step [B]02: ▼ Network & Security → Key Pairs**

**Step [B]03: Actions ▼ → Import key pair**

**Step [B]04: Import key pair**

**→ Name:** `multicloud`

**→ Kay pair file:** Paste the contents of your `multicloud.pub` file

**→** Click **Import key pair**

✅**Green banner: Successfully imported key pair**

**Step [B]05:** Go to **▼ Instances**

**→ Instances**

**→ Launch instances**

**Step B[06]: Launch an instance**

**→ Name:** `multicloud-aws`

**→ Add additional tags**

**→ Key:** `Project` | **Value:** `multicloud`

**→ Key:** `Environment`| **Value:** `management`

**→ Application and OS Images (Amazon Machine Image):** `ubuntu`

**→ Amazon Machine Image (AMI):** `Ubuntu Server 24.04 LTS (Free tier eligible)`

**→ ▼ Instance type:** `t3.micro`

**→ ▼ Key pair (login):** `multicloud`

**→ ▼ Network Settings**

**→ Firewall (security groups)**

**→ Create security group**

✔ Allow SSH traffic from: `My IP`

✔ Allow HTTP traffic from the internet

**→ ▼ Configure storage:** `Leave default`

**→ ▼** Summary

**→ Launch instance**

✅**Green banner: Success**

**Step B[07]:** Click **View all Instances**

⚠️ **Verify:** Your instance should show **Running** with a green status check within 2 minutes.

### [C] GCP Compute Engine Instance

First, add your shared SSH key to the project

**Step [C]01:** Go to **APIs & Services ›**

**→ Library**

🔎︎ **Compute Engine API**

**Step [C]02: Enable Compute Engine API**

**Step [C]03:** Go to **Compute Engine ›**

**→ Metadata**

**→ SSH Keys**

**→ Add SSH Key:** Paste the contents of your `multicloud.pub` file

**→ Save**

🔔**Successfully saved SSH keys**

**Step [C]04: VM Instances**

**→ + Create Instance**

● **Machine Configuration**

**→ Name:** `multicloud-gcp`

**→ Region:** `us-east1 (South Carolina)`

**→ Zone:** `Any`

**→ Series:** `E2`

**→ Machine type:** `e2-micro`

● **OS and storage**

**→** Change

→ **Operating system:** `Ubuntu`

**→ Version:** `Ubuntu 24.04 LTS`

**→ Boot disk type:** `Standard persistent disk`

**→ Size (GB):** `10`

**→ Select**

● **Networking**

**→ Firewall:** ✔ `Allow HTTP Traffic`

**→ Create**

> **_💡_**_Your shared SSH key is automatically applied to the instance via project metadata._

⚠️ **Verify:** The VM should show a green checkmark within 1–2 minutes. **Note the external IP address.**

**Step [C]05: Manage Labels**

**→ Key:** `project` | **Value:** `multicloud`

**→ Key:** `environment`| **Value:** `management`

> **💸 _Always Free Note:_** _One e2-micro instance in us-west1, us-central1, or_ **_us-east1_** _is free indefinitely (up to 730 hours/month)._
> 
> _If you pick a different region, it will consume your $300 trial credit instead._

### [D] Azure Linux VM

**Step [D]01:** Go to 🖥️ **Virtual Machines**

**→** ╋ **Create** ⮟

**→** 🖥️ V**irtual machine**

**→ Basics**

*   **Subscription:** `Your free subscription`
*   **Resource group:** **Create new** → `multicloud`
*   **Virtual machine name:** `multicloud-azure`
*   **Region:** `East US 2`
*   **Availability options:** `No infrastructure redundancy required`
*   **Security type:** `Standard`
*   **Image:** `Ubuntu Server 24.04 LTS`
*   **Size**: **Click See all sizes** → search for `**B2ats_v2**`→ **Select**
*   **Authentication type:** `SSH public key`
*   **SSH public key source:** `Use existing public key`
*   **Username:** `azureuser`
*   **SSH public key:** Paste the contents of your `multicloud.pub`

**→ Disks**

*   **OS disk size:** `**Image default** (30GiB)`
*   **OS disk type:** `**Standard SSD** (locally-redundant storage)`

**→ Networking**

*   **Select inbound ports:** ✔ `**SSH** (22)`and `**HTTP** (80)`

**→ Tags**

*   **Name:** `Project` → **Value**: `multicloud`
*   **Name:** `Environment` → Value: `management`

**→ Review + create** → **Create**

**Verify:** Go to Virtual Machines. Your VM should show _Running_ within 2–3 minutes.

> **_Note on B-series retirement:_** _The original B1s (v1) is being phased out in many regions. If you can’t find it, use B2ats_v2 which is the next-generation burstable equivalent. Your $200 free credit covers it regardless._

### [E] Verify All Three VMs Are Running

At this point you should have:

```
Provider | VM Name              | Type               | Region                 | Status
---------|----------------------|--------------------|------------------------|-----------
AWS      | multicloud-aws       | t3.micro           | us-east-1              | ✅ Running
GCP      | multicloud-gcp       | e2-micro           | useast-1               | ✅ Running
Azure    | multicloud-azure     | btast_v2           | us-east                | ✅ Running
```

Three clouds.

Three VMs.

Same OS.

Similar specs.

_Now let’s see them all in one place._

### [F] Pricing Calculators

Before scaling beyond free tier, it’s smart to estimate costs.

Each provider offers a pricing calculator.

```
**Provider**  | _Calculator URL_                        | Notes
----------|-------------------------------------  |---------------------------------------------------------
**AWS**       | _calculator.aws_                        | Build estimates by service, export as PDF/CSV
**GCP**       | _cloud.google.com/products/calculator_  | Includes sustained-use and committed-use discounts
**Azure**     | _azure.microsoft.com/pricing/calculator_| Supports reservations and hybrid benefit pricing
**IBM Cloud** | _cloud.ibm.com/estimator_               | Covers IBM Cloud services including Turbonomic
```

⚠️**Try this now:** Open each calculator and price out the VM you just created.

> **_💡_** **_These are the costs you’d pay without free tier. Understanding pricing across providers is a core Multicloud skill. Especially when comparing like-for-like workloads at scale._**

Part III | The Headache of Setting Up IBM Turbonomic
----------------------------------------------------

### [A] Start The Turbonomic SaaS Trial

**Step [A]01:** Go to [https://www.ibm.com/products/turbonomic](https://www.ibm.com/products/turbonomic)

**Step [A]02:** Click **Start Free Trial** ➜

**Step [A]03:** Sign in with your IBM Cloud credentials

> **_💡IBM provisions your Turbonomic SaaS instance (takes 2–5 minutes)_**
> 
> **_You’ll receive an email with your dashboard URL_**

**Step [A]04:** Click **Access now** ➜

**Step [A]05: IBM SaaS account name:** `multicloud`

**Step [A]06:** Click **Next**

**Step [A]07: Region:** `N.Virginia(us-east-1)`

**Step [A]08:** Click **Submit and provision**

### [B] When the Trial Doesn’t Provision

Everything above is how the trial is _supposed_ to work. Here’s what actually happened when I ran through it, because the failure mode is more instructive than the happy path.

The trial request went through on **1 August 2026**. The subscription appeared in the **IBM SaaS Console** under the product name **Concert Optimize** which is the current packaging of Turbonomic’s SaaS offering, so don’t be thrown if you don’t see the Turbonomic name on your subscription. The instance page showed

*   Status: **Error provisioning**
*   Region: **N. Virginia (us-east-1)**
*   **Open instance** button: greyed out and unusable

No dashboard URL was ever issued, so there was nothing to log into. Note the console also listed “Cloud provider: AWS” despite the trial being requested directly from IBM. That field describes the infrastructure IBM runs the instance on, not how you signed up.

Since a failed provision is a platform-side problem, the only path forward was IBM support. That’s where it ended:

> _IBM eSupport replied that provisioning failures are outside their scope. Apparently they handle the Support Community site itself, not products. To open a_ product _support case, your IBMid must be linked to an_ **_IBM Customer Number (ICN)_**_, a 7-digit identifier tied to a purchasing account. Their suggested ways to obtain one: ask your management or team leads, contact your IBM Sales Representative or IBM Business Partner, or go through IBM Passport Advantage._

Read that carefully and the catch becomes clear. **The trial is self-service, but support for the trial is not.** If provisioning succeeds, you’re fine. If it fails, the remedy requires an ICN and an ICN comes from a purchasing relationship that a trial user, by definition, doesn’t have.

An individual learner, student, or independent engineer has no management chain to ask, no assigned sales rep, and no Passport Advantage account. The escalation path assumes you’re an employee of an existing IBM customer.

I’ll be straight about the disappointment here, because pretending otherwise would be dishonest. I genuinely wanted to use **Turbonomic.** I picked it deliberately as the centrepiece of this post. It seemed like the tool with the strongest cross-cloud optimisation story, IBM markets the trial as self-service, and demonstrating a real single pane of glass across three providers was the whole point of the exercise. I wrote the surrounding sections expecting it to work.

Instead it cost me ten days and produced nothing: a subscription that errored on creation, a dashboard I never saw, and a support process that ended by telling me to ask my employer for a customer number I was never going to have. That’s time I’d rather have spent on the actual multicloud work. If you’re evaluating tooling on your own time, learn from it. The trial being free doesn’t mean it’s cheap.

So I’m not proceeding with Turbonomic in this series. The instance never provisioned, and the support route is closed to the exact audience this post was written for. And, it’s multi_cloud._ The cloud is all about “_minimal management effort or service provider interaction.”_ I do not want to interact with any humans. Period.

### [C] **What This Means**

*   If your trial provisions cleanly, tell me all about it. I am all ears.
*   If you see **“Error provisioning,**” don’t burn a week on support. You have no realistic case-opening path without an ICN.
*   Before deleting a failed instance and retrying, be aware you may only get one trial entitlement per account.

### [D] Beyond Turbonomic

This is a genuine multicloud lesson, not just a vendor complaint. Enterprise management tooling is built and priced for enterprises, and the support model reflects that. When you’re evaluating a management plane, the question isn’t only “what can it do”, it’s “what happens when it breaks, and do I have standing to get help.”

AWS, GCP, and Azure will all take a support case from an individual with a credit card. Much of the enterprise multicloud tooling layer will not. That asymmetry is worth knowing before you build a strategy on top of it.

The concepts in Post 2 still hold. Turbonomic’s approach to cross-cloud optimisation is real and worth understanding. I just can’t demonstrate it hands-on here. But, at least I have demonstrated the complexity of multicloud management. The first lesson learnt is finding a multicloud management tool, oh well, I have an IBM Cloud Account now.

Part IV | Hunting For A MultiCloud Management Tool
--------------------------------------------------

The obvious next move was to find another tool. We’re managing virtual machines across three clouds, so I started with the vendor that has owned virtual machine management for two decades.

### [A] VMware, post-Broadcom

VMware has not one but two products aimed squarely at this problem, and the Broadcom acquisition reshaped access to both.

**Tanzu CloudHealth** is the multicloud cost and FinOps platform which was originally CloudHealth Technologies, acquired by VMware in 2018, now part of Broadcom’s portfolio.

It does cross-cloud cost visibility, allocation, and rightsizing recommendations across AWS, Azure, and GCP, which is the same territory Turbonomic occupies. It’s actively developed: Broadcom shipped a rebuilt interface with AI-assisted features in mid-2025.

The access problem is worse than IBM’s. Broadcom appointed **Arrow Electronics as the sole global go-to-market provider** for Tanzu CloudHealth. There is no direct purchase and no self-service trial. The route in is a distributor relationship. IBM at least let me create a subscription before the process collapsed.

**Aria Operations** (formerly vRealize Operations) is the closer functional match to Turbonomic with continuous performance optimisation, capacity planning, cost analysis, and automated remediation across vSphere and public cloud.

But it’s being folded into **VCF Operations** as part of VMware Cloud Foundation 9.x. Post-acquisition, Broadcom retired perpetual licensing and bundled the surviving products into VCF and VVF subscriptions priced per core with minimum core counts. You cannot buy Aria Operations on its own to look at three small cloud VMs.

Worth knowing about even though it’s out of reach here: **VMware Cloud on AWS**, **Azure VMware Solution**, and **Google Cloud VMware Engine**. These represent a genuinely different multicloud philosophy from anything else in this series.

Instead of abstracting over three dissimilar clouds, you run the same vSphere stack inside all three, so your tooling, runbooks, and skills stay identical everywhere. There’s no free tier because they’re dedicated bare-metal hosts, but it’s the option a large enterprise with twenty years of vSphere investment actually chooses, and understanding why is useful even if you never touch it.

### [B] Flexera One

**Flexera One** is a broader play than either Turbonomic or CloudHealth. Where those focus on infrastructure optimisation, Flexera One bundles **Cloud Cost Optimization** together with **IT Asset Management** and **SaaS Management** in one platform.

The pitch is that your real technology spend isn’t just cloud resources, it’s also software licensing, support contracts, SaaS subscriptions, and labou. Optimising cloud compute in isolation misses most of the bill. Its cloud cost engine goes past reporting into policy-based automated actions, and its lineage traces back to RightScale, which Flexera acquired in 2018.

It’s the most enterprise-shaped of the three: licence position, audit defence, and vendor renewal negotiation are core features. Access is sales-led. There’s no self-service tier, and pricing isn’t published.

One thing Flexera gives away freely and that’s genuinely worth your time: their annual **State of the Cloud Report**, which is the most-cited public dataset on multicloud adoption. You’ll see its figures quoted across the industry, including this series.

Free tooling? No. Free research? yes.

### [C] The Pattern

Three vendors, three different walls:

```
| Tool | What blocks an individual |
|------|--------------------------|
| IBM Turbonomic | Product support requires an IBM Customer Number tied to a purchasing account |
| VMware Tanzu CloudHealth | Sold exclusively through a single distributor; no direct trial |
| VMware Aria / VCF Operations | Only available inside per-core VCF/VVF subscription bundles |
| Flexera One | Sales-led onboarding; no self-service tier, no published pricing |
```

That’s not three unlucky vendors. It’s how this category is built, priced, and sold.

Enterprise multicloud management is designed around a procurement conversation, and the trial motion (where one exists at all) is a lead-generation step, not a product. The moment anything goes wrong, you need standing that only a paying customer has.

Compare that to the clouds themselves. AWS, GCP, and Azure will each take a support case from an individual with a credit card. The management layer that sits _above_ them mostly will not.

If you’re building a multicloud strategy, that asymmetry deserves a line in your evaluation criteria alongside features and price: **what happens when it breaks, and do I have the standing to get help?**

### [E] What Actually Works Without A Procurement Department

After checking primary pricing pages rather than vendor listicles, I found four options an individual can access without an enterprise sales relationship:

**→ Mist Hosted Edition is** a managed multicloud control plane for VM inventory, lifecycle actions, monitoring, cost visibility, scheduling, scripting, and orchestration. It has a 14-day trial, followed by usage-based billing.

**→ Vantage** has a free Starter tier covering up to $2,500 of tracked monthly cloud spend across AWS, Azure, and GCP, with cost reports and recommendations. Signup goes straight to a console.

**→ Grafana Cloud** has a free tier, no credit card, with CloudWatch, Azure Monitor, and Google Cloud Monitoring all available as built-in data sources. Three data sources, one dashboard.

**→ Steampipe + Powerpipe** is open source, nothing to sign up for at all. Query all three clouds in SQL, with pre-built dashboards for resource counts, cost, and usage.

For the optimisation recommendations that are Turbonomic’s actual differentiator, the free equivalents are each provider’s native advisor: AWS Compute Optimizer and Trusted Advisor, Azure Advisor, and GCP’s Active Assist. You lose cross-cloud normalisation and automated action-taking. That gap is real, and it’s precisely what the commercial tools charge for.

Part V | Starting… Another Dead End
-----------------------------------

### **[A]** Mist Initially Looked Like The Practical Replacement.

Its public website still advertises a **Hosted Edition** as SaaS, a **14-day free trial**, and pay-as-you-go pricing. It claims support for AWS, Azure, GCP, VMware, Kubernetes, and other infrastructure from one control plane. Exactly what I need.

But clicking **Sign up** produces a definitive message:

> **_Account creation has been disabled._**

This isn’t a temporary registration problem. The [Mist Community Edition repository](https://github.com/mistio/mist-ce) explains what the marketing site does not: **Dell Technologies acquired Mist.io Inc. in December 2023, and the Enterprise Edition and Hosted Service are no longer available.** The website, pricing page, trial offer, and signup buttons remain online even though nobody can create an account.

That makes the advertised Hosted Edition pricing academic. There is no trial to start, no credit card to enter, and no SaaS dashboard to connect to our clouds. Mist should not be included in a current shortlist of self-service multicloud platforms.

### [B] What About Mist Community Edition?

The Community Edition remains downloadable under the Apache 2.0 licence, but the same repository says it is **no longer maintained**, apart from occasional security fixes contributed by the community. It is a substantial platform rather than a desktop utility: the single-host deployment runs roughly 25 Docker containers and officially calls for at least 4 CPU cores, 8 GB RAM, 10 GB of Docker storage, and a current Debian or Ubuntu host. Components include MongoDB, RabbitMQ, Elasticsearch, InfluxDB or VictoriaMetrics, Vault, API workers, schedulers, proxies, and the web interface.

I’m not going to turn this post into a local-platform installation guide. That would shift the exercise away from multicloud management and into maintaining an unsupported management plane. More importantly, Mist would hold credentials capable of controlling resources in all three cloud accounts. Running old infrastructure components locally, without vendor support, creates a security responsibility that deserves its own isolated lab and threat model not a hurried sidebar.

Community Edition is still useful **theoretically**, however, because its architecture exposes what every multicloud management platform has to do behind the polished dashboard. The next section follows that flow without asking readers to install it or trust it with live credentials.

### [C] The Lesson

Mist adds a different failure mode to the list. Turbonomic’s trial failed after provisioning began. Mist’s discontinued trial is still advertised years after new-account creation was switched off. A polished product page is not evidence that a service is available. Test the signup path before evaluating features, designing IAM roles, or writing integration instructions.

Mist Hosted Edition cannot replace Turbonomic in this hands-on guide, and we are deliberately stopping short of deploying Community Edition. What we _can_ do is use Mist CE to understand the machinery a management platform would place between us and the three clouds.

Part VI | How Mist Community Edition Would Work
-----------------------------------------------

Although we’re not installing Mist CE in this post, its architecture is a useful model for understanding what sits behind any multicloud management console.

At a high level, the control plane would sit between the operator and the three cloud APIs:

```
                         ┌──────────────────────────┐
                         │  Mist CE control plane   │
                         │                          │
Operator ── browser ───► │ UI · API · scheduler     │
                         │ workers · databases      │
                         │ credential vault         │
                         └───────┬──────┬──────┬────┘
                                 │      │      │
                              AWS API Azure API GCP API
                                 │      │      │
                              EC2 VM   Azure VM  GCE VM
```

### [A] Deploy the Management Plane

Mist CE can run on Kubernetes with Helm or on a single Debian/Ubuntu host with Docker Compose. The single-host option starts the web interface, API, background workers, schedulers, message queue, credential vault, databases, log index, and time-series monitoring services.

This first step reveals something dashboards hide: the tool used to simplify infrastructure is substantial infrastructure itself. It needs capacity, patching, TLS, backups, log retention, monitoring, and recovery. A hosted product makes those jobs the vendor’s problem; Community Edition makes them ours.

### [B] Create a Trust Relationship with Each Cloud

The control plane cannot discover or manage anything until each provider trusts it.

The trust mechanism differs by provider.

1.  On **AWS,** Mist would use a dedicated IAM identity or assumable role to call EC2, storage, networking, tagging, pricing, and monitoring APIs.
2.  On **Azure**, it would use a Microsoft Entra application and service principal to request tokens for Azure Resource Manager and Azure Monitor.
3.  On **GCP,** it would rely on a dedicated service account to access Compute Engine, Cloud Monitoring, billing, and resource APIs.

The permissions determine what the dashboard can do. Read-only access supports inventory and observation. Lifecycle permissions allow start, stop, reboot, and resize operations. Provisioning permissions allow the platform to create and destroy infrastructure.

This is why a multicloud control plane is security-sensitive: compromising one dashboard can expose every connected environment. Good implementations use dedicated identities, least privilege, short-lived credentials where possible, encrypted secret storage, audit logs, and separate approval paths for destructive actions.

### [C] Discover and Normalize Resources

Mist’s provider adapters would poll three unrelated APIs and translate their results into a common internal model. An EC2 instance, Azure virtual machine, and Compute Engine instance all become a Mist **machine**, even though the providers disagree on names, states, metadata, network objects, disk types, regions, and billing units.

The normalization layer is the real value of a multicloud platform. Without it, the operator must remember that:

*   AWS uses tags, Azure uses tags, and GCP commonly uses labels but their rules and propagation differ.
*   Instance states that look equivalent do not always have identical billing consequences.
*   CPU, memory, disk, and network metrics come from different monitoring systems at different intervals.
*   Every provider structures accounts, subscriptions or projects, regions, zones, identities, and quotas differently.

A single inventory hides those differences from the user, but it does not eliminate them. The platform carries the complexity instead.

### [D] Translate Actions Back into Provider APIs

When an operator clicks **Stop**, Mist identifies the provider, chooses the appropriate API call, supplies the stored identity, waits for the asynchronous operation, and updates its internal state. The same visible button may invoke three completely different workflows.

That translation becomes harder for provisioning and resizing. An abstract request for “a small Ubuntu VM” still has to become an AWS instance type and AMI, an Azure VM size and image reference, or a GCP machine type and image family. Network interfaces, disks, firewalls, SSH keys, availability zones, and prices also need provider-specific treatment.

This is why multicloud management products can offer a common interface without making the underlying clouds interchangeable. The lowest common denominator is easy; preserving each cloud’s unique capabilities is not.

### [E] Collect Metrics, Costs, and Events

Mist can poll provider APIs and install an agent on managed machines to collect operating-system metrics. The control plane stores metrics in a time-series database, logs in a search index, and inventory in its primary database. Rules and schedules can then trigger alerts, scripts, or lifecycle actions.

Community Edition still offers inventory, provisioning, lifecycle actions, scripts, browser-based SSH, monitoring, schedules, audit logging, and current cost estimation. However, historical cost comparison, rightsizing recommendations, fine-grained role-based access control, governance constraints, and advanced orchestration templates belonged to the discontinued Enterprise and Hosted editions. Mist CE therefore demonstrates the mechanics of management, but it is not a feature-for-feature Turbonomic replacement.

### [F] Why We’re Stopping at the Architecture

A responsible deployment would require an isolated Linux host, a security review, TLS, restricted network access, purpose-built cloud identities, credential rotation, and a teardown plan. It would also rely on an unmaintained codebase containing aging dependencies. That is a worthwhile future homelab project, but it isn’t a sensible final step for this article.

The important point is conceptual: a **“single pane of glass”** isn’t magic. It is a privileged translation and automation layer operating three separate systems on your behalf.

Part VII: Lessons Learned!
--------------------------

The original goal was to place three comparable VMs behind one working management console, in order to observe the complexity of multicloud management. And, well, we observed alright:

### [A] **Account Creation**

Opened accounts across the major public-cloud ecosystems.

### [B] **VM Provisioning**

Created comparable Linux VMs on AWS, GCP, and Azure.

### **[C] Cross-Cloud Consistency**

Reused one SSH key and applied a common naming and tagging strategy.

### **[D] Cost Awareness**

Compared equivalent VM pricing and free-tier constraints across providers.

### **[E] Product Evaluation**

Tested the access path, provisioning process, support model, and current availability. Not just the feature list.

### **[F] Platform Architecture**

Mapped how one control plane would authenticate, discover, normalize, monitor, and act across three clouds.

### **[G] Risk Assessment**

Recognized that a central manager becomes a high-value store of credentials and authority.

The most important outcome wasn’t a screenshot. It was discovering that the difficult part of multicloud management begins _after_ the clouds are running.

Part VIII: The Complexity of…Complexity
---------------------------------------

I began this exercise expecting the hard part to be creating the same VM three times. It wasn’t. AWS, Azure, and GCP all made that possible with an individual account and a credit card.

The harder task was finding an independent management layer that an individual could actually access, provision, and support.

Turbonomic had the feature set and a public trial, but the instance failed to provision. Resolving that failure required an IBM Customer Number tied to an existing purchasing relationship.

VMware Tanzu CloudHealth routes customers through a distributor. Aria Operations has moved into VMware Cloud Foundation bundles. Flexera One is sales-led with no published self-service tier.

Mist.io still advertises a hosted trial even though Dell’s acquisition ended the hosted service and disabled account creation. Mist Community Edition is open source, but unsupported and operationally substantial.

That sequence tells us something important: **multicloud management is an enterprise category, not simply a technical category.** “Enterprise” here means more than advanced features. It means procurement channels, customer numbers, partner relationships, contracts, support entitlements, implementation services, governance teams, and enough infrastructure scale to justify another platform sitting above the clouds.

### [A] The Technical Complexity

Each provider has its own identity model, API vocabulary, resource hierarchy, tagging rules, monitoring system, pricing structure, quotas, regions, machine states, and failure behavior. A management platform must continuously translate among them while preserving enough provider-specific detail to remain useful. Every new cloud integration creates another moving API surface that the vendor must maintain.

Normalizing an EC2 instance, Azure VM, and Compute Engine instance into one object is possible. Making every networking, storage, security, billing, and lifecycle feature behave identically is not. The “single pane of glass” simplifies the operator’s view by moving complexity into adapters, databases, workers, policies, and support teams.

### [B] The Security And Operational Complexity

A centralised manager needs visibility into every connected environment and may be authorized to change or destroy resources. That makes it both valuable and dangerous. It needs least-privilege identities, encrypted credentials, TLS, audit logs, backups, high availability, patching, credential rotation, and a clear recovery process. If the manager is unavailable, stale, or compromised, the blast radius crosses cloud boundaries.

Self-hosting avoids vendor access barriers, but it does not make those responsibilities disappear. It transfers them to you. SaaS removes much of the platform maintenance, but replaces it with vendor dependency, subscriptions, data-residency questions, and a support relationship.

### [C] The Organizational Complexity

A tool can normalize APIs. It cannot automatically normalize teams. AWS, Azure, and GCP resources may be owned by different departments, funded by different budgets, governed by different policies, and operated by people with different skills. Before automation can act safely, an organization must agree on naming, tags, ownership, access, cost allocation, exceptions, and who is allowed to approve destructive changes.

This is why enterprise products emphasize governance, RBAC, audit trails, chargeback, policy engines, and support contracts. At scale, those features matter as much as the dashboard.

### [D] Multicloud Management Complexity

The dashboard experiment failed. The learning exercise didn’t.

We provisioned comparable infrastructure across three clouds, saw where their models align and diverge, and tested the market around the management layer. The result is less satisfying than a polished screenshot, but more honest: multicloud is easy to describe, possible to build, and difficult to operate well. The management platform does not remove the multicloud tax, it becomes part of it.

For an individual learner, the practical path is to master each provider’s native tools, adopt consistent naming and tagging, use open standards where possible, and add centralized tooling only when the operational need justifies its cost and trust requirements.

For an enterprise, the selection criteria must go beyond features: availability, support entitlement, integration maintenance, security architecture, exit strategy, and the ability to get help when provisioning fails all belong in the decision.

That is where this hands-on investigation ends. We won’t force an unsupported local deployment just to manufacture a screenshot. But, lesson.

Part IX: Observability Is Not Quite Management
----------------------------------------------

There is also an uncomfortable gap between **multicloud observability** and genuine **multicloud management**. The tools an individual can access Grafana Cloud, Vantage, Steampipe, and native billing exports are good at showing resources, metrics, costs, and policy violations in one place. They answer _What do we have?_, _What is it costing?_, and _What looks unhealthy?_

But observing three clouds is not the same as operating them. Genuine management means safely provisioning, resizing, patching, networking, governing, and deleting resources through one control plane while preserving each provider’s unique behavior. That capability is concentrated in the expensive enterprise products we couldn’t access.

In practice, many organizations may have a shared observability or FinOps layer but still need distinct AWS, Azure, and GCP expertise underneath it. The single dashboard may be operated by one person. Resolving what it reports could still require three engineers — one who speaks IAM and CloudFormation, one who speaks Entra ID and ARM, and one who speaks service accounts and Cloud Resource Manager.

**Multicloud doesn’t necessarily reduce dependence on specialists. Sometimes it multiplies them by three.**

Part X: ⚠️ Cleanup Protocol
---------------------------

If you no longer need the VMs, remove them to avoid unexpected charges.

### **AWS**

```
aws ec2 terminate-instances --instance-ids <your-instance-id>
# Or: EC2 Console → Select instance → Instance state → Terminat
```

### **GCP**

```
gcloud compute instances delete multicloud-gcp --zone=<your-zone>
# Or: Compute Engine Console → Select VM → Delete
```

### **Azure**

```
az group delete --name multicloud --yes
# Or: Portal → Resource groups → multicloud → Delete
```

If you created any experimental IAM roles, service principals, service accounts, access keys, or downloaded JSON credentials while evaluating management products, delete or revoke those separately. Removing a VM does not remove its external management identities.

> **_💡 You can stop the VMs instead of deleting them if later posts will reuse them. Stopped VMs do not incur compute charges, but disks, reserved IP addresses, snapshots, and other attached resources may continue billing._**

### References

Comparison of AWS Outposts, Azure Arc, and Google Anthos approaches to hybrid and multicloud management.
--------------------------------------------------------------------------------------------------------

### [**A guide to the multicloud strategies of AWS, Azure, and Google Cloud**](https://infoworld.com/article/4048525/a-guide-to-the-multicloud-strategies-of-aws-azure-and-google-cloud.html)

> _Experts advise choosing AWS if you want a broad array of services, require the latency afforded by global infrastructure networks, flexibility to build more complex cloud environments and highly customized apps, and are looking for a wider variety of tools._ **_— Taryn Plumb_**

Google’s architecture guide for “single pane of glass” observability across hybrid and multicloud environments.
---------------------------------------------------------------------------------------------------------------

[**Hybrid and multicloud monitoring and logging patterns**](https://cloud.google.com/solutions/hybrid-and-multi-cloud-monitoring-and-logging-patterns)

> _In a_ **single pane of glass** _architecture, all monitoring and logging is centralized, with the aim of providing a single point of access and control._
> 
> _In a_ **separate application and operations** _architecture, sensitive application data is segregated from less sensitive operations data, with the aim of meeting compliance requirements for sensitive data._ **_— Google Cloud_**

Microsoft’s framework for planning and executing hybrid and multicloud adoption with Azure Arc
----------------------------------------------------------------------------------------------

### [Unified hybrid and multicloud operations](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/scenarios/hybrid/strategy)

> _The challenge is to unify these environments in a secure, well-managed way that enables modernization from cloud to edge. This guidance provides a prescriptive end-to-end framework for unifying and managing hybrid and multicloud environments with Azure as the central control plane._ **_— Microsoft Learn_**

AWS’s own guidance on when multicloud makes sense and how to approach it strategically.
---------------------------------------------------------------------------------------

### [**Proven practices for developing a multicloud strategy**](https://docs.aws.amazon.com/prescriptive-guidance/latest/strategy-multicloud/introduction.html)

> _This paper presents nine proven tenets for multicloud success based on our experiences with AWS enterprise customers. Each tenet addresses a critical aspect of multicloud strategy, from aligning business goals to security implementation. By applying these principles, organizations can navigate multicloud complexity with confidence. —_ **_Tom Godden and Ellie Tamari, Amazon Web Services_**

Comprehensive overview of the multicloud management tooling landscape
---------------------------------------------------------------------

[**20+ Top Multi-Cloud Management Platforms & Tools in 2026**](https://spacelift.io/blog/multi-cloud-management-platforms)

> _You’re running workloads across AWS, Azure, and Google Cloud. Every team picked a different tool to manage their slice, and policy enforcement, cost visibility, and provisioning workflows have splintered along with them. Multicloud management platforms exist to put that back together without forcing everyone onto one cloud._ **_— Mariusz Michalowski_**

Analysis of why fragmented visibility across platforms creates business risk and how to achieve comprehensive observability.
----------------------------------------------------------------------------------------------------------------------------

### [**Achieving visibility in hybrid and multi-cloud environments**](https://www.ibm.com/think/insights/visibility-hybrid-multicloud-environment)

> _When visibility is fragmented across platforms, tools and teams, enterprises face growing complexity, rising costs and slower response times. What begins as a technical inconvenience can quickly snowball into a business risk, impacting uptime, compliance and innovation. Let’s explore what comprehensive visibility entails, why it matters and how to achieve this effectively for hybrid and multicloud environments._ — **_Vikas Makkar_**

How AIOps and generative AI are being applied to multicloud complexity, including centralized observability and security posture management.
--------------------------------------------------------------------------------------------------------------------------------------------

### [**7 ways to tame multicloud chaos with generative AI**](https://www.infoworld.com/article/4130320/7-ways-to-tame-multicloud-chaos-with-generative-ai.html)**’**

> _Generative AI tools, including_ [_AI copilots_](https://www.cio.com/article/1309604/generative-ai-copilots-whats-hype-and-where-to-drive-results.html) _and_ [_AI agents_](https://drive.starcio.com/2025/10/ai-agents-definitive-guide-saas-security-titans/)_, are also becoming invaluable._ [_World-class IT departments_](https://www.cio.com/article/4064313/what-world-class-it-looks-like-in-the-gen-ai-era.html) _are using genAI to_ [_write agile requirements_](https://www.infoworld.com/article/3980319/how-to-use-genai-for-requirements-gathering-and-agile-user-stories.html)_,_ [_develop software_](https://www.infoworld.com/article/3993479/what-we-know-now-about-generative-ai-for-software-development.html)_,_ [_automate testing_](https://www.infoworld.com/article/3711865/5-ways-qa-will-evaluate-the-impact-of-new-generative-ai-testing-tools.html)_, and_ [_maintain documentation_](https://www.infoworld.com/article/4063551/how-to-improve-technical-documentation-with-generative-ai.html)_._ **_—_** [**_Isaac Sacolick_**](https://www.infoworld.com/profile/isaac-sacolick/)

![Multicloud Management — The Complexity of Multicloud Architecture](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*YJtLujCrZKLKb-rr9M0scg.png)

---

# The Original

**Blog:** [StudentAnalyst](https://medium.com/studentanalyst)
<br>
**Article Link:** [Multicloud Management](https://medium.com/studentanalyst/towards-multicloud-26ad5c69f4d5)
<br>
Originally Published by [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona) 
<br>
**22 August 2026**
