---
title: CLI Reference 
date: 2017-01-05
description: >
  Everything you need to master the KRS CLI
categories: [CLI-Reference]
tags: [CLI, KRS CLI, example, commands]
---

The KRS CLI provides a powerful set of commands for interacting with your Kubernetes clusters and leveraging KRS's intelligent features. This section serves as a comprehensive reference guide for all available commands and their functionalities.

```

    krs --help

    Usage: krs [OPTIONS] COMMAND [ARGS]...

    krs: A command line interface to scan your Kubernetes Cluster, detect errors, provide resolutions using LLMs and recommend latest tools for your cluster

    ╭─ Options ─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
    │ --install-completion          Install completion for the current  shell.                                                                                       │
    │ --show-completion             Show completion for the current shell, to copy it or customize the installation.                                                │
    │ --help                        Show this message and exit.                                                                                                     │
    ╰───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
    ╭─ Commands ────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
    │ exit         Ends krs services safely and deletes all state files from system. Removes all cached data.                                                       │
    │ export       Exports pod info with logs and events.                                                                                                           │
    │ health       Starts an interactive terminal using an LLM of your choice to detect and fix issues with your cluster                                            │
    │ init         Initializes the services and loads the scanner.                                                                                                  │
    │ namespaces   Lists all the namespaces.                                                                                                                        │
    │ pods         Lists all the pods with namespaces, or lists pods under a specified namespace.                                                                   │
    │ recommend    Generates a table of recommended tools from our ranking database and their CNCF project status.                                                  │
    │ scan         Scans the cluster and extracts a list of tools that are currently used.                                                                          │
    ╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
```

### Understanding the Output

When you execute krs --help, you'll see a formatted output that provides an overview of the KRS CLI and its functionalities. Here's a breakdown of the key sections:

- **Usage:**
  This line describes the general format for using KRS commands. It specifies that you can use optional arguments ([OPTIONS]) followed by a specific command (COMMAND) and any additional arguments ([ARGS]) needed for that command.
- **krs: A command line interface... :**
  This section provides a brief description of KRS's purpose: scanning Kubernetes clusters, detecting errors, providing solutions using LLMs, and recommending the latest tools.
- **Options (Global):**
  These options apply to all KRS commands and can be used to customize their behavior.
  - **```--install-completion```:**
      Installs autocompletion for the current shell, making it easier to type KRS commands. 
  - **```--show-completion```:**
      Shows available autocompletion options for the current shell.
  - **```--help```:**
      Displays this help message and exits the program. 
- **Commands:**
  This table lists all available KRS commands and their brief descriptions.

### Detailed Command Explanations

This section dives deeper into each KRS command, providing a comprehensive explanation of its purpose, usage syntax, options, and examples for practical application.

##### 1. **krs init:**
- **Purpose:**
  Initializes the KRS services and loads the scanner. This step is necessary for KRS to function properly. Initialization ensures essential internal services are running efficiently, enabling features like health checks and communication with Large Language Models (LLMs).
- **Usage:** 
  - **```krs init```**
- **Options:** None
- **Example:**
  ```
    krs init
  ```
**Output**
  ```
    Services initialized and scanner loaded.
  ```

##### 2. **krs scan:**
- **Purpose:** 
  Scans your Kubernetes cluster to identify currently deployed tools and extract relevant information about their usage. This information is used for various purposes, including understanding your current cluster setup and generating recommendations.
- **Usage:** 
  - **```krs scan```**
- **Options:** None
- **Example:**
  ```
    krs scan
  ```

- **Output:**

  The krs scan command provides a list of tools detected within your Kubernetes cluster. This list may include tools for monitoring, logging, security, networking, and more.

  ```
    Scanning your cluster...

    Cluster scanned successfully...

    Extracted tools used in cluster...


    The cluster is using the following tools:

    +-------------+--------+------------------+---------------+
    | Tool Name   |   Rank | Category         | CNCF Status   |
    +=============+========+==================+===============+
    | cilium      |      1 | Network Policies | graduated     |
    +-------------+--------+------------------+---------------+
    | hubble      |      7 | Security Tools   | listed        |
    +-------------+--------+------------------+---------------+
  ```

##### 3. **krs namespaces:**
- **Purpose:**  
  Lists all namespaces within your cluster. Namespaces provide a way to logically group Kubernetes resources. Understanding your cluster's namespace structure is essential for managing resources effectively.
- **Usage:** 
  - **```krs namespaces```**
- **Options:** None
- **Example:** 
  ```
    krs namespaces
  ```

- **Output:**

  The krs namespaces command displays a list of all namespace names within your Kubernetes cluster.

  ```
    Namespaces in your cluster are: 

    1. default
    2. kube-node-lease
    3. kube-public
    4. kube-system
  ```

##### 4. **krs pods [--namespace <namespace_name>]:**
- **Purpose:**
  Lists all pods within the cluster, optionally filtered by a specific namespace. Pods are the fundamental units of execution in Kubernetes and house containerized applications.
- **Usage:** 
  - **```krs pods```**
  - **```krs pods --namespace <namespace_name>```**
- **Options:**
  - **```--namespace <namespace_name>```**: Filters the list of pods to include only those within the specified namespace.
- **Example:**
  ```
    krs pods
  ```

  ```
    krs pods --namespace kube-system 
  ```
  
- **Output:**

  The krs namespaces command displays a list of all namespace names within your Kubernetes cluster.

  ```
    Pods in namespace 'kube-system': 

    1. cilium-9lqbq
    2. cilium-ffpct
    3. cilium-pvknr
    4. coredns-85f59d8784-nvr2n
    5. coredns-85f59d8784-p9jcv
    6. cpc-bridge-proxy-c6xzr
    7. cpc-bridge-proxy-p7r4p
    8. cpc-bridge-proxy-tkfrd
    9. csi-do-node-hwxn7
    10. csi-do-node-q27rc
    11. csi-do-node-rn7dm
    12. do-node-agent-6t5ms
    13. do-node-agent-85r8b
    14. do-node-agent-m7bvr
    15. hubble-relay-74686df4df-856pj
    16. hubble-ui-86cc69bddc-xc745
    17. konnectivity-agent-9k8vk
    18. konnectivity-agent-h5fm2
    19. konnectivity-agent-kf4xh
    20. kube-proxy-94945
    21. kube-proxy-qgv4j
    22. kube-proxy-vztzf

  ```

##### 5. **krs recommend:**
- **Purpose:**
  Generates a table of recommended tools based on KRS's internal ranking database and your cluster configuration. The recommendations consider factors like the identified gaps in your current tooling, tool popularity within the Kubernetes community, and feature compatibility with your cluster setup.
- **Usage:**
  - **```krs recommend```**
- **Options:** None
- **Example:**
  ```
    krs recommend
  ```

- **Output:**

  The krs recommend command displays a table with recommended tools. The table typically includes information like the tool name, a brief description, and its CNCF project status (e.g., graduated, listed).

  ```
    Our recommended tools for this deployment are:

    +------------------+------------------------+-------------+---------------+
    | Category         | Recommendation         | Tool Name   | CNCF Status   |
    +==================+========================+=============+===============+
    | Network Policies | Already using the best | cilium      | graduated     |
    +------------------+------------------------+-------------+---------------+
    | Security Tools   | Recommended tool       | trivy       | listed        |
    +------------------+------------------------+-------------+---------------+

  ```

##### 6. **krs health:**
- **Purpose:**
  Starts an interactive terminal session for performing in-depth health checks on your Kubernetes cluster. This session utilizes KRS's capabilities to go beyond basic health checks provided by Kubernetes itself.
- **Usage:**
  - **```krs health```**
- **Options:** None
- **Example:**
  ```
    krs health
  ```

- **Output:**

  Executing krs health launches a new interactive terminal window. Within this terminal, you'll have access to a set of KRS health check functionalities. These functionalities may vary depending on your KRS version and configuration, but they typically include:

  - **Detailed Pod Health:** KRS can delve deeper than basic liveness and readiness probes offered by Kubernetes. It can analyze container logs, resource consumption metrics, and even leverage LLMs to identify potential issues within pods that might not be readily apparent with standard checks.
  - **Network Health Analysis:** KRS can assess the health of your cluster's network fabric. This might involve examining pod-to-pod communication latency, identifying potential bottlenecks, and verifying network configuration for optimal performance.
  - **Security Posture Evaluation:** KRS can scan your cluster for security vulnerabilities. This may involve analyzing deployments for outdated container images, checking security context constraints (SCCs), and searching for suspicious activities within the cluster.

  ```

    Starting interactive terminal...


    Choose the model provider for healthcheck: 

    [1] OpenAI 
    [2] Huggingface

    >> 1

    Installing necessary libraries..........

    openai is already installed.

    Enter your OpenAI API key: *open_ai_api_key*
    Enter the OpenAI model name: gpt-3.5-turbo
    API key and model are valid.

    Namespaces in the cluster:

    1. default
    2. kube-node-lease
    3. kube-public
    4. kube-system
    5. portainer

    Which namespace do you want to check the health for? Select a namespace by entering its number: >> 4

    Pods in the namespace kube-system:

    1. cilium-9lqbq
    2. cilium-ffpct
    3. cilium-pvknr
    4. coredns-85f59d8784-nvr2n
    5. coredns-85f59d8784-p9jcv
    6. cpc-bridge-proxy-c6xzr
    7. cpc-bridge-proxy-p7r4p
    8. cpc-bridge-proxy-tkfrd
    9. csi-do-node-hwxn7
    10. csi-do-node-q27rc
    11. csi-do-node-rn7dm
    12. do-node-agent-6t5ms
    13. do-node-agent-85r8b
    14. do-node-agent-m7bvr
    15. hubble-relay-74686df4df-856pj
    16. hubble-ui-86cc69bddc-xc745
    17. konnectivity-agent-9k8vk
    18. konnectivity-agent-h5fm2
    19. konnectivity-agent-kf4xh
    20. kube-proxy-94945
    21. kube-proxy-qgv4j
    22. kube-proxy-vztzf


    Which pod from kube-system do you want to check the health for? Select a pod by entering its number: >> 1

    Checking status of the pod...

    Extracting logs and events from the pod...

    Logs and events from the pod extracted successfully!


    Interactive session started. Type 'end chat' to exit from the session!

    >>  The log entries provided are empty {}, so there is nothing to analyze. Therefore, I can confirm that 'Everything looks good!' in this case.

    If there were warnings or errors in the log entries, I would have analyzed them thoroughly to identify the root cause. Depending on the specific warnings or errors, potential steps to resolve the issues could include:

    1. Analyzing the specific error message to understand the problem
    2. Checking Kubernetes resources (e.g., pods, deployments, configmaps) for any misconfigurations
    3. Verifying connectivity to external resources or dependencies
    4. Checking for resource limitations or constraints that could be causing issues
    5. Reviewing recent changes in the Kubernetes environment that could have introduced problems
    6. Using Kubernetes troubleshooting tools like kubectl logs, describe, or events to gather more information 

    By following these steps and addressing any identified issues, you can resolve warnings or errors in the Kubernetes environment.

    >> Wonderful, anything else to note?
    >>  In addition to resolving warnings or errors in Kubernetes logs, it's important to regularly monitor and maintain the Kubernetes environment to ensure smooth operation. Some best practices for Kubernetes maintenance include:

    1. Regularly updating Kubernetes components and cluster nodes to the latest stable versions to benefit from bug fixes and security patches.
    2. Implementing automated backups of critical data and configurations to prevent data loss in case of failures.
    3. Monitoring resource utilization and scaling components as needed to optimize performance and cost efficiency.
    4. Implementing security best practices, such as network policies, RBAC, and pod security policies to protect the cluster from unauthorized access or malicious activities.
    5. Conducting regular health checks and performance tuning to identify and address any bottlenecks or inefficiencies in the cluster.
    6. Developing a disaster recovery plan and testing it periodically to ensure business continuity in case of unexpected events.

    By following these maintenance practices, you can ensure the stability, scalability, and security of your Kubernetes environment for optimal DevOps operations.

    >> Alright, so are we done?
    >>  Yes, we have covered the analysis of the Kubernetes log entries and discussed best practices for Kubernetes maintenance. If you have any more questions or need further assistance, feel free to ask. Otherwise, we can consider this conversation complete.

    >> Wonderful. Thanks! end chat
    >>  You're welcome! If you have any more questions in the future, feel free to reach out. Have a great day! Goodbye!

    >> end chat


  ```
