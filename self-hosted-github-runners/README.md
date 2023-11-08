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

    ```{"github_app_private_key":"-----BEGIN RSA PRIVATE KEY-----\blablabla==\n-----END RSA PRIVATE KEY-----\n","github_app_id":"123456","github_app_installation_id":"12345678"}```
app_id  located in genral configuration
app_installation id located in installation page in the url example : https://github.com/organizations/beti-safety/settings/installations/<ID>
5. pull it with external secret manifest under /templates/external-secret.yaml

6. install with argocd application :
```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: github-runner
  namespace: argocd
  labels:
    type: infra
    cluster: {{ .Values.cluster_name }}
spec:
  project: {{ .Values.argocd.project }}
  source:
    repoURL: git@github.com:beti-safety/argocd.git
    path: helm/beti-github
    targetRevision: auto1
    helm:
      values: |
        externalSecretName: controller-manager
        externalSecretSecretStoreRefName: secret-store
        externalSecretRemoteRefKey: github-token
        externalSecretRemoteRefProperty: GITHUB_TOKEN
        runnerDeploymentName: org-runners
        github_orginzation: org
        runnerLabels:
          - org-runners
          - github-self-hosted-runners
        runnerGroup:
          - org-runners
        actions-runner-controller:
          enabled: true

  destination:
    namespace: actions-runner-system
    server: {{ .Values.cluster_address }}
  syncPolicy:
    syncOptions:
      - CreateNamespace=true
      - ServerSideApply=true
    automated:
      prune: true
      selfHeal: true

```
or with helm install
```bash
helm install -n github-runners github ./  
```
 