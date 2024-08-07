### 1. **Lancer PostgreSQL avec Docker**

1. **Lance le conteneur PostgreSQL :**
    
    ```bash
    
    sudo docker run -d \
      --name postgres-db \
      -e POSTGRES_DB=mydatabase \
      -e POSTGRES_USER=user \
      -e POSTGRES_PASSWORD=userpassword \
      -p 5432:5432 \
      postgres:13
    
    ```
    
    - `e POSTGRES_DB` : Crée une base de données nommée `mydatabase`.
    - `e POSTGRES_USER` : Crée un utilisateur nommé `user`.
    - `e POSTGRES_PASSWORD` : Définit le mot de passe de l'utilisateur `user`.
    - `p 5432:5432` : Expose le port PostgreSQL à ton VPS.
2. **Vérifie que le conteneur PostgreSQL est en cours d'exécution :**
    
    ```bash
    
    sudo docker ps
    
    ```
    
    Tu devrais voir `postgres-db` dans la liste des conteneurs actifs.
    

### 2. **Se Connecter à PostgreSQL**

1. **Utilise le client `psql` depuis ton VPS ou un autre client PostgreSQL pour se connecter :**
    
    Si tu as `psql` installé sur ton VPS, tu peux te connecter directement au conteneur :
    
    ```bash
    
    sudo psql -h localhost -U user -d mydatabase
    
    ```
    
    - **`h localhost`** : Adresse du serveur PostgreSQL (ici localhost car le client et le serveur sont sur le même VPS).
    - **`U user`** : Nom d’utilisateur pour se connecter.
    - **`d mydatabase`** : Nom de la base de données à laquelle se connecter.
2. **Si tu n’as pas `psql` installé sur ton VPS, tu peux utiliser un client PostgreSQL comme pgAdmin ou DBeaver pour te connecter à l’adresse `localhost` sur le port `5432`.**

### 4. **Utiliser des Scripts SQL pour créer les tables et initialiser les données**

- **Créer le Fichier SQL Localement :**
    
    Place le fichier `init.sql` dans un répertoire sur ton système local, par exemple `/home/ton-utilisateur/scripts/init.sql`.
    
- **Copier le Fichier SQL dans le Conteneur :**
    
    Utilise la commande `docker cp` pour copier le fichier depuis ton système local vers le conteneur PostgreSQL.
    
    ```bash
  
    sudo docker cp /home/ton-utilisateur/scripts/init.sql postgres-db:/init.sql
    
    ```
    
- **Exécuter le Script SQL depuis le Conteneur :**
    
    Ensuite, tu exécutes le script SQL à l'intérieur du conteneur avec la commande `docker exec`.
    
    ```bash
   
    sudo docker exec -i postgres-db psql -U user -d mydatabase -f /init.sql
    
    ```
    
