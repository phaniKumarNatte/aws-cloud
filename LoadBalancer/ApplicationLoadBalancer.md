💡 What is an Application Load Balancer (ALB)?
An Application Load Balancer (ALB) is a smart traffic manager that works at the application level (Layer 7) — meaning it understands HTTP and HTTPS (the language of websites).
It not only distributes traffic across servers but also decides where to send each request based on the content — like the URL, domain name, or even data in the request.

🧠 Simple Explanation
Think of ALB like a receptionist in a big company 🏢:
When a visitor comes in (user request), the receptionist asks,
“Which department do you want?”
and directs them to the right floor (server).
In AWS:
The Application Load Balancer does the same —
when users visit your website, it looks at the request and routes it to the right EC2 instance or microservice.

💻 Real-Time Example
Let’s say you have a website:
www.mycompany.com
You have different parts of your app:
/user → handled by User Service EC2
/admin → handled by Admin Service EC2
/api → handled by API Service EC2
You set up an Application Load Balancer in front of them.

Now:
When someone visits www.mycompany.com/user
👉 ALB sends that request to the User Service EC2.
When someone visits www.mycompany.com/admin
👉 ALB sends it to the Admin Service EC2.
When someone visits www.mycompany.com/api
👉 ALB sends it to the API Service EC2.
So ALB doesn’t just split traffic —
it’s smart enough to route requests based on the path, domain, or headers.
**************************************************
⚙️ What is Scaling?
Scaling means increasing your system’s capacity to handle more users or more work.
When your website or app gets popular, more people start visiting — your servers must handle the extra load.

There are two ways to scale:
Vertical Scaling (Scale Up)
Horizontal Scaling (Scale Out)
**************************************************

🏗️ 1. Vertical Scaling (Scale Up)
💡 Simple Meaning:
Add more power (CPU, RAM, Storage) to your existing server.
Think of it like upgrading your laptop:
If it’s slow, you add more RAM or a faster processor.
It’s still the same laptop, just more powerful.

🧠 Example:
You have one EC2 instance (server):
Initially: t2.micro (1 CPU, 1 GB RAM)
Now traffic increases 🚀
You upgrade it to: t2.large (2 CPU, 8 GB RAM)
That’s vertical scaling — same server, just stronger.
⚠️ Limitation:
Every server has a maximum capacity (you can’t keep upgrading forever).
If that one server crashes — your app goes down 😬

**************************************************
🌐 2. Horizontal Scaling (Scale Out)
💡 Simple Meaning:
Add more servers instead of upgrading one.
Think of it like hiring more people instead of making one person do all the work.

🧠 Example:
You have 1 EC2 instance handling your website.
As more users come:
You launch 2 more EC2 instances.
Use a Load Balancer to distribute traffic among them.
Now 3 servers handle users together → better performance & no single point of failure.
If one instance fails, others keep working ✅
That’s horizontal scaling.

**************************************************

🏬 Real-Life Analogy : 🍔 Restaurant Example

Vertical Scaling:
You hire a super chef who can cook faster and handle more orders.
But one chef can only do so much — if he’s sick, the kitchen stops.

Horizontal Scaling:
You hire more chefs.
Each chef handles fewer orders, and if one is sick, others continue cooking.
You can easily add or remove chefs as customer load changes.

**************************************************

💡 What is a Target Group?
A Target Group in AWS is a collection of targets (servers) — usually your EC2 instances — that a Load Balancer sends traffic to.
Think of it like a contact list 📞 for your Load Balancer:
The Load Balancer doesn’t directly know about every EC2 instance.
Instead, it sends traffic to a Target Group, and that Target Group contains the list of EC2s it can forward traffic to.

🧠 Simple Example

Let’s say you have:
3 EC2 instances running your website.
1 Load Balancer (ALB).
Now, you create a Target Group and add those 3 EC2 instances inside it.

When a user visits your site:
The Application Load Balancer receives the request.
It looks at the rule (e.g., send /user traffic to the “User Target Group”).
Then, it forwards that request to one of the EC2s in that Target Group.

**************************************************

💡 What is a Health Check?

A Health Check is a way for AWS (especially a Load Balancer) to check if your server (EC2 instance) is working properly or not.
If the server is healthy ✅ → AWS sends traffic to it.
If the server is unhealthy ❌ → AWS stops sending traffic to it automatically.
So basically, it’s a safety system that makes sure users are only sent to servers that are alive and working fine

🧠 Simple Explanation

Imagine you have 3 EC2 instances behind a Load Balancer (LB).
The LB keeps asking each server:
“Hey, are you okay? Can you respond?”
It does this by sending a small test request (like visiting a URL, e.g., /health or /index.html) every few seconds.
If the server replies with “Yes, I’m fine” (HTTP 200 OK) → ✅ Healthy.
If it doesn’t reply or gives an error (like 500, timeout, etc.) → ❌ Unhealthy.

The Load Balancer then:
Sends traffic only to the healthy servers
Avoids unhealthy servers until they recover
**************************************************

⚙️ Health Check Settings (in AWS)

When you set up a health check, you configure:
Protocol → HTTP, HTTPS, or TCP
Path → Example: /, /health, or /index.html
Interval → How often to check (e.g., every 30 seconds)
Unhealthy threshold → After how many failures to mark it unhealthy
Healthy threshold → How many successes before marking it healthy again

**************************************************


⚙️ 1. Interval — "How often should I check?"
Interval means how often AWS sends a health check request.
Example:
Interval = 30 seconds →
AWS sends a check every 30 seconds to your EC2.

********************************************************************
👉 Healthy Threshold = how many times your server must pass before it’s marked healthy again.
When a server was unhealthy before, AWS doesn’t mark it healthy again after just one success.
It waits for a certain number of consecutive successful checks.
Example:

Healthy Threshold = 3
Interval = 30 sec
EC2 passed 3 checks in a row →
✅ AWS marks it as healthy (after 90 seconds total).
********************************************************************
⚙️ 3. Unhealthy Threshold — "How many times must it fail to be called unhealthy?"
Similarly, if one check fails, AWS doesn’t immediately assume the server is dead (maybe it was just a network glitch).
Example:

Unhealthy Threshold = 2
Interval = 30 sec
EC2 fails 2 checks in a row →
❌ AWS marks it as unhealthy (after 60 seconds total).
********************************************************************
what is "Nested Round Robin" and "Least Outstanding Requests" ?

When a Load Balancer (like Application Load Balancer) has multiple targets (EC2 instances) in a Target Group,
it needs to decide which EC2 instance should handle the next request.
That decision is made using an algorithm — a traffic-distribution rule.
The two main ones in AWS ALB are:
Round Robin (default — shown as Nested Round Robin)
Least Outstanding Requests

⚙️ 1. Nested Round Robin (Default Algorithm)
🧠 Simple Meaning: it rotates through your servers like a circle
The Load Balancer sends requests to each target one by one in order, and then repeats.

⚙️ 2. Least Outstanding Requests Algorithm
🧠 Simple Meaning:
Send the next request to the server that currently has the least number of ongoing (unfinished) requests.
Instead of taking turns, the ALB checks which server is currently least busy.
If one server is handling many slow requests, and another is free,
the Load Balancer will send new traffic to the less busy one.

| Concept                        | Plain Explanation                                     |
| ------------------------------ | ----------------------------------------------------- |
| **Nested Round Robin**         | Send requests to servers one by one, evenly (default) |
| **Least Outstanding Requests** | Send requests to whichever server is least busy       |
| **Where to set**               | Target Group → Attributes → Load Balancing Algorithm  |

********************************************************************

💡 What is Stickiness?
Stickiness means keeping a user connected to the same server (EC2 instance) every time they visit your website — for a period of time.

In simple words:
Stickiness = “Same user → Same server”
🧠 Why is this needed?

Normally, a Load Balancer distributes traffic evenly:
1st request → Server A
2nd request → Server B
3rd request → Server C

But sometimes, a user’s data is stored temporarily on one server — for example, login sessions, shopping carts, or user preferences.
If the Load Balancer suddenly sends that user to a different server,
that new server won’t have the user’s session data → user might get logged out or lose their cart.

So we use Stickiness to make sure:
The same user always goes back to the same EC2 (where their data is stored).

********************************************************************

********************************************************************

********************************************************************


********************************************************************

create two server in differce zone 1a and 1b 
minimy 2 sub nets need to add while creating applicaito load balace

task : 
create 2 instace those shoule work on 80 port
create Tagater group with these 2 instace:
access with dns url check working r not and try sticky and other 

tast2 : 
create one more instace should work with8 80 80 port, create anthothe TG 
 we can add html file in user data while creating instace 

#!/bin/bash
yum install httpd -y
server httpd start 
chkconfig http on 
echo "<h1>content </h1> /var/www/html/index.html