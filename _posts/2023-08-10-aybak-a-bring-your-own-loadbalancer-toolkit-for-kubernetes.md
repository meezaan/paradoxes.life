---
layout: post
title: Aybak by Mamluk - A Bring Your Own Load Balancer Toolkit for Kubernetes
tags: kubernetes aws azure eks aks gke cloud devops sustainability autoscaling
---

<img src="/assets/img/k8s-aybak.png" 
alt="Aybak - a bring your own loadbalancer toolkit for Kubernetes" />
Today, at <a href="https://mamluk.net" target="_blank" rel="nofollow">Mamluk</a>, we are announcing 
the release of <a href="https://github.com/mam-luk/aybak" target="_blank">Aybak</a>, an Open Source 
Bring your own load balancer toolkit for any managed Kubernetes service
(AWS EKS, Google GKE, Microsoft Azure AKS, etc.).

Aybak was born out of the necessity to efficiently manage distributed clusters when Cloud Native services 
are simply not good enough. And whilst consultancies would charge exorbitant amounts for this service, it should really be 
free and open source.

If you've had to run busy distributed clusters, and understand the necessity of tuning load balancers to efficiently 
distribute traffic across your worker nodes, then you'll understand the need for Aybak. A typical load balancer 
from a Cloud Provider (any cloud provider, be it AWS, GCP, Azure, Digital Ocean, or Linode) will only handle 
a certain number of open connections (not requests, but connections at layer 4). The recent trend from the 
hyperscale cloud providers has been to recommend running load balancers at layer 7 as the ingress that directly 
communicates with pods on the cluster. Whilst this is marketed is giving you higher availability, it is in fact 
a way for the cloud providers to sell you more cloud native load balancers.

In a typical setup, you would run a layer 4 cloud provider managed load balancer that forwards traffic to 
your ingress controller (which is a layer 7 component).

As your cluster autoscales and adds more worker nodes, the Kube Cloud Controller Manager (KCCM) from the cloud 
provider will update the load balancer with IP addresses of the new nodes. This is all good, until you hit the connection 
limit on the cloud provider's load balancer. Once you hit the limit, it's effectively game over unless your intervene manually 
by adding another cloud native load balancer and updating your DNS enstries. 

As this is a managed service, you can't tune it for optimal performance.  

For instance, you would tune an HA Proxy load balancer completely differently to serve a high volume of connections from a web application 
vs a high volume of connections to an API from mobile or IoT devices.

In our case, we hit a limitation where we would need to run at least 7 cloud provider managed load balancers in each cluster to service 
our daily traffic.

But with a correctly tuned instance of HA Proxy, the same thing can be accomplished with just a single node with 1 CPU and 2 GB of memory.

And this is where Aybak was born. Aybak will save:

1. Your time. The code is all there for you to get the IPs from your cluster, with GitHub Actions to update your HA Proxy load balancer automatically.
2. The carbon footprint of running 7 load balancers (or VMs) vs running 1 VM in each region.
3. The amount of money involved. If we have just 2 regions and each load balancer or virtual machine costs $30, we are talking about spending $420 vs $60 per month. Ergo, a saving of $350 per month. This translates into $4,200 per year.
3. Now, this is not a lot of money, but think of all the villages and towns in Africa where people don't have the money to dig a well for fresh water. Perhaps you could donate this money there instead of using a 'Cloud Native' service and contribute to improving the lives of hundreds of thousands of people.

There are, of course, other considerations.