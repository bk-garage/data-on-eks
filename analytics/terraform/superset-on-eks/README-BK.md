# Bulent's Notes

## Modifications

In `main.tf`:
* Comment out `core_node_group`
* Reduce `superset_node_group` size to 1 (desired 2)
* Reduce volume_size to 10
* Reduce instance_types to `m5.large`

Add `terraform.tfvars`:
```
region = "eu-west-2"
```

## Deployment

Followed this for deployment and access to Superset:
https://awslabs.github.io/data-on-eks/docs/blueprints/data-analytics/superset-on-eks

Connected to the EKS cluster as explained here: https://docs.aws.amazon.com/eks/latest/userguide/create-kubeconfig.html

```zsh
aws eks update-kubeconfig --region eu-west-2 --name superset-on-eks
```

```zsh
kubectl get ingress  -n superset -o json | jq -r '"http://" + .items[0].status.loadBalancer.ingress[0].hostname'
```

Downloaded sample data (CSV) here: https://www.ecdc.europa.eu/en/covid-19/data

## Deletion

> **Don't forget to delete the EBS volumes after deleting the cluster.**
