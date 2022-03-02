# Ingesting Linux or Windows Logs with Management Agent

## Introduction

This lab will install Oracle Management Agent on a Linux Host

Estimated Lab Time: 30 documentation

### Objectives

In this lab, you will:
* Create Agent Installation Keys for Management Agent software to communicate with OCI
* Install and verify management agent for log collection

### Prerequisites

* An Oracle Cloud Environment


Install Management Agents on your Hosts

Now we will walk through installing management agents on our hosts. Because we are using linux servers in this lab we will stick to steps for those servers. For further documentation on installing agents and specifically on Windows servers refer to [Install Management Agents Documentation](https://docs.oracle.com/en-us/iaas/management-agents/doc/install-management-agent-chapter.html#GUID-5F2A1CEF-1185-469C-AF2E-8A94BC95DC35)

## **STEP :**  Create and Download Keys
1. In the OCI Console navigate to Management Agents - Downloads and Keys
     ![](./images/download-and-keys.png " ")

2. Click and download **Agent for LINUX**

3. Click **Create Key** below

  a. Name the key `ebs_agent_key`

  b. Select our `ebshol_compartment`

  c. Click **Create**

  d. on the right click the three dots in the row of our agent key we just created.

  e. Click `Download Key to File`

  ![](./images/keydownload.png " ")

  f. Once you have Downloaded the key file, we need to edit it

  g. open the `ebs_agent_key.txt` file

      Add agent name
        - AgentDisplayName

      Add Password
        - CredentialWalletPassword

      Uncomment the Service Plugins
        - Service.plugin.dbaas.download=true
        - Service.plugin.dbaas.download=true

    ![](./images/editkey.png " ")

4. We now need to copy our `oracle.mgmt_agent.rpm` and `ebs_agent_key.txt` to our Cloud Manager Instance.

5. Verify an SSH connection to our `ebshol_ebscm` instance

  a. Navigate to Compute and find your `ebshol_ebscm` and note the Public IP

  b. From your terminal SSH to the Cloud Manager

    ```
    ssh opc@<public_ip_of_cloud_manager>
    ```

  c. After verifying you can connect via ssh exit

  ![](./images/sshverify.png " ")

6. Secure Copy your management agent and .txt file to cloud manager

    ```
    scp ~/Downloads/oracle.mgmt_agent.rpm opc@<public_ip_of_cloud_manager>:~
    scp ~/Downloads/ebs_agent_key.txt opc@<public_ip_of_cloud_manager>:/tmp
    ssh opc@<public_ip_of_cloud_manager>
    ```

  a. Type ls to verify your .txt and .rpm file are in your home directory

7. Install Java

    ```
    <copy>
    sudo yum install java
    </copy>
    ```

8. Edit permissions on the `ebs_agent_key.txt` file

    ```
    <copy>
    cd /tmp
    sudo chmod 755 ebs_agent_key.txt
    </copy>
    ```

  a. Go back to home directory and run management agent

    ```
    <copy>
    cd ~
    sudo rpm -ivh oracle.mgmt_agent.rpm
    </copy>
    ```

  Note: If successful your terminal should see this response ending with Agent install successful

  ![](./images/installsuccess.png " ")

9. Setup and the management agent with info from Install Key

    ```
    <copy>
    sudo /opt/oracle/mgmt_agent/agent_inst/bin/setup.sh opts=/tmp/ebs_agent_key.txt
    </copy>
    ```

  ![](./images/startagent.png " ")

10. Now to install our agent on the other instances built with our cloud manager we will move the `ebs_agent_key.txt` and oracle mgmt agent to our Oracle Home Directory

    ```
    <copy>
    sudo mv /tmp/ebs_agent_key.txt /u01/install/APPS
    sudo mv oracle.mgmt_agent.rpm /u01/install/APPS
    sudo su - oracle
    </copy>
    ```

11. From the Oracle user on the cloud manager you can connect to your other instances using ssh. Now scp your management agent and key file to each of the other instances via their private IP address.

    ```
    scp oracle.mgmt_agent.rpm opc@<privateIPofebsinstance>:~
    scp ebs_agent_key.txt opc@<privateIPofebsinstance>:/tmp
    ssh opc@<privateIPofebsinstance>
    ```

12. Go to the /tmp folder and using vi, edit the `ebs_agent_key.txt` file and change the name to refer to the server. We will use the same .txt file.

13. Once you edited the `ebs_agent_key.txt` file you can repeat the steps for install starting from `6.` to `9.` on each instance you want to monitor then exit to repeat.

Note: You can also follow the recommended procedure of deleting your key file from your instance one the agent has been installed and is configured properly

  ```
  $ rm /tmp/ebs_agent_key.txt
  ```

**Note:** If you have other instances not created with the cloud manager follow the same steps to add the agent and key file to those instances and install.

This will now complete the Ingest Logs to Logging Analytics Lab for this workshop.

You may now proceed to the next lab.

## Acknowledgements
* **Author** - Quintin Hill, Cloud Engineering, Packaged Applications
* **Contributors** -  Kumar Varun, Logging Analytics Product Management
* **Last Updated By/Date** - Quintin Hill, Cloud Engineering, Mar 8 2021
