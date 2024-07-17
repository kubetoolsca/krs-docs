---
title: Getting Started
description: What does your user need to know to try your project?
categories: [guide, setup, intro, getting started]
tags: [krs, install]
weight: 2
---

KRS empowers you to manage your Kubernetes clusters with the help of cutting-edge Artificial Intelligence. This guide equips you with everything you need to get started and unlock the potential of KRS's intelligent recommendations, proactive problem detection, and powerful health checks.


## Prerequisites

- **Up and Running Kubernetes Cluster:** Ensure you have a Kubernetes cluster running locally (e.g., Minikube, etc) or in the cloud (e.g., Amazon EKS, Google Kubernetes Engine, etc), if on the cloud, ensure that you've secured a config file, before using KRS.

- **Python 3.6+:** KRS is a Python-based tool, so make sure you have Python 3.6 or a later version installed on your system. You can check your version by running python3 --version in your terminal. If you don't have Python installed, head over to https://www.python.org/downloads/ for installation instructions.

- **Basic understanding of Kubernetes concepts:** Having a foundational understanding of Kubernetes concepts like pods, namespaces, and deployments will help you get the most out of KRS's functionalities.

## Installation

1. **Clone the Repository** 
    {{% pageinfo %}}
    git clone https://github.com/kubetoolsca/krs.git
    {{% /pageinfo %}}
2. **Change directory to the cloned repository** 
     {{% pageinfo %}}
    cd krs
    {{% /pageinfo %}}
3. **Python Package Installation** 
     {{% pageinfo %}}
    pip install krs
    {{% /pageinfo %}}

## Initial Setup

1. **Initialize KRS** 
    This step initializes KRS's services and loads the scanner.
    {{% pageinfo %}}
    krs init
    {{% /pageinfo %}}
2. **Explore KRS Commands (Optional)** 
    {{% pageinfo %}}
    krs --help
    {{% /pageinfo %}}

## Scan Your Cluster and Explore Recommendations

This is where the real power of KRS comes in!

1. **Scan your cluster** 
    Execute the following command to scan your cluster and identify the tools currently in use:
    {{% pageinfo %}}
    krs scan
    {{% /pageinfo %}}
2. **View recommended tools** 
    KRS analyzes your cluster and recommends tools based on best practices and its internal ranking database. Use the following command to explore these recommendations
    {{% pageinfo %}}
    krs recommend
    {{% /pageinfo %}}
3. **Interactive Health Check with AI** 
    KRS leverages Large Language Models (LLMs) like OpenAI or Hugging Face to provide in-depth health checks for your pods.
    {{% pageinfo %}}
    pip install krs
    {{% /pageinfo %}}

## Try it out!

Can your users test their installation, for example by running a command or deploying a Hello World example?
