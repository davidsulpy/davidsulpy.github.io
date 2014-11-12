---
layout: post
title: "Speeding Up Deployments AND Scale responsiveness with TeamCity"
date: 2014-06-17 18:49
published: false
comments: true
categories: ["aws", "packer", "ubuntu", "devops", "automation", "scaling"]
---

We've all faced the piper payment challenge. That is, do you pay the piper now, later, or spread it out in small payments throughout. The answer depends mostly on your needs.

Here's how to accomplish both fast, resiliant deployments with Packer, a relatively new project created by the original developer of Vagrant to help automate the AMI creation process.

###What about Puppet and Chef and Ansible oh my!?
Configuration management and deployment tools like those mentioned above (and many others) have proven *excellent* tools for increasing three main things:

1. Configuration Consistency (configuration as version-controlled code)
2. Tamper-proofing; or at least periodic self-healing
3. Environment flexability

Automating DevOps is crucial... These tools provide a great start for adding a touch of automation into your environment management. However, I don't believe these tools alone allow you to take full advantage of the atomic, ephemeral lifecycle of virtual cloud servers. A fact that is changing the nature of operations in the cloud.

###What do you mean atomic and ephemeral?
Atomic: with cloud services like AWS, EC2 servers have become small units in a larger system.

