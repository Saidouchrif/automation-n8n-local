![n8n Logo](https://raw.githubusercontent.com/n8n-io/n8n/master/assets/n8n-logo.png)

# Automation n8n Local

Ce dépôt propose un environnement clé-en-main pour exécuter n8n en local via Docker Compose. Il a été développé avec soin par Said Ouchrif pour faciliter le prototypage, les démonstrations et les tests de flux d’automatisation n8n.

## 🚀 Aperçu

- **Technologie principale :** [n8n](https://n8n.io/) (outil d’automatisation low-code)
- **Orchestration :** Docker Compose
- **Persistance :** Volume Docker `n8n_data` pour conserver les workflows, identifiants et paramètres
- **Sécurité de base :** Authentification HTTP Basic activée via le fichier `.env`

## 🧱 Architecture

```
┌───────────────┐
│   Docker      │
│  (Compose)    │
└──────┬────────┘
       │ service: n8n
       ▼
┌──────────────────────────┐
│  Conteneur n8n (5678)    │
│  • Image n8nio/n8n       │
│  • Volume: n8n_data      │
│  • Auth Basic activée    │
└──────────────────────────┘
```

## ✅ Prérequis

1. [Docker Desktop](https://www.docker.com/products/docker-desktop/) (ou moteur Docker + Docker Compose v2)
2. Accès réseau au port `5678`
3. Optionnel : compte n8n cloud si vous souhaitez synchroniser vos workflows

## ⚙️ Configuration

Tous les paramètres se trouvent dans le fichier `.env`. Ajustez-les avant le démarrage :

```env
N8N_BASIC_AUTH_ACTIVE=true
N8N_BASIC_AUTH_USER=admin
N8N_BASIC_AUTH_PASSWORD=admin123
N8N_HOST=localhost
N8N_PORT=5678
N8N_PROTOCOL=http
TZ=Africa/Casablanca
```

- **N8N_BASIC_AUTH_ACTIVE** : active la protection par mot de passe.
- **N8N_BASIC_AUTH_USER / PASSWORD** : identifiants de connexion à l’interface n8n.
- **N8N_HOST / PORT / PROTOCOL** : coordonnées pour l’accès web ; adaptez-les si vous exposez n8n en réseau.
- **TZ** : fuseau horaire des workflows et des logs.

## 🛠️ Installation & Démarrage

1. Cloner ce dépôt :
   ```bash
   git clone https://github.com/votre-compte/automation-n8n-local.git
   cd automation-n8n-local
   ```
2. Vérifier ou modifier le fichier `.env` selon votre contexte.
3. Lancer n8n en arrière-plan :
   ```bash
   docker compose up -d
   ```
4. Ouvrir l’interface web : [http://localhost:5678](http://localhost:5678) (ou le host/port configuré).

## 💻 Utilisation

1. Authentifiez-vous avec l’utilisateur et le mot de passe définis dans `.env`.
2. Créez vos workflows via l’interface drag-and-drop de n8n.
3. Définissez des déclencheurs (webhook, cron, etc.) et chaînez des intégrations.
4. Sauvegardez vos workflows ; ils resteront persistants grâce au volume Docker `n8n_data`.

### Gestion des conteneurs

- **Arrêter** : `docker compose down`
- **Voir les logs** : `docker compose logs -f`
- **Mettre à jour l’image** :
  ```bash
  docker compose pull
  docker compose up -d
  ```

## 🔧 Personnalisation

- **Ajout de backends (PostgreSQL, Redis, etc.)** : étendez `docker-compose.yml` avec des services supplémentaires.
- **Certificats SSL** : placez un reverse proxy (Traefik, Caddy, Nginx) devant n8n et modifiez `N8N_PROTOCOL=https`.
- **Extensions n8n** : montez des volumes supplémentaires pour charger des nœuds personnalisés.

## ❗ Dépannage

| Problème | Piste de résolution |
|----------|---------------------|
| Impossible d’accéder à l’UI | Vérifier que le conteneur est en cours (`docker ps`). Confirmer le port 5678 libre. |
| Authentification refusée | Mettre à jour `N8N_BASIC_AUTH_USER/PASSWORD`, relancer `docker compose up -d`. |
| Workflows non sauvegardés | S’assurer que le volume `n8n_data` n’est pas nettoyé et que Docker dispose des droits d’écriture. |

## 📚 Ressources utiles

- Documentation officielle n8n : <https://docs.n8n.io/>
- Marketplace de nœuds et d’exemples : <https://n8n.io/integrations/>
- Communauté n8n : <https://community.n8n.io/>

## 🙏 Remerciements

Projet initialement développé avec Said Ouchrif pour offrir un environnement local robuste et prêt à l’emploi autour de n8n.

---

💡 Besoin d’aller plus loin ? N’hésitez pas à enrichir ce dépôt avec vos propres recettes d’automatisation, workflows d’exemple ou guides complémentaires.
