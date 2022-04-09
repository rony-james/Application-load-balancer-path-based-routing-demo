# Application-load-balancer-path-based-routing-demo
Path-based routing is one of the unique feature offered by ALB. Path-based routing is also referred as URL based routing. The Application load balancer will forward the requests to the specific targets based on the Rules configured in the Load balancer. 

DIAGRAM
=========
![alt text](https://github.com/rony-james/Application-load-balancer-path-based-routing-demo/blob/main/DIAGRAM.jpg?raw=true)


# Configure Path-based Routing on Application Load balancer
## My Environment Setup
- VPC
- EC2 instances
- ALB
- Target Groups
- AWS Certificate Manager
- Route53



[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

Step 1: Created a public hosted zone on Route53 for "rony.website". The nameserves of the domaon "rony.website" changed as mentioned on the public hosted zone.
![alt text](https://github.com/rony-james/Application-load-balancer-path-based-routing-demo/blob/main/53.png?raw=true)


Step 2: Initiated a Certificate request for the domain "rony.website"
![alt text](https://github.com/rony-james/Application-load-balancer-path-based-routing-demo/blob/main/Certificate.png?raw=true)

Step 3: Created a Security Group for This project.

Step 4: Created 3 EC2 Instances and installed httpd service.
![alt text](https://github.com/rony-james/Application-load-balancer-path-based-routing-demo/blob/main/EC2.png?raw=true)

Step 5: Create the Target Groups for 3 EC2 instances. Once It's created, register the corresponding EC2 with Target Group.
![alt text](https://github.com/rony-james/Application-load-balancer-path-based-routing-demo/blob/main/TG.png?raw=true)

Step 6: Create an ALB. we can mention both 80 and 443 listener. If the AWS Ssl certificate is ready to use, we can attach the certificate details during the time of ALB creation.
![alt text](https://github.com/rony-james/Application-load-balancer-path-based-routing-demo/blob/main/LB.png?raw=true)

Step 7: Rule set creation on ALB. Here we can create path based rule set for redirecting the request to corresponding Target Group. The rules we have configured for the Path based routing are an Exact Match.
For this project , We have configured rules to forward the requests from the Users to a definite Path (/credit & /debit). But There are some cases where the users requests for an information which is further down the path such as /credit/cibil and /debit/data. So In this case We have to configure a rule for the path with the wildcard , This will ensure that the any other information under this path is served for the users properly. During that time we can use wildcard as /credit* or /debit*.

![alt text](https://github.com/rony-james/Application-load-balancer-path-based-routing-demo/blob/main/rule-set.png?raw=true)

Step 8: Creating Record on Route53.
![alt text](https://github.com/rony-james/Application-load-balancer-path-based-routing-demo/blob/main/53-alias.png?raw=true)

![alt text](https://github.com/rony-james/Application-load-balancer-path-based-routing-demo/blob/main/53-records.png?raw=true)


## Working Procedure.

- In this environment, the domain "rony.webiste" using aws Name Servers. We need to forward the traffics to the 3 EC2 instances by the help of Application Load Balancer. 
- The Rout53 configured with an alias which will leads the requests to the ALB.
- Once the ALB got the request, It will be evaluate the rule set for matching the received request. As per our senario, we have 3 target groups for 3 Instanceses. If the request path contain "rony.website", the default rule set will be activated and  the that request will be passes to the Traget group "rony". The "rony" Target Group associated with first instance which will serve the "rony.website". 
- If the incomming request contain /credit, the application load balancer will activate the corresponding rule set and forward the request to the Target Group "credit". The credit Target Group has been atached with next EC2 which contain the credit details.
- Same as above if the request contain /debit, ALB will active next rule set for the debit Target Group. Request will be served by the registred EC2 that attached with "debit" Target Group.
- SSL certificate will be attached with ALB and the ssl termination process will happen between client meachine and ALB.

