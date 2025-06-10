# Project-Epitech-DOP-603
  
  
## Gestion Avancement du Projet
🔴 To do  
🟠 In progress  
🟢 Done
| Avancement | Tâches |
| :--------- |:------ |
| 🟢 Done | Le déploiement du Result est OK |
| 🟢 Done | Le déploiement du Worker est OK |
| 🟢 Done | Le déploiement de Postgres est OK |
| 🟢 Done | Le déploiement de Redis est OK |
| 🟢 Done | Le déploiement de Traefik est OK |
| 🟢 Done | Le configmap de Postgres est OK |
| 🟢 Done | Le configmap de Redis est OK |
| 🟢 Done | Les secrets Postgres sont correctement définis et stockés |
| 🟢 Done | Les variables d'environnement du Poll sont correctement définies |
| 🟢 Done | Les variables d'environnement du Result sont correctement définies |
| 🟢 Done | Les variables d'environnement de Postgres sont correctement définies |
| 🟢 Done | Un volume persistant existe pour Postgres |
| 🟢 Done | Le volume Postgres est déployé correctement |
| 🟢 Done | Le service Postgres est correctement configuré |
| 🟢 Done | Le service Redis est correctement configuré |
| 🟢 Done | Le service Poll est correctement configuré |
| 🟢 Done | Le service Traefik est correctement configuré |
| 🟢 Done | Les règles de routage du trafic Poll sont correctement définies |
| 🟢 Done | L'affinité du Poll est correctement configurée |
| 🟢 Done | Les ressources du Poll sont correctement configurées |
| 🟢 Done | L'affinité du Result est correctement configurée |
| 🟢 Done | Les ressources du Result sont correctement configurées |
| 🟢 Done | L'affinité du Traefik est correctement configurée |
| 🟢 Done | Le monitoring des ressources et performances est correctement configuré |
| 🟢 Done | La quantité et les chemins des volumes surveillés sont correctement configurés |
| 🟢 Done | Toutes les tâches ont été effectuées |


# Lancer l'app :

## Ajouter dans C:\Windows\System32\drivers\etc\hosts :
127.0.0.1 poll.dop.io result.dop.io  
(commande windows, powershell en admin) :  
``Add-Content -Path C:\Windows\System32\drivers\etc\hosts -Value "127.0.0.1 poll.dop.io"``  
``Add-Content -Path C:\Windows\System32\drivers\etc\hosts -Value "127.0.0.1 result.dop.io"``  

Pour Mac:  
``echo "127.0.0.1 poll.dop.io" | sudo tee -a /etc/hosts > /dev/null``  
``echo "127.0.0.1 result.dop.io" | sudo tee -a /etc/hosts > /dev/null``  
  
``tail -n 10 /etc/hosts``   
``sudo dscacheutil -flushcache; sudo killall -HUP mDNSResponder``  
  
  
## Les différentes pages :  
  
### Page de vote  
http://poll.dop.io:30021  
  
### Page de résultats  
http://result.dop.io:30021   
  
### Page Traefik  
http://localhost:30042/dashboard#/  
  
  
# Commandes dans l'ordre :  
## Créer le cluster KIND  
(lancer docker)  
``kind create cluster --config=kind-config.yaml --name=dop603``  
``kubectl cluster-info --context kind-dop603``  

## Namespace kube-public (Si n'existe pas)  
``kubectl create namespace kube-public``  
  
## Monitoring (cadvisor)  
``kubectl apply -f cadvisor.daemonset.yaml``  
  
## PostgreSQL  
``kubectl apply -f postgres.secret.yaml -f postgres.configmap.yaml -f postgres.volume.yaml -f postgres.deployment.yaml -f postgres.service.yaml``  
  
## Redis  
``kubectl apply -f redis.configmap.yaml -f redis.deployment.yaml -f redis.service.yaml``  
  
## Poll  
``kubectl apply -f poll.deployment.yaml -f worker.deployment.yaml -f result.deployment.yaml -f poll.service.yaml -f result.service.yaml -f poll.ingress.yaml -f result.ingress.yaml``  
  
## Traefik  
``kubectl apply -f traefik.rbac.yaml  -f traefik.deployment.yaml  -f traefik.service.yaml``  
  
## Table sql  
``kubectl exec -i deployment/postgres -- psql -U postgres -c "CREATE TABLE IF NOT EXISTS votes (id VARCHAR(255) PRIMARY KEY, vote VARCHAR(255) NOT NULL);"``  


# Relancer l'app :  
  
## Services applicatifs  
``kubectl apply -f worker.deployment.yaml``