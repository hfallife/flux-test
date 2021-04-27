- access token  Settings -> Developer Settings -> Personal Access Token -> Generate New Token -> Enable SSO

- export GITHUB_TOKEN=xxxx
- export GITHUB_USER=xxxx

flux bootstrap github \
  --owner=EnterpriseDB \
  --repository=upm-terraform \
  --branch=flux-test \
  --team=upm-admins \
  --path=./examples/fluxcd \
  --token-auth

flux create source git substrate \
  --url=https://github.com/EnterpriseDB/upm-substrate.git \
  --branch=demo \
  --interval=3s \
  --secret-ref=flux-system \
  --export > ./fluxcd/substrate-git-source.yaml

flux create kustomization service-definition \
--source=substrate \
--path=./config/k8s/variants/development/service-definition \
--prune=true \
--validation=client \
--interval=10m \
--export > ./fluxcd/service-definition.yaml

flux create kustomization service-instance \
--depends-on=service-definition \
--source=substrate \
--path=./config/k8s/variants/development/service-instance \
--prune=true \
--validation=client \
--interval=10m \
--export > ./fluxcd/service-instance.yaml

flux create kustomization superset \
--depends-on=service-definition \
--source=substrate \
--path=./config/k8s/variants/development/upm-services/superset \
--prune=true \
--validation=client \
--interval=10m \
--export > ./fluxcd/superset.yaml

flux create kustomization upm-api-admin \
--depends-on=service-definition \
--source=substrate \
--path=./config/k8s/variants/development/upm-services/upm-api-admin \
--prune=true \
--validation=client \
--interval=10m \
--export > ./fluxcd/upm-api-admin.yaml

flux create kustomization upm-api-provisioning \
--depends-on=service-definition \
--source=substrate \
--path=./config/k8s/variants/development/upm-services/upm-api-provisioning \
--prune=true \
--validation=client \
--interval=10m \
--export > ./fluxcd/upm-api-provisioning.yaml

flux create kustomization upm-event-collector \
--depends-on=service-definition \
--source=substrate \
--path=./config/k8s/variants/development/upm-services/upm-event-collector \
--prune=true \
--validation=client \
--interval=10m \
--export > ./fluxcd/upm-event-collector.yaml

flux create kustomization upm-ui \
--depends-on=service-definition \
--source=substrate \
--path=./config/k8s/variants/development/upm-services/upm-ui \
--prune=true \
--validation=client \
--interval=10m \
--export > ./fluxcd/upm-ui.yaml


flux create kustomization upm-services \
--depends-on=service-definition \
--source=substrate \
--path=./config/k8s/variants/development/upm-services \
--prune=true \
--validation=client \
--interval=10m \
--export > ./fluxcd/upm-services.yaml






under flux-repo, git commit and git push


- AzureIdentity
- AzureIdentityBinding