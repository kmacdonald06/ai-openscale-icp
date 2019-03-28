---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:download: .download}

# Retrieving log files for Support
{: #log-files}

Learn how to retreive log files for {{site.data.keyword.icpfull}}, and send those files to IBM Support.
{: shortdesc}

These are the key steps:

- Log into the ICP cluster

    - Ensure that you have downloaded and installed the command line tool `cloudctl`.

    - Log into the ICP cluster, for example:

      ```curl
      cloudctl login -c id-mycluster-account -u <AdminUserName> -p <AdminPassword> -a https://169.60.000.000:1234 --skip-ssl-validation -n aiopenscale
      ```

- Retrieve log files

    - Check what pods are available:

      ```bash
      kubectl get pods --namespace aiopenscale
      ```

Example output:

| NAME | READY | STATUS | RESTARTS | AGE
|:---|:---:|:---:|:---:|:---|
| ai-open-scale-ibm-aios-bias-744df9d95d-slhnp | 2/2 | Running | 0 | 1h |
| ai-open-scale-ibm-aios-common-api-577b75c445-p9ftk | 1/1 | Running | 0 | 1h |
| ai-open-scale-ibm-aios-configuration-86b87746f8-nvt5t | 1/1 | Running | 0 | 1h |
| ai-open-scale-ibm-aios-dashboard-55444db6b6-vfxsz | 1/1 | Running | 0 | 1h |
| ai-open-scale-ibm-aios-datamart-55fc74474d-9hjw4 | 1/1 | Running | 0 | 1h |
| ai-open-scale-ibm-aios-explainability-5cdb4687f5-hln7h | 2/2 | Running | 0 | 1h |
| ai-open-scale-ibm-aios-feedback-59f7c558bd-xgd56 | 2/2 | Running | 0 | 1h |
| ai-open-scale-ibm-aios-ml-gateway-discovery-88c87d548-52ldh | 1/1 | Running | 0 | 1h |
| ai-open-scale-ibm-aios-nginx-7d7695c447-cm2j6 | 1/1 | Running | 0 | 5d |
| ai-open-scale-ibm-aios-payload-logging-84c794df8-dwsv9 | 1/1 | Running | 0 | 1h |
| ai-open-scale-ibm-aios-payload-logging-api-896674959-hzbq8 | 1/1 | Running | 0 | 1h |
| ai-open-scale-ibm-aios-scheduling-7d6d96545c-2v8s8 | 1/1 | Running | 0 | 1h |
| aios-redis-sentinel-6d5bffbcd8-dnssh | 1/1 | Running | 0 | 5d |
| aios-redis-sentinel-6d5bffbcd8-nss89 | 1/1 | Running | 0 | 5d |
| aios-redis-sentinel-6d5bffbcd8-wg992 | 1/1 | Running | 0 | 5d |
| aios-redis-server-6f4c55fd75-24nqn | 1/1 | Running | 0 | 5d |
| aios-redis-server-6f4c55fd75-5ntxb | 1/1 | Running | 0 | 5d |
| aios-redis-server-6f4c55fd75-kdqn5 | 1/1 | Running | 0 | 5d |
| etcd-0 | 1/1 | Running | 1 | 5d |
| etcd-1 | 1/1 | Running | 0 | 5d |
| etcd-2 | 1/1 | Running | 0 | 5d ||

- For the following pods:

| NAME | READY | STATUS | RESTARTS | AGE
|:---|:---:|:---:|:---:|:---|
| ai-open-scale-ibm-aios-common-api-577b75c445-p9ftk           | 1/1 |      Running |  0  |        1h |
| ai-open-scale-ibm-aios-configuration-86b87746f8-nvt5t        | 1/1 |      Running |  0  |        1h |
| ai-open-scale-ibm-aios-dashboard-55444db6b6-vfxsz            | 1/1 |      Running |  0  |        1h |
| ai-open-scale-ibm-aios-datamart-55fc74474d-9hjw4             | 1/1 |      Running |  0  |        1h |
| ai-open-scale-ibm-aios-ml-gateway-discovery-88c87d548-52ldh  | 1/1 |      Running |  0  |        1h |
| ai-open-scale-ibm-aios-nginx-7d7695c447-cm2j6                | 1/1 |      Running |  0  |        5d |
| ai-open-scale-ibm-aios-payload-logging-84c794df8-dwsv9       | 1/1 |      Running |  0  |        1h |
| ai-open-scale-ibm-aios-payload-logging-api-896674959-hzbq8   | 1/1 |      Running |  0  |        1h |
| ai-open-scale-ibm-aios-scheduling-7d6d96545c-2v8s8           | 1/1 |      Running |  0  |        1h |
| aios-redis-sentinel-6d5bffbcd8-dnssh                         | 1/1 |      Running |  0  |        5d |
| aios-redis-sentinel-6d5bffbcd8-nss89                         | 1/1 |      Running |  0  |        5d |
| aios-redis-sentinel-6d5bffbcd8-wg992                         | 1/1 |      Running |  0  |        5d |
| aios-redis-server-6f4c55fd75-24nqn                           | 1/1 |      Running |  0  |        5d |
| aios-redis-server-6f4c55fd75-5ntxb                           | 1/1 |      Running |  0  |        5d |
| aios-redis-server-6f4c55fd75-kdqn5                           | 1/1 |      Running |  0  |        5d |
| etcd-0                                                       | 1/1 |      Running |  1  |        5d |
| etcd-1                                                       | 1/1 |      Running |  0  |        5d |
| etcd-2                                                       | 1/1 |      Running |  0  |        5d ||

  issue the command:

  ```bash
  kubectl logs <podName> --namespace aiopenscale > pod.log
  ```

- For the remaining pods:

| NAME | READY | STATUS | RESTARTS | AGE
|:---|:---:|:---:|:---:|:---|
| ai-open-scale-ibm-aios-bias-744df9d95d-slhnp                 | 2/2 |      Running |  0  |        1h |
| ai-open-scale-ibm-aios-explainability-5cdb4687f5-hln7h       | 2/2 |      Running |  0  |        1h |
| ai-open-scale-ibm-aios-feedback-59f7c558bd-xgd56             | 2/2 |      Running |  0  |        1h ||

  ```bash
  kubectl logs ai-open-scale-ibm-aios-explainability-5cdb4687f5-hln7h  --container aios-bias --namespace aiopenscale
  ```

  Container names will be displayed when using the earlier command:

  ```bash
  kubectl logs <podName> --namespace aiopenscale > pod.log
  ```

- Package and send log files to IBM Support

    - Zip your logs, and send the compressed files to [IBM Support ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/home/)
