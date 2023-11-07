# github-self-hosted runners on eks

A brief description of your project goes here.



## Table of Contents

- [GitHub app Installation](#installation)
- [secret manager store](#usage)
- [chart installation](#features)

## Installation

Deploy github application :
1. <github url>/settings/apps/new or settings>developer setting>github app>new app

2. Define permissions
- repository permitions:
  - actions : access r/w
  - administration : r/w
  - Checks: r/w
  - Webhooks: r/w
- organization permitions:
  - self-hosted-runners : r/w

3. save app config 

4. Save the credentials in secret manager in plain text form in this json block:

    ```{"github_app_private_key":"-----BEGIN RSA PRIVATE KEY-----\nMIIEpAIBAAKCAQEA2kuoG+tuYMID/lAiSEOzkXxoOM82eD507bllblablablaUQXMZxxevTUXiWsKSGsEzKSKhs6KSveExe6\nBjloLsmkxceoWTi88XadEP0CgYA8k/r7KqLlPesqkAYvYH+OD3iERXDF0d5IDvzG\nGpzxklJ2OBQmk96AWlsHTM+EvTI+118A3nfmINWgw2OT0+nE+jrWmX+c0qSXvJZQ\nqmfaXP64dxhtFAqCVyWlx7M1R/aSRso2IVn0qeIeO0aBoair6uMFBAkhuHphksDN\nYBQoQQKBgQC2ylirPxn4NywuysPIAhiXlieMJiieOos3rcgUwh+lUt5XYAgMFNit\nxQB2oLbfqeVS7t0gMdCfqf02HD8zOlh5cLLDiRv/riN/3KMBRHdKFUpkrQanmAY5\nWTynIMAgoX8qyKUJYdh9goxs6La51ZDLEf+V772NE7Q1DlVPzkUSNQ==\n-----END RSA PRIVATE KEY-----\n","github_app_id":"123456","github_app_installation_id":"12345678"}```
app_id  located in genral configuration
app_installation id located in installation page in the url example : https://github.com/organizations/beti-safety/settings/installations/<ID>
5. pull it with external secret manifest under /templates/external-secret.yaml

