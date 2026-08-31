## Install

'''
    $ pyenv local 3.12.9
    $ python3 -m venv .venv-theguardian
    $ source .venv-theguardian/bin/activate
    $ pip install --upgrade pip
    $ pip install -r requirements.txt# Installation complète en dev
    $ pip install -r requirements-torch.txt
    $ pip install torch --index-url https://download.pytorch.org/whl/cpu
'''

### Jenkins

'''
    $ docker compose -f docker-compose.yaml down --remove-orphans
    $ cd _server-jenkins
    $ docker compose build --no-cache
    $ docker-compose up -d
'''
1. Ouvrir localhost:9105
2. Nouveau job → Pipeline
3. Coller l'URL GitHub du repo
4. Jenkins trouve le Jenkinsfile à la racine automatiquement


##### Configurer (le job)

**General**

✓ Do not allow concurrent builds ✓ — évite deux builds simultanés sur le même workspace
✓ GitHub project ✓ — colle l'URL du repo : https://github.com/GitHub_User/Project_Name
✓ Supprimer les anciens builds ✓ — puis mettre 10 dans "Nombre de builds à conserver"

**Triggers**

✓  GitHub hook trigger for GITScm polling

**Pipeline**

Definition : Pipeline script from SCM
SCM : Git
Repository URL : https://github.com/GitHub_User/Project_Name.git
Credentials : + Ajouter
Branch : */main
Script Path : Jenkinsfile

##### Administrer Jenkins

**Configuration du système / Plugins**

Installer le plugin GitHub dans Jenkins
Administrer Jenkins → Plugins → Available
→ chercher "GitHub" → installer "GitHub Integration "

**Sécurité / Security**

Git plugin notifyCommit access tokens → Current access tokens → + Add new access token
Ex : 'github-webhook' → Copier Token

**Sécurité / Credentials

→ Add Credentials
→ Kind : Secret text
→ Secret : https://discord.com/api/webhooks/1**************USER **************/********HOOK**************
→ ID : discord-webhook
→ Save

##### NGROK

Note pour une machine derrière une box
Rendre Jenkins accessible depuis GitHub: Jenkins tourne sur localhost:9105 — GitHub ne peut pas l'atteindre. Il faut un tunnel. 
'''
    ngrok http 9105
'''

##### Webhook GitHub

GitHub → repo → Settings → Webhooks → Add webhook
→ Payload URL : <MAPPING_NGROK>/github-webhook/?token=<TOKEN_GÉNÉRÉ_PAR_JENKINS>
→ Content type : application/json
✓ Just the push event
✓ Active
→ + Add webhook




### PostgreSQL
créer un projet dans Neon
créér une database dans l'interface

### pipeline
rendre pipeline importable comme module

creation pyproject.toml à la racine
$ pip install -e .

