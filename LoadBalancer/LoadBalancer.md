💡 What is a Load Balancer?
A Load Balancer is like a traffic police officer that directs vehicles (requests) to the right lanes (servers) so that no single lane gets overloaded.
In AWS, a Load Balancer automatically distributes incoming network traffic across multiple EC2 instances (servers) to make sure your application:
Runs faster ⚡
Doesn’t crash under heavy load 💪
Keeps running even if one server fails 🛠️

    ******************************
🧠 Simple Example

Imagine you run a website — www.myshop.com
 — and it has 3 EC2 instances running the same code:
EC2 #1
EC2 #2
EC2 #3
Without a Load Balancer:
All users might hit EC2 #1, causing it to overload, crash, and make your website slow or unavailable.

With a Load Balancer:
User 1 → EC2 #1
User 2 → EC2 #2
User 3 → EC2 #3 And so on...
The Load Balancer distributes traffic evenly among all EC2s.
If EC2 #2 fails, the Load Balancer automatically stops sending traffic to it and sends users to EC2 #1 and #3 instead

        *************************
🏬 Real-Life Example
Think of a restaurant with 3 chefs (servers):
Without a manager (load balancer):
Customers go randomly to any chef. One chef gets 10 orders, others get none → slow service.
With a manager (load balancer):
The manager assigns customers evenly — 1 to each chef → faster and smoother operation.
AWS Load Balancer = that manager distributing requests to chefs (EC2s).

**************************************************

🧩 Types of Load Balancers in AWS
AWS offers different types, each for different needs:
Application Load Balancer (ALB) → for web apps (HTTP/HTTPS traffic).
Example: Routing traffic between user.myapp.com and admin.myapp.com.
Network Load Balancer (NLB) → for high-speed, low-latency connections (TCP/UDP).
Example: Gaming servers or financial apps.
Gateway Load Balancer (GLB) → for routing traffic through security tools.
Example: Sending traffic through firewalls or monitoring tools.

