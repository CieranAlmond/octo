# 🐙

# Octopus Energy Technical Task  
### Cieran Almond

*You have just joined a very fast growing startup as the only security person. The company has roughly 100 employees and the CTO has been making decisions about what is needed based on function. Security is not always considered.*

*You’ve been hired by the CTO for your security knowledge and because you’ll have a different perspective and priorities.*

*The company has built a custom CRM solution that it sells to clients. It is hosted in AWS and they use CI/CD tooling to make a handful of production changes per day. Any other services they need to run (email, office productivity, etc.) are bought as SaaS services. Staff are encouraged to buy their own IT (like laptops and accessories) and expense it.*


<h1><span style="color:#D6336C;">How would you identify and prioritise any potential security problems?</span></h1>

# Initial thoughts / assumptions being made from the initial read:

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

# AWS Architecture:
- Any architecture diagrams that illustrate the CRM solution?
- How are we selling the CRM solution to customers? Are we exposing any endpoints?
- How is authentication handled?

# AWS Account(s):
- IAM user roles and permissions, who has access to what and why. Are there any overreaching permissions?
- MFA, is MFA required to access AWS accounts? Do we have other ISPs (OKTA,PING) that can authenticate users securely using other authentication methods (SSO)?
- Network segregation - VPC architecture, security groups
- Encryption - especially in the context of customer PII, are RDS/S3’s encrypted by default? What protocols are being used?
- Logging and monitoring - thinking is cloudtrail, cloudwatch, guardduty enabled? Where are our logs and what are we alerting on (if anything)
- Availability - do we have any redundancy in our deployment, what geographical area are we deployed to? Do we take backups?
- Secrets - how are production secrets being handled? 

# CI/CD:
- Who has permissions to push to prod? Is there a review cycle involved in this, or can anyone commit and merge? 
- Do we perform any SAST/DAST scanning in the build pipeline to check for packages or secrets being pushed to public repos?
- Do we have any environment separation? Ie do we have a prod/test environment. Do they actually mirror each other? 




# Company Assets / Third Parties:
- BYOD - do we have any controls on users BYOD devices?
- Do we have any visibility into the assets we own?
- Are laptops encrypted?
- Are laptops updated? Do software packages get updated?
- Is Antivirus/DLP deployed? 
 -Do we have any MDM solutions to containerise company assets?
 -JML process. What happens when a user leaves? Does company data get deleted?
 -Do we have an asset list of SaaS solutions we use?
 -What data are we sharing with these SaaS tools? How is the data being shared? What type of data is it? What are the volumes

Identifying a lot of these problems would likely involve speaking to SME’s in respective business areas, so sit-down sessions asking “can you walk me through how you do x?” , or “how do you do y?”. If possible I would lean on any documentation, policies or procedures to help answer these questions. 

<h1><span style="color:#D6336C;">Making some assumptions about what you might expect to find, what are the most important controls you would look to implement?
</span></h1>

In terms of prioritisation, using a risk x likelihood method I would prioritize dependent on the answers given in part one, which would look something like: 

High Priority

- Phishing program to better educate users (as this is a common attack vector)
- Encrypt databases containing PII
- Protect assets by deploying MDM solution. Establish a JML process for safe return of assets, or perform remote wipes to ensure company data is deleted. Deploy AV on company machines
- Scan public repos to ensure no secrets in plaintext in code
- Ensure MFA is enabled for users accessing company assets and data

Medium Priority

- Enable logging and start creating alerts for key indicators of compromise
- Work towards getting company issued machines. Create an image that builds in security controls. Have a VPN/AV/DLP deployed by default
- Introduce a change process for deploying. At least have a peer review of deployments to prevent damaging codebase.
- Perform IAM reviews on a monthly/quarterly basis depending on permissions granted.#
- Establish an asset inventory / list. 


Low Priority

- Vendor risk - obtain security attestations, check scope of systems being procured
- Build policies / procedures to better govern JML, Data Governance, etc
- Documentation / diagramming of AWS architecture
- Build a medium to long term security roadmap
 -Create a high level infosec policy, issue guidance on best practise (password length, data sharing, etc) - have this socialised during onboarding or within a HR platform
 -Consider scoping the company against a security standard (CE, ISO, etc) to establish a baseline


Again not an exhaustive list, but just a few examples from each area identified during the scoping stage. 

 
