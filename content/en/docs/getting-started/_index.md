---
title: Getting Started
description: A clear roadmap for installing and using KRS
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
    You'll see the following results:
    {{% pageinfo %}}
    Scanning your cluster...

    Cluster scanned successfully...

    Extracted tools used in cluster...


    The cluster is using the following tools:

    +-------------+--------+------------+---------------+
    | Tool Name   | Rank   | Category   | CNCF Status   |
    +=============+========+============+===============+
    +-------------+--------+------------+---------------+
    {{% /pageinfo %}}

2. **View recommended tools** 
    KRS analyzes your cluster and recommends tools based on best practices and its internal ranking database. Use the following command to explore these recommendations
    {{% pageinfo %}}
    krs recommend
    {{% /pageinfo %}}

    You'll see similar results to this:
    {{% pageinfo %}}

    krs recommend

    Our recommended tools for this deployment are:

    +----------------------+------------------+-------------+---------------+
    | Category             | Recommendation   | Tool Name   | CNCF Status   |
    +======================+==================+=============+===============+
    | Alert and Monitoring | Recommended tool | grafana     | listed        |
    +----------------------+------------------+-------------+---------------+
    | Cluster Management   | Recommended tool | rancher     | unlisted      |
    +----------------------+------------------+-------------+---------------+
    {{% /pageinfo %}}

## Interactive Health Check with AI

KRS leverages Large Language Models (LLMs) like OpenAI or Hugging Face to provide in-depth health checks for your pods.

1. **Start the health check** 
    Execute the following command to initiate an interactive terminal session:
    {{% pageinfo %}}
    krs health
    {{% /pageinfo %}}
    You'll see the following results:
    {{% pageinfo %}}
    krs health

    Starting interactive terminal...


    Choose the model provider for healthcheck:

    [1] OpenAI
    [2] Huggingface

    >>
    {{% /pageinfo %}}

2. **Choose your LLM provider** 
    The user is prompted to choose a model provider for the health check. The options provided are "OpenAI" and "Huggingface". The selected option determines which LLM model will be used for the health check.

    Let's say you choose the option "1", then it will install the necessary libraries.

    {{% pageinfo %}}
    Enter your OpenAI API key: open_ai_api_key

    Enter the OpenAI model name: gpt-3.5-turbo
    API key and model are valid.

    Namespaces in the cluster:

    1. default
    2. kube-node-lease
    3. kube-public
    4. kube-system
    5. ns1

    Which namespace do you want to check the health for? Select a namespace by entering 
    its number: >> 4


    {{% /pageinfo %}}
    
3. **Specify the pod** 
    Choose the pod you want to analyze from the listed options. KRS will then extract logs and events for the selected pod.

    {{% pageinfo %}}
    Which namespace do you want to check the health for? Select a namespace by entering 
    its number: >> 4

    Pods in the namespace kube-system:

    1. coredns-76f75df574-mdk6w
    2. coredns-76f75df574-vg6z2
    3. etcd-docker-desktop
    4. kube-apiserver-docker-desktop
    5. kube-controller-manager-docker-desktop
    6. kube-proxy-p5hw4
    7. kube-scheduler-docker-desktop
    8. storage-provisioner
    9. vpnkit-controller

    Which pod from kube-system do you want to check the health for? Select a pod by entering its 
    number: >> 4

    Checking status of the pod...

    Extracting logs and events from the pod...

    Logs and events from the pod extracted successfully!

    >>
    {{% /pageinfo %}}

4. **Interact with the LLM** 
    The LLM will analyze the extracted information and provide insights into potential issues with your pod. 
    You can ask clarifying questions or request further analysis within the interactive terminal.

    If your pod has no errors, your output would be :

    {{% pageinfo %}}

    Interactive session started. Type 'end chat' to exit from the session!

    >>  The log entries provided are empty {}, so there is nothing to analyze. Therefore, 
    I can confirm that 'Everything looks good!' in this case.

    If there were warnings or errors in the log entries, I would have analyzed them 
    thoroughly to identify the root cause. Depending on the specific warnings or 
    errors, potential steps to resolve the issues could include:

    1. Analyzing the specific error message to understand the problem
    2. Checking Kubernetes resources (e.g., pods, deployments, configmaps) 
    for any misconfigurations
    3. Verifying connectivity to external resources or dependencies
    4. Checking for resource limitations or constraints that could be causing issues
    5. Reviewing recent changes in the Kubernetes environment that could have introduced problems
    6. Using Kubernetes troubleshooting tools like kubectl logs, describe, or events 
    to gather more information 

    By following these steps and addressing any identified issues, you can resolve 
    warnings or errors in the Kubernetes environment.

    >> Wonderful, anything else to note?
    >>  In addition to resolving warnings or errors in Kubernetes logs, it's important to regularly 
    monitor and maintain the Kubernetes environment to ensure smooth operation. Some best 
    practices for Kubernetes maintenance include:

    1. Regularly updating Kubernetes components and cluster nodes to the latest stable versions 
    to benefit from bug fixes and security patches.
    2. Implementing automated backups of critical data and configurations to 
    prevent data loss in case of failures.
    3. Monitoring resource utilization and scaling components as needed to optimize 
    performance and cost efficiency.
    4. Implementing security best practices, such as network policies, RBAC, and 
    pod security policies to protect 
    the cluster from unauthorized access or malicious activities.
    5. Conducting regular health checks and performance tuning to identify 
    and address any bottlenecks or 
    inefficiencies in the cluster.
    6. Developing a disaster recovery plan and testing it periodically to 
    ensure business continuity in case of unexpected events.

    By following these maintenance practices, you can ensure the stability, scalability, and security 
    of your Kubernetes environment for optimal DevOps operations.

    >> Alright, so are we done?
    >>  Yes, we have covered the analysis of the Kubernetes log entries and 
    discussed best practices for Kubernetes maintenance. If you have any more 
    questions or need further assistance, feel free to ask. Otherwise, 
    we can consider this conversation complete.

    >> Wonderful. Thanks! end chat
    >>  You're welcome! If you have any more questions in the future, 
    feel free to reach out. Have a great day! Goodbye!

    >> end chat

    {{% /pageinfo %}}

    Else, your output would be:

    {{% pageinfo %}}
    Interactive session started. Type 'end chat' to exit from the session!

    >>  Warning/Error 1:
    "Unable to authenticate the request" with err="[invalid bearer token, 
    service account token has expired]"
    This indicates that there was an issue with authenticating the request due to an invalid bearer token and 
    an expired service account token. To resolve this issue, the bearer token needs to be updated or regenerated, 
    and the service account token needs to be renewed.

    Warning/Error 2:
    "Failed to update lease" with err="StorageError: invalid object, Code: 4, Key: 
    /registry/leases/kube-system/apiserver-457xdkumpkdqmkwikdt6khrbya"
    This error indicates a storage error while trying to update a lease, possibly due to an invalid object 
    or a conflict in UIDs. To resolve this issue, the lease object needs to be checked and possibly 
    recreated with the correct UID.

    Warning/Error 3:
    "Error removing old endpoints from kubernetes service: no API server IP addresses were listed in storage, 
    refusing to erase all endpoints for the kubernetes Service"
    This warning indicates that there were no API server IP addresses listed in storage, causing the removal 
    of old endpoints from the Kubernetes service to fail. To resolve this issue, the API server IP addresses 
    need to be correctly listed in storage.

    Warning/Error 4:
    "Skipping API apps/v1beta1 because it has no resources."
    This warning indicates that the API version 'apps/v1beta1' is being skipped because it has no 
    associated resources. This might be an informational warning and may not necessarily require 
    immediate action, depending on the use case.

    Warning/Error 5:
    "watch chan error: etcdserver: mvcc: required revision has been compacted"
    This error indicates a watch channel error related to the revision being compacted in etcdserver. 
    To resolve this issue, the etcd database revision or configuration may need to be checked and potentially adjusted.

    Overall, it is important to investigate and address each warning and error to ensure the stability 
    and reliability of the Kubernetes cluster. If there are no concerns in the log entries provided, 
    the message 'Everything looks good!' can be returned.

    >> can you help me in fixing this error message
    >>  To help you fix the error messages mentioned in the log entries, here are some steps you can take:

    1. For the "Unable to authenticate the request" error:
    - Generate a new bearer token and update it in the relevant configuration files.
    - Renew the service account token to prevent expiration issues.

    2. For the "Failed to update lease" error:
    - Investigate the storage error and check for any invalid objects.
    - Recreate the lease object with the correct UID if needed.

    3. For the "Error removing old endpoints from Kubernetes service" error:
    - Ensure that the API server IP addresses are correctly listed in the storage.
    - Verify the configuration of the Kubernetes service and update it if necessary.

    4. For the "watch chan error: etcdserver: mvcc: required revision has been compacted" error:
    - Check the etcd server configuration and ensure that the revision is maintained correctly.
    - Monitor the etcd server for any potential issues causing revision compaction.

    After performing these steps, restart relevant services or components as needed to apply the changes. 
    Monitor the Kubernetes cluster for any further errors and ensure that the issues have been resolved successfully.

    Feel free to provide more specific details or additional logs if you need further assistance with resolving the error messages.

    {{% /pageinfo %}}


5. **Exit the session** 
    Type end chat to exit the interactive health check session.

## Additional Resources!

KRS Project Repository: For those interested in contributing to the project or exploring the source code, visit the project repository. ([Github Repo](https://github.com/kubetoolsca/krs-docs))
