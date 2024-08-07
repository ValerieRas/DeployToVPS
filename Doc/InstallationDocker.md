
### Sur une distribution basée sur Debian (comme Ubuntu) :

1. **Met à jour les paquets :**
    
    ```bash
    
    sudo apt update
    
    ```
    
2. **Installe les paquets nécessaires :**
    
    ```bash
    
    sudo apt install apt-transport-https ca-certificates curl software-properties-common
    
    ```
    
3. **Ajoute la clé GPG officielle de Docker :**
    
    ```bash
    
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    
    ```
    
4. **Ajoute le dépôt Docker :**
    
    ```bash
    
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    
    ```
    
5. **Mets à jour les informations sur les paquets :**
    
    ```bash
    
    sudo apt update
    
    ```
    
6. **Installer Docker :**
    
    ```bash
    
    sudo apt install docker-ce
    
    ```
    
7. **Démarre et active le service Docker :**
    
    ```bash
    
    sudo systemctl start docker
    sudo systemctl enable docker
    
    ```
    
8. **Vérifie que Docker est bien installé :**
    
    ```bash
    
    sudo docker --version
    
    ```
    
- **Connexion docker**

  ```bash
    
    sudo docker login
    
  ```
