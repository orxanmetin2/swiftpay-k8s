# SwiftPay - Banking Microservices on Kubernetes 🏦

## Architecture
```
[Client] → [Nginx Ingress] → [Auth Service :4001]
                           → [Account Service :4002]
                           → [Transfer Service :4003]
                                    ↓
                           [PostgreSQL DBs]
                                    ↓
                           [HashiCorp Vault]
```

## Stack
- **Cloud:** AWS EC2 (2 nodes)
- **Orchestration:** Kubernetes v1.32 (kubeadm)
- **CNI:** Calico
- **Ingress:** Nginx Ingress Controller (Helm)
- **Databases:** PostgreSQL (Helm) - per microservice
- **Secret Management:** HashiCorp Vault (Helm)
- **Monitoring:** Prometheus + Grafana (Helm)
- **Alerting:** AlertManager + Telegram Bot

## Microservices
| Service | Port | Database |
|---|---|---|
| Auth Service | 4001 | authdb |
| Account Service | 4002 | accountdb |
| Transfer Service | 4003 | transferdb |

## Monitoring
- Prometheus: `:30090`
- Grafana: `:30030`
- AlertManager: `:30093`

## Alert Rules
- Node CPU > 80% → Telegram alert
- Node RAM > 80% → Telegram alert
- Disk > 85% → Telegram alert
- Pod CrashLooping → Telegram alert
- PostgreSQL Down → Telegram alert
