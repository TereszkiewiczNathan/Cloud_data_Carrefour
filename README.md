Projet Carrefour – mini architecture microservices
Objectif

Ce projet est un exemple simple de microservices avec Docker.
Le but est 

une API qui envoie des données

un système de messages (Kafka)

un service qui consomme et stocke les données

une autre API qui permet de les lire

Ce n’est pas un projet de prod, juste une démonstration pédagogique.

Architecture (simplement)

api1
→ reçoit un ticket (id, total)
→ l’envoie dans Kafka

Kafka + Zookeeper
→ transporte les messages

save
→ consomme les messages Kafka
→ sauvegarde les tickets

api3
→ permet de lire les tickets sauvegardés

ui
→ petite interface pour visualiser (optionnel)

Lancer le projet

Prérequis :

Docker Desktop lancé

être dans le dossier du projet

Commande unique :

docker compose up -d --build


Vérifier que tout est lancé :

docker compose ps

Test
1. Envoyer un ticket
Invoke-RestMethod -Uri http://localhost:8001/ticketsend `
-Method POST `
-ContentType "application/json" `
-Body '{"id":1,"total":10}'

2. Lire les tickets
Invoke-RestMethod http://localhost:8003/tickets


 Si un ticket apparaît, le projet fonctionne.

Ports utilisés

api1 : http://localhost:8001

api3 : http://localhost:8003

ui : http://localhost:8501

kafka : 9092

Arrêter le projet
docker compose down


Kafka peut parfois mettre quelques secondes à démarrer.
Si une API ne répond pas au premier essai, attendre un peu et réessayer.
