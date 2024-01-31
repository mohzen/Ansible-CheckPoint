<a name="readme-top"></a>
<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="#">
    <img src="images/logo.png" alt="Logo" width="80" height="80">
  </a>

  <h3 align="center">Ansible Checkpoint Documentation</h3>

  <p align="center">
    Integration Automation Checkpoint using Ansible Playbook & AWX
    <br />
  </p>
</div>



<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li>
      <a href="#usage">Usage</a>
      <ul>
        <li><a href="#create-playbook">Create Playbook</a></li>
      </ul>
    </li>
  </ol>
</details>



<!-- ABOUT THE PROJECT -->
## About The Project

This Project is for Integrate and Automation Checkpoint Feature using Ansible & Running on top of Awx.




### Built With

Stack & Technology that been used

* [![Ansible][Ansible]][Ansible-url]
* [![Checkpoint][Checkpoint]][Checkpoint-url]
* [![Awx][Awx]][Awx-url]



<!-- GETTING STARTED -->
## Getting Started

To start Development this Project the first thing you need is to clone this repository 
```
git clone https://{{username}}@bitbucket.org/mohan_softnetx/ansible-checkpoint.git
```

### Prerequisites

You need to install ansible if you dont have it on your development env
  ```sh
  sudo apt install ansible
  ```

### Installation

for more details Intallation Ansible you can go to this documentation 
[Setup ENV Development for Ansible](https://docs.ansible.com/ansible/latest/dev_guide/developing_modules_general.html#environment-setup)

Enable Azure CLI forget token and making azure hiden apiworking
-------
```
curl -L https://aka.ms/InstallAzureCli | bash
az login --use-device-code 
# follow the login wizard after that run this command
az account get-access-token --resource=74658136-14ec-4630-ad9b-26e160ff0fc6 --query accessToken --output tsv
# use the token to access portal.azure.com api
```



<!-- USAGE EXAMPLES -->
## Usage 

To use and run this project 

```sh
  sudo ansible-playbook {{playbookfile}}.yml -vvv
```


## Create Playbook 

for creating new playbook the first thing you need is create task playbook under <b>task</b> directory ex:


```
---

- name: Make HTTP POST Request to Create Site
  uri:
    url: "https://cloudinfra-gw.portal.checkpoint.com/app/gwaas/graphql"
    method: POST
    headers:
      Content-Type: "application/json"
      x-access-token: "{{x_token}}"
      cookie: "{{cookie}}"
    body_format: json
    body: "{{ payload_create_site_dtc | to_json }}"
  register: sites
```

this playbook gonna create site into checkpoint portal with graphql payload <b>(payload_create_site_dtc)</b> 

which is the payload here collected from checkpoint inspect header for creating site under payload tab and then convert from json into yaml configuration
ex : 


```
---
payload_create_site_dtc:
  operationName: "addSiteMutation"
  variables:
    data:
      name: "{{siteNameDtc}}"
      description: "{{siteDescDtc}}"
      type: "dataCenter"
      routerSubnets: 
      - "{{routerSubnetsDtc}}"
      preSharedKey: "{{sitePreSharedKeyDtc}}"
      tunnelType: "{{siteTunnelIpDtc}}"
  query: "mutation addSiteMutation($data: AddSiteInput!) {\n  addSite(data: $data)\n}\n"

```


<!-- CONTACT -->
## Contact

viyancs - msofyancs@gmail.com

<p align="right">(<a href="#readme-top">back to top</a>)</p>


<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[Ansible]: https://img.shields.io/badge/ansible-000000?style=for-the-badge&logo=ansible&logoColor=white
[Checkpoint]: https://img.shields.io/badge/checkpoint-FFC0CB?style=for-the-badge&logo=checkpoint&logoColor=pink
[Awx]: https://img.shields.io/badge/awx-000000?style=for-the-badge&logo=awx&logoColor=white
[Checkpoint-url]: https://portal.checkpoint.com/
[Ansible-url]: https://ansible.com/
[Awx-url]: https://github.com/ansible/awx
