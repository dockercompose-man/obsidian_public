# [](https://github.com/ChristianLempa/boilerplates/blob/main/kubernetes/certmanager/README.md#installation)Installation

## [](https://github.com/ChristianLempa/boilerplates/blob/main/kubernetes/certmanager/README.md#deployment)

## Deployment

1.  Add the Helm Repository & Update

helm repo add jetstack https://charts.jetstack.io

helm repo update

2.  Install Cert-Manager with Helm & CRDs

helm install cert-manager jetstack/cert-manager --namespace cert-manager --create-namespace --set installCRDs=true

## [](https://github.com/ChristianLempa/boilerplates/blob/main/kubernetes/certmanager/README.md#configuration)

## Configuration

Add your Issuer or ClusterIssuer Objects, Credentails and Certificates.

_For more info visit:_ [Official Cert-Manager Documentation](https://cert-manager.io/docs/)

# [](https://github.com/ChristianLempa/boilerplates/blob/main/kubernetes/certmanager/README.md#best-practices--post-installation)

# Best-Practices & Post-Installation

## [](https://github.com/ChristianLempa/boilerplates/blob/main/kubernetes/certmanager/README.md#troubleshooting)

## Troubleshooting

You can troubleshoot issues and inspect log entries for the Certificate Objects with the `kubectl describe` command.

_For more info visit:_ [Official Cert-Manager Troubleshooting Guide](https://cert-manager.io/docs/faq/troubleshooting/)

# [](https://github.com/ChristianLempa/boilerplates/blob/main/kubernetes/certmanager/README.md#additional-referfences)

# Additional Referfences

[Official Cert-Manager Documentation](https://cert-manager.io/docs/)