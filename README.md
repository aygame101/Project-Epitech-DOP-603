# Project-Epitech-DOP-603


## Gestion Avancement du Projet
🔴 To do  
🟠 In progress  
🟢 Done
| Avancement | Tâches |
| :--------- |:------ |
| 🟠 In progress | Le déploiement du Result est OK |
| 🟠 In progress | Le déploiement du Worker est OK |
| 🟠 In progress | Le déploiement de Postgres est OK |
| 🟠 In progress | Le déploiement de Redis est OK |
| 🟠 In progress | Le déploiement de Traefik est OK |
| 🟠 In progress | Le configmap de Postgres est OK |
| 🟠 In progress | Le configmap de Redis est OK |
| 🟠 In progress | Les secrets Postgres sont correctement définis et stockés |
| 🟠 In progress | Les variables d'environnement du Poll sont correctement définies |
| 🟠 In progress | Les variables d'environnement du Result sont correctement définies |
| 🟠 In progress | Les variables d'environnement de Postgres sont correctement définies |
| 🟠 In progress | Un volume persistant existe pour Postgres |
| 🟠 In progress | Le volume Postgres est déployé correctement |
| 🟠 In progress | Le service Postgres est correctement configuré |
| 🟠 In progress | Le service Redis est correctement configuré |
| 🟠 In progress | Le service Poll est correctement configuré |
| 🟠 In progress | Le service Traefik est correctement configuré |
| 🟠 In progress | Les règles de routage du trafic Poll sont correctement définies |
| 🟠 In progress | L'affinité du Poll est correctement configurée |
| 🟠 In progress | Les ressources du Poll sont correctement configurées |
| 🟠 In progress | L'affinité du Result est correctement configurée |
| 🟠 In progress | Les ressources du Result sont correctement configurées |
| 🟠 In progress | L'affinité du Traefik est correctement configurée |
| 🟠 In progress | Le monitoring des ressources et performances est correctement configuré |
| 🟠 In progress | La quantité et les chemins des volumes surveillés sont correctement configurés |
| 🟠 In progress | Toutes les tâches ont été effectuées |


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
