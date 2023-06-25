Nginx and ArgoCD installation with patches to configure it to work with Azure AD

# Install ArgoCD and NginX

## Setup the variables

Copy the following files and fill in the variables wherever the REPLACE comment is found:

* `argocd-cm-patch.yaml.example` to `argocd-cm-patch.yaml` 
* `argocd-secret-patch.yaml.example` to `argocd-secret-patch.yaml`

## Add TLS certificates

Create a folder called `certificates` and add the following files from your TLS certificate

* tls.crt: The TLS certificate
* tls.key: The TLS private key

You may also copy the `certificates-exmaple` folder to use the sample certificates.

## Run the installation

First install the certificates and ArgoCD

```bash
kubectl apply -k .
```

Then install the nginx ingress controller

```bash
helm upgrade --install ingress-nginx ingress-nginx \
  --repo https://kubernetes.github.io/ingress-nginx \
  --namespace ingress-nginx --create-namespace \
  -f nginx/values.yaml
```