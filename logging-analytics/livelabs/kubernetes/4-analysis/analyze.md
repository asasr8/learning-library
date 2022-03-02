
# Introduction

## Introduction well done!

This lab walks you through the steps to ...

Estimated Lab Time: n minutes

### Objectives

In this lab, you will:
* Objective 1
* Objective 2
* Objective 3

### Prerequisites

* Same as specified in the introduction section


## **STEP 1**: Create a docker image

The plan is to create Docker Base Images (for various Fluentd versions) containing [Fluentd](https://www.fluentd.org/), [Logging Analytics fluentd output plugin](https://docs.oracle.com/en/learn/oci_logging_analytics_fluentd/) and other dependent plugins/gems, along with out of the box configuration for both Linux System Logs and OKE System/Service Logs.
The following deployment mechanisms are being planned to support,

  - Kubectl based deployment through sample deployment yaml configuration(s).
      - Each Deployment yaml configuration contains Fluentd config as config map and required docker image pre-filled an targeted for a specific version of Fluentd and Kubernetes.
  - Helm charts.
      - Customer would get an option to enable all other container logs (say application) in /var/log/containers using a default source, they could either choose this and modify the configuration as required (OR) they may need to modify the fluentd configuration to include the necessary log files to monitor on demand.

**OCI ServiceConnector (using Logging as Source and Logging Analytics as destination) based Log collection**

This approach is the proposed collection mechanism to collect the following type of logs,
  - OCI Service Logs integrated with OKE
  - API Server Audit Logs
  - OKE Control Plane Logs

Steps on how to build docker image is present in Lab 4.

## Learn More

* [Product Documentation](https://docs.oracle.com/en-us/iaas/logging-analytics/index.html)

## Acknowledgements
* **Author** - Ashwini R, Senior Member of Technical Staff
* **Contributors** -  Kumar Varun, Product Manager
* **Last Updated By/Date** - <Name, Group, Month Year>
