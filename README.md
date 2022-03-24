# This is a CloudBuild integrating with GKE Lab

1. Grant CloudBuild access permission to GKE [1]
2. Create a docker Artifact repo and GKE
```bash
gcloud artifacts repositories create demo --repository-format=docker --location=asia-east1
gcloud container clusters create demo-cluster --zone=asia-east1-b
```

3. Add GCE SA to artifacts repositories [2]
4. Run CloudBuild and check the result
```
cd cloudbuild-lab
gcloud builds submit --config=cloudbuild.yaml --substitutions=_PROJECT_ID=$DEVSHELL_PROJECT_ID
gcloud container clusters get-credentials demo-cluster --zone=asia-east1-b
# check the resilt in Kubernetes
kubectl get pods
kubectl get svc
```
5. Delete GKE
```
gcloud container clusters delete demo-cluster --zone=asia-east1-b
```

REF
---
- [1] https://cloud.google.com/kubernetes-engine/docs/tutorials/gitops-cloud-build#granting_access_to
- [2] https://cloud.google.com/artifact-registry/docs/access-control#compute
- https://cloud.google.com/build/docs/configuring-builds/substitute-variable-values
- https://cloud.google.com/build/docs/building/build-containers
- https://cloud.google.com/build/docs/build-config-file-schema
