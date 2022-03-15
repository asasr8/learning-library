
# Introduction

This lab walks you through the steps to create a docker image.
Once we have a docker image it can be then pushed to OCIR registry.

Estimated Lab Time: n minutes


## Objectives


In this lab, you will:
* Create Docker File for creating FluentD container image with Logging Analytics output plugin
* Push the container image to your container registry / OCIR


## **STEP 1**: Create a docker image
  Below are the steps to create a docker image.
  ```
  # Change directory to docker-image
  cd docker-image/

  # Build the docker image, you may use name of your choice for the image name (fluentd_loganalytics)
  docker build -t fluentd_loganalytics -f Dockerfile .
  ```
  NOTE : The sample config files can be found [here](https://confluence.oci.oraclecorp.com/download/attachments/547589578/fluentd-kubernetes-daemonset-logging_analytics.zip?version=3&modificationDate=1626448288481&api=v2)

## **STEP 2**: Push the image to registry
  Below are the steps to push the image.
  ```
  $ docker login phx.ocir.io
  Username: xyz/oracle/ASHWINI.A.R@ORACLE.COM
  Password:
  Login Succeeded

  # To view the image built from local repo
  $ docker image ls |grep fluend_loganalytics
  fluend_loganalytics                            latest    b089c74670bc   2 seconds ago   398MB

  # To Push the Image to a Docker registry, first tag using the registry info.
  # Tag the image. tag looks like, <container-registry>/<Namespace/UserId>/<repo_name>:<version>
  docker tag fluentd_loganalytics:latest <tag>
  $ docker tag fluentd_loganalytics:latest phx.ocir.io/xyz/kube-la-demo:latest

  # Push the image to the registry.
  $ docker push phx.ocir.io/xyz/la-fleuntd:new
  The push refers to repository [phx.ocir.io/xyz/la-fleuntd]
  bb17d51da672: Pushed
  6946e6af4474: Pushed
  ba8219b7f775: Pushed
  39f7df7b5780: Pushed
  8c5c0b738f1a: Pushed
  703ecfb5c55a: Pushed
  c7906f515a8d: Pushed
  facc4df3ad34: Pushed
  49608a986d4b: Pushed
  1a557862c9e3: Pushed
  e0f000aa4b6c: Pushed
  57e7a4ab5e92: Pushed
  ae3be1de02e7: Pushed
  a3227ae5fd99: Pushed
  943b74aafeae: Pushed
  ea26b3b86ad5: Pushed
  476baebdfbf7: Pushed
  new: digest: sha256:75afdc123507e4c64e9142dfcdc2b0bd2c4abee1b041cf710999e59c14e8f9b4 size: 3868
  ```
  NOTE : The above is an example tag/push commands reference for OCIR Registry in IAD with namespace xyz.


## Acknowledgements
* **Author** - Ashwini R, Senior Member of Technical Staff
* **Contributors** -  Kumar Varun, Product Manager
* **Last Updated By/Date** - <Name, Group, Month Year>
