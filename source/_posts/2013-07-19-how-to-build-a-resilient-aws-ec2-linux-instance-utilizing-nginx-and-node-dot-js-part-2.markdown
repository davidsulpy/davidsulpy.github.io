---
layout: post
title: "How to Build a Resilient AWS EC2 Linux Instance Utilizing Nginx and Node.js (Part 2)"
date: 2013-07-19 09:25
comments: true
categories: [aws, node.js, Amazon Linux, nginx]
---

If you followed read my last post, you were walked through how to build a node-nginx EC2 instance on RHEL 6. I had initially started with Amazon Linux before writing that post, and then switch to Ubuntu 12.04 and finally to RHEL6.4 only after not having much, off-the-bat success with the first two. This post, I am going to tackle the same thing, but with Amazon Linux and work out the kinks. Why? Because Amazon Linux is cheaper per hour, optomized for running in Amazon's cloud, has much better Amazon support, AND if you want to do any kind of automated deployments/installations when launching this instance from an AMI, you can use aws-cfn-bootstrap which isn't terribly well supported on RHEL6.4 (for instance, if you install on RHEL6.4 your likely to run into some interesting issues trying to reconnect to your instance on port 22 later...).