# 🐙 Octopus Energy Technical Task - Cieran Almond


🚀*You have just joined a very fast growing startup as the only security person. The company has roughly 100 employees and the CTO has been making decisions about what is needed based on function. Security is not always considered.*🚀

*You’ve been hired by the CTO for your security knowledge and because you’ll have a different perspective and priorities.* 🎉

*The company has built a custom CRM solution that it sells to clients. It is hosted in AWS and they use CI/CD tooling to make a handful of production changes per day. Any other services they need to run (email, office productivity, etc.) are bought as SaaS services. Staff are encouraged to buy their own IT (like laptops and accessories) and expense it.*


<h1><span style="color:#D6336C;">Question: How would you identify and prioritise any potential security problems❓</span></h1>

# Initial thoughts / assumptions being made from the initial read 🧠:

- Small org and immature functions, first security hire. Have to be pragmatic with solutions and with what is addressed based on resource available 
- AWS architecture probably would need a review, as there likely wouldn’t have had security implementations 
- CI/CD would probably need a review, assuming it's to a github repo. Who can make deployments? What testing is performed? Change process/ 2 eyes reviews?
- Potentially would need to get a handle on third parties being used. What data are we sending these third parties? How is that being protected? On a light touch might have to ascertain security artifacts/trust center to see SaaS products we are using are in scope and assessed
- Laptops IT. Review of how this is being managed. Is there an asset list or inventory. Would look to deploy MDM solutions using SaaS (Azure InTune) in order to protect assets. Seems like employers can work from home, how do we securely connect to corp network, VPN? Also think about Antivirus, DLP.
- Assuming Phishing training is not being performed at this time. 

# Approach:

My approach would take into consideration the size and resource of the company and the infosec team (me). I am also taking into consideration that the CRM solution we are selling would contain customer data containing PII. Reputation is likely an important factor during this “growth stage” of the journey. The approach I would take would focus less on governance and establishing processes, and more focus on reducing the immediate risk based on the scenario. Establishing good practice, process and procedure would be a later goal. I am again assuming there is little or no documentation so would start with the following:

Start with a quantitative approach to identifying the key risks from a scoping operation. For this exercise the scope would be similar to my “initial thoughts” and would look to encompass 
- A review of AWS 
- A review of our CI/CD and deployment pipelines
- A review of third parties and company assets 

Expanding further, things I would be considering for each of the above bulletpoints:

# AWS Architecture 🎯:
- Any architecture diagrams that illustrate the CRM solution?
- How are we selling the CRM solution to customers? Are we exposing any endpoints?
- How is authentication handled?

# AWS Account(s) 🎯:
- IAM user roles and permissions, who has access to what and why. Are there any overreaching permissions?
- MFA, is MFA required to access AWS accounts? Do we have other ISPs (OKTA,PING) that can authenticate users securely using other authentication methods (SSO)?
- Network segregation - VPC architecture, security groups
- Encryption - especially in the context of customer PII, are RDS/S3’s encrypted by default? What protocols are being used?
- Logging and monitoring - thinking is cloudtrail, cloudwatch, guardduty enabled? Where are our logs and what are we alerting on (if anything)
- Availability - do we have any redundancy in our deployment, what geographical area are we deployed to? Do we take backups?
- Secrets - how are production secrets being handled? 

# CI/CD 🎯:
- Who has permissions to push to prod? Is there a review cycle involved in this, or can anyone commit and merge? 
- Do we perform any SAST/DAST scanning in the build pipeline to check for packages or secrets being pushed to public repos?
- Do we have any environment separation? Ie do we have a prod/test environment. Do they actually mirror each other? 




# Company Assets / Third Parties 🎯:
- BYOD - do we have any controls on users BYOD devices?
- Do we have any visibility into the assets we own?
- Are laptops encrypted?
- Are laptops updated? Do software packages get updated?
- Is Antivirus/DLP deployed? 
 -Do we have any MDM solutions to containerise company assets?
 -JML process. What happens when a user leaves? Does company data get deleted?
 -Do we have an asset list of SaaS solutions we use?
 -What data are we sharing with these SaaS tools? How is the data being shared? What type of data is it? What are the volumes

📝 Identifying a lot of these problems would likely involve speaking to SME’s in respective business areas, so sit-down sessions asking “can you walk me through how you do x?” , or “how do you do y?”. If possible I would lean on any documentation, policies or procedures to help answer these questions. 

<h1><span style="color:#D6336C;">Question: Making some assumptions about what you might expect to find, what are the most important controls you would look to implement❓
</span></h1>

In terms of prioritisation, using a risk x likelihood method I would prioritize dependent on the answers given in part one, which would look something like: 

# 🔴High Priority

- Phishing program to better educate users (as this is a common attack vector)
- Encrypt databases containing PII
- Protect assets by deploying MDM solution. Establish a JML process for safe return of assets, or perform remote wipes to ensure company data is deleted. Deploy AV on company machines
- Scan public repos to ensure no secrets in plaintext in code
- Ensure MFA is enabled for users accessing company assets and data

# 🟠Medium Priority

- Enable logging and start creating alerts for key indicators of compromise
- Work towards getting company issued machines. Create an image that builds in security controls. Have a VPN/AV/DLP deployed by default
- Introduce a change process for deploying. At least have a peer review of deployments to prevent damaging codebase.
- Perform IAM reviews on a monthly/quarterly basis depending on permissions granted.#
- Establish an asset inventory / list. 


# 🟢Low Priority

- Vendor risk - obtain security attestations, check scope of systems being procured
- Build policies / procedures to better govern JML, Data Governance, etc
- Documentation / diagramming of AWS architecture
- Build a medium to long term security roadmap
 -Create a high level infosec policy, issue guidance on best practise (password length, data sharing, etc) - have this socialised during onboarding or within a HR platform
 -Consider scoping the company against a security standard (CE, ISO, etc) to establish a baseline


Again not an exhaustive list, but just a few examples from each area identified during the scoping stage. 

---

🚀*The company has been a success and now has over 5000 employees. The CRM solution they built, AWS environment and CI/CD tooling have scaled well and they are now making over 100 production changes per day. In order to expand internationally they have bought several smaller companies around the world.*

  *The company now has much bigger clients and they are taking an interest in how security is managed, meaning some subsidiaries now need to achieve SOC 2 or ISO 27001 certification. At the same time the CTO is keen to ensure the company stays “tech-first” in its approach to security, and avoid introducing manual or inefficient GRC processes.* 🚀


<h1><span style="color:#D6336C;">Question: Given the changes to the company, what (if anything) changes about your answers to the questions in the first part❓ 
</span></h1>


With the context of the organisation now being much larger, more mature, we should shift our approach from identifying the most pressing risks and firefighting them as a priority, to a more governance approach. 

So if we revisit the prioritisation list:

# 🔴High Priority

- Phishing program to better educate users (as this is a common attack vector)
- Encrypt databases containing PII
- Protect assets by deploying MDM solution. Establish a JML process for safe return of assets, or perform remote wipes to ensure company data is deleted. Deploy AV on company machines
- Scan public repos to ensure no secrets in plaintext in code
- Ensure MFA is enabled for users accessing company assets and data

# 🟠Medium Priority

- Enable logging and start creating alerts for key indicators of compromise
- Work towards getting company issued machines. Create an image that builds in security controls. Have a VPN/AV/DLP deployed by default
- Introduce a change process for deploying. At least have a peer review of deployments to prevent damaging codebase.
- Perform IAM reviews on a monthly/quarterly basis depending on permissions granted.#
- Establish an asset inventory / list. 


# 🟢Low Priority

- Vendor risk - obtain security attestations, check scope of systems being procured
- Build policies / procedures to better govern JML, Data Governance, etc
- Documentation / diagramming of AWS architecture
- Build a medium to long term security roadmap
 -Create a high level infosec policy, issue guidance on best practise (password length, data sharing, etc) - have this socialised during onboarding or within a HR platform
 -Consider scoping the company against a security standard (CE, ISO, etc) to establish a baseline

What I would expect now is that the items considered lower priority would now invert. What we would now be looking to do is build good governance, operate against frameworks, perform horizon scanning (for future regulatory/security compliance obligations), with the assumption that those higher priority items have now been remediated.

We should now look to build centralised, easily accessible Policies, Procedures, and Guidelines. These should have controls mapped to test effectiveness (either in the form of traditional GRC or GRC Engineering), have established a formal risk process and risk register, and have a way to track these risks.

One new challenge being faced is that it's likely now the main organisation is operating effectively, but the subsidiaries or acquisitions probably don’t align to the same governance the main org is, so the new challenge would be building a framework that allows you to better integrate subsidiaries into the governance and control frameworks of the main organization. 

Another challenge is the company size likely has dedicated resources just for more niche parts of the business, such as regulatory compliance obligations. How does the organisation remain compliant with GDPR? Has the company expanded internationally? Would we now have to comply with their regional regulatory compliance obligations, ie APRA for Australia, EU DORA, etc?. These are the new challenges and questions I'd expect to be asked as a high priority. 

<h1><span style="color:#D6336C;">Question: What do you think will be the biggest challenges, for a startup that’s grown quickly, in getting security certifications such as ISO 27001❓ 
</span></h1>

ISO27001 requires a well documented and process driven framework that effectively illustrates controls and controls owners operating them effectively.  

Drawing from performing the CE gap analysis at my current org, the challenges we faced could be broken down into a few categories.

# Documentation📝: 
Documentation either is few and far between for operating processes, or if a process is well documented, operates in silos and therefore no other teams have visibility. 

For a startup company, trying to introduce formal policies and procedures that are operated centrally can be seen as something bureaucratic that isn’t helping drive growth or mission success. The other challenge will also be building the guardrails to effectively govern the policies being introduced, as these also likely don’t exist in the current setup. A gap analysis would have to be performed to identity non conformities/gaps against ISO27001 processes, and then buy-in would be needed from teams operating ineffective processes to make technical changes to address the gaps. 

# Tech💻:
Again, from a lack of central governance of what “good” looks like, it’s highly likely the product has been built around multiple different tech stacks, backup processes, security processes, etc. 
The solution being again, formal documentation needs to establish good SDLC practices, Patch Management, etc. to better govern these processes. Again controls need to be implemented to make sure governance is effective. Procedures should look to encourage standardisation and can perhaps reference out to playbooks in a Jira/Git repo as a point of reference to standardised deployments. These playbooks can have CIS benchmarks baked in to offer a baseline level of security. 

# Resource🕵️:
It is highly likely that for a startup, there are people wearing many hats. This means that when it comes to implementing technical controls that align to a standard, they just may not have the capacity. The challenge here being there will need to be a driving factor to convince teams to perform implementation work, against what they likely consider higher priority items.

# Risk⚠️:
ISO27001 will fundamentally change the way the company thinks about risk, and it's entirely probable that risk hasn’t been much of a thought during the growth stages. Since ISO27001 has a hard requirement to operate a form of risk register the idea is to think about risk before it materialises, and how we can better manage risks by operating controls to reduce its inherent impact.  The hard part again is this is probably seen as a bureaucratic process, but if done right, it can help reduce firefighting efforts teams are likely wasting resources on, and better enable decision making as we can make a more informed decision from a security perspective. 

# Culture🚀:
Management buy-in. Ultimately it’s critical to get management buy-in for a fast paced startup. Without management help, it’s very difficult to achieve any of the above mentioned points. The difficulty to convince management would be the why. Why are we spending time and resources to implement these controls, to align to this standard? The why can be supported by board objectives or KPI’s; for example we can reduce overall risk of a cyber attack or material loss resulting in financial or reputational damage. Having an ISO27001 can be used as a driving force to present the company in a positive light, as it is internationally recognised as a baseline, and can be used to drive more sales. Usually you can make it more relatable by telling a story of what happened to x company (in a similar industry) and how ISO27001 saved them from x attack, or positively resulted in more sales.  

Employee buy-in. This would just represent an overall culture shift. Again it’s important to communicate the why though this might look slightly different to the why of management. As an example, to a devops team, this can be demonstrated by showing the effectiveness of having centralised playbooks with prebaked CIS benchmarks in an ansible playbook. This saves devops teams time deploying these manually, and saves time overall by having standardisation meaning they don’t have to write custom scripts every time they deploy. 

<h1><span style="color:#D6336C;">Question:How would you introduce GRC requirements and initiatives while minimising manual processes❓
</span></h1>


I think the key here is to sell the idea of GRC engineering to management, and then stakeholders. In theory it should be a good sell as you are presenting the following options

> operate a manual GRC process, with a GRC tool or spreadsheet. Have GRC analysts chase engineering teams, HR, Legal, Privacy, etc asking for screenshots, which takes away time from teams in order to satisfy compliance obligations.

> perform GRC engineering. Have GRC analysts get all the data they need in either a code, low code or SaaS tool. This upskills your GRC team, reduces strain on other teams, and also improves GRC from a just in time / point in time compliance obligation into a continuous monitoring program that effectively operates controls. Improved security. 

In the context of the scenario "subsidiaries now need to achieve SOC 2” presents a challenge in itself since our main org is heavily SaaS oriented, so it would have lended itself to an out of the box buy side GRC tool such as Vanta or Drata. However, it’s highly likely that the subsidiaries operate separate processes that don’t necessarily follow a normal workflow, or don’t rely on a SaaS solution (could be onprem). In this case then integrating GRC buy side tools becomes an issue as their out of the box API’s wouldn’t be able to work. 

The two options I see:

- Use a GRC SaaS tool for the main org (which by the scenario would fit very well). Perform a gap analysis on the subsidiary to understand what systems they are using, and eventually migrate over to the tools the main org is using. This way we achieve a single view, while also achieving added benefits of not having to operate effectively 2 control sets (one for the subsidiary, one for the main org). We can rely entirely on the main orgs controls to manage this now integrated subsidiary. 

- Consider a more flexible option like JupiterOne, Backstage, or use policy-as-code or open source alternatives for different use-cases. 

Ultimately regardless of the implementation a mapping of SOC 2 Trust Services Criteria to our controls would take place. With these control descriptions we can contextualise how these apply to our business, and then perform either API calls to get the data in real time or make queries to get data to perform continuous monitoring of these controls. There are considerations that would have to take place regarding the permissions assigned to analysts in terms of what they are allowed to view and get, but this could be solved through just in time access or time based access tokens if needed. 

This creates an automated workstream that requires very little manual work once set up, and places less resource burden on the stakeholders of the GRC team. 
