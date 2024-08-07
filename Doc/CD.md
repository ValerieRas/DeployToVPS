### **Préparer l'Environnement sur le VPS**

Avant de mettre en place le CD, assure-toi que PostgreSQL est installé et configuré sur ton VPS. Si PostgreSQL est déjà installé dans un conteneur Docker comme nous l'avons vu précédemment, tu dois t'assurer que les deux conteneurs (API et PostgreSQL) peuvent communiquer.

### **Lancer PostgreSQL avec Docker**

Si PostgreSQL n'est pas encore en cours d'exécution sur ton VPS, lance-le avec la commande suivante :

```bash
bashCopier le code
docker run -d \
  --name postgres-db \
  -e POSTGRES_DB=mydatabase \
  -e POSTGRES_USER=user \
  -e POSTGRES_PASSWORD=userpassword \
  -p 5432:5432 \
  postgres:13

```

### 2. **Configurer l'API pour Connexion à PostgreSQL**

Dans ton application API C#, configure les variables d'environnement pour se connecter à PostgreSQL. Dans ton `Dockerfile`, tu peux passer ces variables comme paramètres `ENV` ou les définir dans la commande `docker run`.

### **Configurer les Variables d'Environnement**

Ton API doit être configurée pour utiliser les variables d'environnement pour se connecter à PostgreSQL. Voici un exemple de configuration dans un fichier `appsettings.json` pour .NET Core :

```json

{
  "ConnectionStrings": {
    "DefaultConnection": "Host=postgres-db;Port=5432;Database=mydatabase;Username=user;Password=userpassword;"
  }
}

```

### 3. **Déployer avec GitHub Actions**

Dans ton fichier de workflow GitHub Actions, ajoute les étapes pour déployer ton application API en communiquant avec PostgreSQL.

### **Créer le Workflow CD avec Docker**

Crée ou modifie `.github/workflows/cd.yml` pour inclure les étapes suivantes :

```yaml

name: CD Pipeline

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout code
      uses: actions/checkout@v3

    - name: Build Docker image
      run: |
        docker build -t my-api-image .

    - name: Log in to Docker Hub
      uses: docker/login-action@v2
      with:
        username: ${{ secrets.DOCKER_HUB_USERNAME }}
        password: ${{ secrets.DOCKER_HUB_ACCESS_TOKEN }}

    - name: Push Docker image to Docker Hub
      run: |
        docker tag my-api-image my-dockerhub-username/my-api-image:latest
        docker push my-dockerhub-username/my-api-image:latest

    - name: Deploy to VPS
      run: |
        ssh -o StrictHostKeyChecking=no -i ${{ secrets.SSH_PRIVATE_KEY }} user@your-vps-ip << 'EOF'
          # Pull the latest Docker image
          docker pull my-dockerhub-username/my-api-image:latest

          # Stop and remove old API container if it exists
          docker stop my-api-container || true
          docker rm my-api-container || true

          # Run the new API container with PostgreSQL link
          docker run -d \
            --name my-api-container \
            -p 3000:3000 \
            --link postgres-db:db \
            -e DB_HOST=postgres-db \
            -e DB_USER=user \
            -e DB_PASSWORD=userpassword \
            -e DB_NAME=mydatabase \
            my-dockerhub-username/my-api-image:latest
        EOF
      env:
        SSH_PRIVATE_KEY: ${{ secrets.SSH_PRIVATE_KEY }}

```

### 4. **Configurer les Secrets GitHub**

Assure-toi que les secrets nécessaires sont configurés dans GitHub pour accéder à Docker Hub et à ton VPS :

- **`DOCKER_HUB_USERNAME`** : Ton nom d'utilisateur Docker Hub.
- **`DOCKER_HUB_ACCESS_TOKEN`** : Jeton d'accès Docker Hub.
- **`SSH_PRIVATE_KEY`** : Clé privée SSH pour accéder à ton VPS.

### Résumé des Étapes pour le CD

1. **Préparer le VPS :**
    - Lancer PostgreSQL si ce n’est pas déjà fait.
    - Assurer la connectivité entre les conteneurs API et PostgreSQL.
2. **Configurer ton API C# pour se connecter à PostgreSQL :**
    - Utiliser les variables d'environnement pour la connexion.
3. **Mettre en place le Workflow GitHub Actions :**
    - **Construire et pousser l’image Docker.**
    - **Déployer l’image sur le VPS.**
4. **Configurer les secrets GitHub :**
    - Pour Docker Hub et l’accès SSH au VPS.
