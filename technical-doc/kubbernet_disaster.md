## Kubernetes Disaster Recovery & Security Discovery Form

- **Client Name:** \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
- **Project/Application Name:** \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
- **Date:** \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_



### 1. Cluster & Cloud Information

| Question                                                                        | Response |
| ------------------------------------------------------------------------------- | -------- |
| What cloud provider are you using? (AWS / GCP / Azure / On-prem)                |          |
| How was your Kubernetes cluster created? (eksctl, terraform, GKE console, etc.) |          |
| What Kubernetes version are you currently running?                              |          |
| How many clusters do you operate (prod, staging, dev)?                          |          |
| Is high availability (multi-zone or multi-region) enabled?                      |          |



### 2. Application Deployment

| Question                                                          | Response     |
| ----------------------------------------------------------------- | ------------ |
| How are applications deployed? (Helm, ArgoCD, Flux, kubectl)      |              |
| Do you store your deployment configurations in Git (GitOps)?      |  |
| Do your workloads include StatefulSets (e.g., databases, queues)? |        |
| What types of services are exposed (APIs, web apps, etc.)?        |              |



### 3. Backup & Restore

| Question                                                             | Response |
| -------------------------------------------------------------------- | -------- |
| Do you currently back up the cluster (etcd, manifests)? If yes, how? |          |
| Do you use a tool like Velero, Kasten, or Stash?                     |    |
| What is your **Recovery Point Objective (RPO)?** (e.g., 15 mins)     |          |
| What is your **Recovery Time Objective (RTO)?** (e.g., 2 hours)      |          |
| Are there regular snapshot schedules for persistent volumes?         |     |
| Where are backups stored? (S3, GCS, Azure Blob, NFS, etc.)           |          |



###  4. Database & Storage

| Question                                                                          | Response |
| --------------------------------------------------------------------------------- | -------- |
| Which databases are in use? (e.g., PostgreSQL, MySQL, MongoDB)                    |          |
| Are these databases running inside the cluster or managed externally (e.g., RDS)? |          |
| How are DB backups handled? (Tool, frequency, storage)                            |          |



### 5. Secrets & Configuration

| Question                                                         | Response |
| ---------------------------------------------------------------- | -------- |
| How are secrets managed? (Kubernetes Secrets, Vault, SOPS, etc.) |          |
| Are secrets encrypted at rest?                                   |     |
| Are config files versioned and stored in Git?                    |     |



###  6. Networking & Ingress

| Question                                                             | Response |
| -------------------------------------------------------------------- | -------- |
| Which Ingress controller is used? (NGINX, ALB, Traefik, Istio, etc.) |          |
| Are external DNS records managed automatically?                      |     |
| Is HTTPS (TLS) enforced on all services?                             |     |
| Are there NetworkPolicies defined for pod-to-pod communication?      |    |



### 7. Monitoring & Alerts

| Question                                                                | Response |
| ----------------------------------------------------------------------- | -------- |
| What monitoring stack is in place? (Prometheus, Grafana, Datadog, etc.) |          |
| Is AlertManager or another alerting tool configured?                    |     |
| Are alerts connected to a communication tool (Slack, email, PagerDuty)? |     |
| Are audit logs collected for Kubernetes activity?                       |     |



### 8. Security & Compliance

| Question                                                               | Response |
| ---------------------------------------------------------------------- | -------- |
| Are container images scanned for vulnerabilities? (Trivy, Clair, etc.) |     |
| Are RBAC permissions limited by role and namespace?                    |    |
| Is there a PodSecurity or OPA/Kyverno policy in place?                 |     |
| Are you targeting compliance (CIS, SOC 2, PCI-DSS)?                    |     |



### 9. DR Testing & Automation

| Question                                                                               | Response |
| -------------------------------------------------------------------------------------- | -------- |
| Do you conduct disaster recovery simulations? If yes, how often?                       |          |
| Do you use automation tools for restoration? (e.g., Terraform, Ansible, shell scripts) |    |
| Would you like automated DR scripts provided as part of this project?                  |    |


###  10. Team & Contacts

| Role                 | Name | Email | Slack/Phone |
| -------------------- | ---- | ----- | ----------- |
| DevOps Lead          |      |       |             |
| Application Owner    |      |       |             |
| Infrastructure Admin |      |       |             |



### Additional Notes

> Please share any additional architecture diagrams, GitHub repositories, or backup policy documents if available.

