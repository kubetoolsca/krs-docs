---
title: Azure AKS
description: >
  How to Install KRS on AKS
date: 2017-01-05
weight: 4
---

Optimize your AKS cluster management with KRS. This powerful tool, installed locally on your machine, analyzes your AKS cluster to identify areas for improvement. KRS leverages AI to provide recommendations for enhancing your cluster's efficiency and functionality.

## Prerequisites:

- An Azure account
- Install Azure CLI on your laptop

## Installation

1. **Clone the repository using the command**

    ```
    git clone https://github.com/kubetoolsca/krs.git
    ```

2. **Install the Krs Tool**

    Change directory to /krs and run the following command to install krs locally on your system:

    ```
    pip install .
    ```

3. **Check if the tool has been successfully installed using**

    ```
    krs --help
    ```

    ```
    krs --help
                                                                                    
    Usage: krs [OPTIONS] COMMAND [ARGS]... **                                        
                                                                                    
    krs: A command line interface to scan your Kubernetes Cluster, detect errors,  
    provide resolutions using LLMs and recommend latest tools for your cluster     
                                                                                    
    ╭─ Options ────────────────────────────────────────────────────────────────────╮
    │ --install-completion          Install completion for the current shell. **     │
    │ --show-completion             Show completion for the current shell, to copy │
    │                               it or customize the installation. **             │
    │ --help                        Show this message and exit. **                   │
    ╰──────────────────────────────────────────────────────────────────────────────╯
    ╭─ Commands ───────────────────────────────────────────────────────────────────╮
    │ exit         Ends krs services safely and deletes all state files from       │
    │              system. **Removes all cached data. **                               │
    │ export       Exports pod info with logs and events. **                         │
    │ health       Starts an interactive terminal using an LLM of your choice to   │
    │              detect and fix issues with your cluster                         │
    │ init         Initializes the services and loads the scanner. **                │
    │ namespaces   Lists all the namespaces. **                                      │
    │ pods         Lists all the pods with namespaces, or lists pods under a       │
    │              specified namespace. **                                           │
    │ recommend    Generates a table of recommended tools from our ranking         │
    │              database and their CNCF project status. **                        │
    │ scan         Scans the cluster and extracts a list of tools that are         │
    │              currently used. **                                                │
    ╰──────────────────────────────────────────────────────────────────────────────╯
    ```



    Once you get a list of commands you can move onto the next part.

## Create an AKS cluster on your Azure account

1. **Create an AKS Cluster**

    To create an AKS account, you can log into your account and search for Azure Kubernetes Service.

    <img width="558" alt="Screenshot 2024-07-01 at 10 17 54 PM" src="https://github.com/kubetoolsca/krs/assets/90956242/10b571d3-4c22-449b-81a3-c742aa0e893f">


    Once you click create, you can name your cluster, add a node pool (I used the default agent pool but you can create your own), and leave everything else to its default state. **This will help you create a cluster.

2. **Install Azure CLI**


    ```
    brew update && brew install azure-cli
    ```

3. **Log into your Azure account**

    Once the CLI is installed, log into your Azure account using the command:

    ```
    az login
    ```

4. **Connect to Your Cluster**

    Retrieve the connection command from your cluster details on the Azure portal and execute it to connect to your cluster.

    <img width="558" alt="Screenshot 2024-07-01 at 10 18 25 PM" src="https://github.com/kubetoolsca/krs/assets/90956242/652cc069-4bf8-4ba2-98b1-330ff7dd46fe">
    <img width="557" alt="Screenshot 2024-07-01 at 10 18 51 PM" src="https://github.com/kubetoolsca/krs/assets/90956242/8738ca38-e4bf-40a7-b676-381886a44eca">


## Using Krs

1. **Initialise Krs**

    ```
    krs init
    ```

2. **Scan the Clusters**

    ```
        krs scan
        Scanning your cluster...
        Cluster scanned successfully...
        Extracted tools used in cluster...
        The cluster is using the following tools:
        +-------------+--------+-----------------------------+---------------+
        | Tool Name   | Rank   | Category                    | CNCF Status   |
        +=============+========+=============================+===============+
        | autoscaler  | 5      | Cluster with Core CLI tools | unlisted      |
        +-------------+--------+-----------------------------+---------------+
    ```

3. **Get Recommended Tools**

    ```
        % krs recommend`
        Our recommended tools for this deployment are:
        +-----------------------------+------------------+-------------+---------------+
        | Category                    | Recommendation   | Tool Name   | CNCF Status   |
        +=============================+==================+=============+===============+
        | Cluster with Core CLI tools | Recommended tool | k9s         | unlisted      |
        +-----------------------------+------------------+-------------+---------------+
    ```

4. **Installing a few tools**

    ```
      brew install helm
      helm install kubeview kubeview
    ```

    ```
      helm install kubeview kubeview
      NAME: kubeview
      LAST DEPLOYED: Sat Jun 29 21:44:17 2024
      NAMESPACE: default
      STATUS: deployed
      REVISION: 1
      NOTES:
      =====================================
      ==== KubeView has been deployed! ====
      =====================================
      To get the external IP of your application, run the following:
      export SERVICE_IP=$(kubectl get svc --namespace default kubeview -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
      echo http://$SERVICE_IP
      NOTE: It may take a few minutes for the LoadBalancer IP to be available.
      You can watch the status of by running 'kubectl get --namespace default svc -w kubeview'
    ```

5. **Exports pod info with logs and events**

    ```
        krs export
        Pod info with logs and events exported. **Json file saved to current directory!

        ```
        meetsimarkaur@meetsimars-MBP krs % ls
        CODE_OF_CONDUCT.md   arch.png      gke.md         kubeview
        CONTRIBUTIONS.md     bhive.png     krs            samples
        LICENSE              build         krs.egg-info   setup.py
        README.md            exported_pod_info.json   kubetail
    ```

6. **Detecting and Fixing Issues with my cluster**

    ```
        krs health`
        Starting interactive terminal...
        Choose the model provider for healthcheck:
        [1] OpenAI
        [2] Huggingface
        >> 1
        Installing necessary libraries.........
        openai is already installed.
        Enter your OpenAI API key: sk-proj-xxxxxxx
        Enter the OpenAI model name: gpt-3.5-turbo
        API key and model are valid.
        Namespaces in the cluster:
        1. **default
        2. **kube-node-lease
        3. **kube-public
        4. **kube-system
        Which namespace do you want to check the health for? Select a namespace by entering its number:
        >> 1
        Pods in the namespace default:
        1. **kubeview-64fd5d8b8c-khv8v
        Which pod from default do you want to check the health for? Select a pod by entering its number:
        >> 1
        Checking status of the pod...
        Extracting logs and events from the pod...
        Logs and events from the pod extracted successfully!
        Interactive session started. **Type 'end chat' to exit from the session!
        >> Everything looks good!
        Since the log entries provided are empty, there are no warnings or errors to analyze or address. **If there were actual log entries to review, common steps to resolve potential issues in a Kubernetes environment could include:
        1. **Checking the configuration files for any errors or inconsistencies.
        2. **Verifying that all necessary resources (e.g. **pods, services, deployments) are running as expected.
        3. **Monitoring the cluster for any performance issues or resource constraints.
        4. **Troubleshooting any networking problems that may be impacting connectivity.
        5. **Updating Kubernetes components or applying patches as needed to ensure system stability and security.
        6. **Checking logs of specific pods or services for more detailed error messages to pinpoint the root cause of any issues.
        >> 2
        >> Since the log entries are still empty, the response remains the same: Everything looks good! If you encounter any specific issues or errors in the future, feel free to provide the logs for further analysis and troubleshooting.
    ```

With KRS, you can effortlessly identify and optimize the tools within your Kubernetes clusters, whether on-premises or in the public cloud, simplifying your Kubernetes management journey.