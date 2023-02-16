# terraform-helm-argocd

[![Lint Status](https://github.com/tothenew/terraform-aws-template/workflows/Lint/badge.svg)](https://github.com/tothenew/terraform-aws-template/actions)
[![LICENSE](https://img.shields.io/github/license/tothenew/terraform-aws-template)](https://github.com/tothenew/terraform-aws-template/blob/master/LICENSE)

Terraform module for deploying Kubernetes [Argo CD](https://argoproj.github.io/argo-cd/) and related services inside a pre-existing EKS cluster.

#### Login

Initial Password
```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

ArgoCD Server URL
```bash
kubectl get ing argocd-server -n argocd -o json | jq --raw-output .status.loadBalancer.ingress[0].hostname
```

<!-- BEGIN_TF_DOCS -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 1.3.0 |
| aws | >= 3.72 |
| helm | >= 1.0, < 3.0 |
| kubernetes | >= 1.10.0, < 3.0.0 |

## Providers

| Name | Version |
|------|---------|
| helm | >= 1.0, < 3.0 |
| kubernetes | >= 1.10.0, < 3.0.0 |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| create\_namespace | Whether to create Kubernetes namespace with name defined by `namespace`. | `bool` | `true` | no |
| enabled | Variable indicating whether deployment is enabled. | `bool` | `true` | no |
| helm\_chart\_repo | Argo CD repository name. | `string` | `"https://argoproj.github.io/argo-helm"` | no |
| helm\_services | n/a | `list` | <pre>[<br>  {<br>    "chart_version": "3.26.12",<br>    "name": "argo-cd",<br>    "release_name": "argo-cd",<br>    "settings": {}<br>  }<br>]</pre> | no |
| mod\_dependency | Dependence variable binds all AWS resources allocated by this module, dependent modules reference this variable. | `any` | `null` | no |
| namespace | Kubernetes namespace to deploy Argo CD Helm chart. | `string` | `"argocd"` | no |
| settings | Additional settings which will be passed to the Helm chart values. | `map` | `{}` | no |

## Outputs

No outputs.
<!-- END_TF_DOCS -->

## Authors

Module managed by [TO THE NEW Pvt. Ltd.](https://github.com/tothenew)

## License

Apache 2 Licensed. See [LICENSE](https://github.com/tothenew/terraform-aws-template/blob/main/LICENSE) for full details.
