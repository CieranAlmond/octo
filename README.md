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



 
