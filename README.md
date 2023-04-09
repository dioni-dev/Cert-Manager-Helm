# cert-manager Helm Chart

This Helm chart deploys [cert-manager](https://cert-manager.io/), a Kubernetes add-on that automates the management and issuance of TLS certificates from various certificate authorities, including Let's Encrypt.

## Prerequisites

- Kubernetes 1.16+
- Helm v3.x

## Installation

1. Add the cert-manager Helm repository:

`helm repo add jetstack https://charts.jetstack.io`
`helm repo update`

2. Install the cert-manager Helm chart:

`helm install cert-manager jetstack/cert-manager --namespace cert-manager --create-namespace --version v1.7.1`


To customize the installation, you can create a custom values file and pass it during the installation using the `--values` flag. For available options, please see the [cert-manager documentation](https://cert-manager.io/docs/).

## Configuration

After installing cert-manager, you need to configure an issuer or cluster issuer for certificate management. Please refer to the [official documentation](https://cert-manager.io/docs/configuration/) for more information on configuring issuers.

## Usage

To request a certificate, create a `Certificate` resource in your Kubernetes cluster that refers to the issuer you have configured. For example:

```yaml
apiVersion: cert-manager.io/v1
kind: Certificate
metadata:
name: my-certificate
namespace: default
spec:
secretName: my-certificate-tls
dnsNames:
 - example.com
issuerRef:
 name: my-issuer
 kind: Issuer
```

For more information on using cert-manager, please refer to the official documentation.