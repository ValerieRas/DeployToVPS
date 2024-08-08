## Installer pSQL

### **1. Installation de `psql`**

Si `psql` n’est pas encore installé sur ton système, voici comment le faire :

- **Sous Linux :**
    
    Installe PostgreSQL et `psql` en utilisant le gestionnaire de paquets :
    
    ```bash
    
    sudo apt-get update
    sudo apt-get install postgresql postgresql-contrib
    
    ```
    
- **Sous macOS :**
    
    Utilise Homebrew :
    
    ```bash
    
    brew install postgresql
    
    ```
    
- **Sous Windows :**
    
    Télécharge et installe PostgreSQL depuis [le site officiel](https://www.postgresql.org/download/windows/), ce qui inclut `psql`.
    

### **2. Connexion à une Base de Données**

Pour te connecter à une base de données PostgreSQL avec `psql` :

1. **Ouvrir un terminal ou une invite de commandes.**
2. **Utiliser `psql` pour se connecter :**
    
    Voici la commande générale :
    
    ```bash
    
    psql -h hote -U utilisateur -d base_de_donnees
    
    ```
    
    - `h` : Hôte où le serveur PostgreSQL est en cours d'exécution (par exemple, `localhost` ou l’adresse IP du serveur).
    - `U` : Nom d'utilisateur pour se connecter.
    - `d` : Nom de la base de données à laquelle tu souhaites te connecter.
    
    **Exemple :**
    
    Si PostgreSQL est installé localement et que tu souhaites te connecter à une base de données nommée `mydatabase` avec l'utilisateur `myuser` :
    
    ```bash
    
    psql -U myuser -d mydatabase
    
    ```
    
    Si tu te connectes à une base de données PostgreSQL sur un conteneur Docker, le nom de l'hôte sera le nom du conteneur ou `localhost` si tu es sur la même machine.
    

### **3. Exécuter des Commandes SQL**

Une fois connecté à `psql`, tu peux exécuter des commandes SQL. Voici quelques commandes de base :

- **Afficher les bases de données :**
    
    ```sql
    
    \l
    
    ```
    
- **Afficher les tables dans la base de données actuelle :**
    
    ```sql
    
    \dt
    
    ```
    
- **Se connecter à une autre base de données :**
    
    ```sql
    
    \c nom_de_la_base
    
    ```
    
- **Créer une table :**
    
    ```sql
    
    CREATE TABLE users (
        id SERIAL PRIMARY KEY,
        username VARCHAR(50) NOT NULL,
        email VARCHAR(100) NOT NULL
    );
    
    ```
    
- **Insérer des données dans une table :**
    
    ```sql
    
    INSERT INTO users (username, email) VALUES ('john_doe', 'john.doe@example.com');
    INSERT INTO users (username, email) VALUES ('jane_doe', 'jane.doe@example.com');
    
    ```
    
- **Afficher les données d'une table :**
    
    ```sql
    
    SELECT * FROM users;
    
    ```
    
- **Modifier des données dans une table :**
    
    ```sql
    
    UPDATE users SET email = 'john.new@example.com' WHERE username = 'john_doe';
    
    ```
    
- **Supprimer des données d'une table :**
    
    ```sql
    
    DELETE FROM users WHERE username = 'john_doe';
    
    ```
    
- **Supprimer une table :**
    
    ```sql
    
    DROP TABLE users;
    
    ```
    

### **4. Quitter `psql`**

Pour quitter `psql`, utilise la commande :

```sql

\q

```

### **5. Options Avancées**

- **Afficher l'aide pour les commandes `psql` :**
    
    ```sql
    
    \?
    
    ```
    
- **Afficher l'aide pour les commandes SQL :**
    
    ```sql
    
    \h
    
    ```
    
- **Exécuter des commandes SQL depuis un fichier :**
    
    ```bash
    
    psql -U utilisateur -d base_de_donnees -f chemin/vers/fichier.sql
    
    ```
