# EDR – Libérer le cyberdétective : créer une expérience de laboratoire EDR immersive

## Introduction

Les solutions **EDR** (*Endpoint Detection and Response*) sont des outils de cybersécurité conçus pour **surveiller, détecter et répondre aux menaces** de sécurité sur les terminaux (ordinateurs, serveurs, appareils mobiles, etc.) au sein d'un réseau. Elles jouent un rôle crucial dans la protection des organisations contre les cyberattaques modernes, souvent sophistiquées et persistantes.

Aspects clés d'une solution EDR :

Détection des menaces en temps réel

Surveillance et collecte de données

Réponse rapide aux incidents

Analyse et investigation post-incident

Automatisation et intelligence artificielle

Intégration avec d'autres outils de sécurité

Parmi les solutions EDR les plus connues : CrowdStrike Falcon, Microsoft Defender for Endpoint, Symantec Endpoint Detection and Response et SentinelOne.

## Objectif du projet

Construire un **laboratoire EDR** avec **Wazuh** sur des machines virtuelles Debian, puis s'en servir pour **penser comme un attaquant afin de mieux se défendre** : installer la solution, déployer des agents, configurer et créer des règles de détection, simuler des attaques et automatiser la réponse pour réduire le temps de neutralisation d'une menace.

## Sommaire

| **Job** | **Thème** | **Ce qui est réalisé** | **Documentation** | **Statut** |
| --- | --- | --- | --- | --- |
| **01** | Documentation sur l'EDR | Se documenter sur l'EDR et préparer la documentation pour la soutenance | [JOB01\_documentation\_edr.md](./JOB01_documentation_edr.md) | ✅ |
| **02** | Installation de la solution EDR | Installer une solution EDR compatible Debian : **Wazuh** | [JOB02\_installation\_wazuh\_debian13.md](./JOB02_installation_wazuh_debian13.md) | ✅ |
| **03** | VM Debian, agents et règles de détection | Créer plusieurs VM Debian sans GUI, installer et configurer l'agent Wazuh, configurer les règles de détection (fichiers, processus, connexions réseau) | [JOB03\_vm\_debian\_agents\_wazuh.md](./JOB03_vm_debian_agents_wazuh.md) | ✅ |
| **04** | Simulation d'attaque | Simuler une attaque (Metasploit ou scripts bash), observer la réaction de Wazuh, rédiger un rapport (attaque, détection, mesures de réponse) avec captures des alertes et des logs | [JOB04\_simulation\_attaque.md](./JOB04_simulation_attaque.md) | ⏳ |
| **05** | Règles de détection personnalisées | Choisir une technique d'attaque non couverte par les règles par défaut, développer des règles personnalisées (agent et serveur), les tester, documenter | [JOB05\_regles\_personnalisees.md](./JOB05_regles_personnalisees.md) | ⏳ |
| **06** | Réponse automatisée | Configurer une « réponse active » (suppression d'un fichier suspect, arrêt d'un processus malveillant), la déclencher, documenter la logique et son intérêt pour un SOC | [JOB06\_reponse\_active.md](./JOB06_reponse_active.md) | ⏳ |
| **Bonus** | Pour aller plus loin | Intégrer Wazuh à un SIEM (Elastic Stack) pour une analyse avancée des journaux et des alertes | [BONUS\_integration\_elastic.md](./BONUS_integration_elastic.md) | ⏳ |

✅ réalisé · ⏳ à venir

## Détail des jobs

### Job 01 – Documentation sur l'EDR

Recherche documentaire sur les EDR : définition, architecture, fonctionnalités, différences avec EPP / XDR / MDR, limites et solutions du marché.

### Job 02 – Installation de Wazuh

Mise en place du serveur Wazuh : indexer, manager et dashboard.

### Job 03 – VM Debian, agents et règles de détection

Création de plusieurs VM Debian sans interface graphique, installation de l'agent Wazuh, puis configuration de la surveillance des **fichiers**, des **processus** et des **connexions réseau**.

### Job 04 – Simulation d'attaque

Attaque simulée pour observer la réaction de Wazuh. Le rapport documente l'attaque, les actions de détection et les mesures de réponse, avec captures d'écran des alertes et des logs.

### Job 05 – Règles de détection personnalisées

Au-delà des règles par défaut : choix d'une technique d'attaque, création des règles (fichiers de configuration de l'agent et du serveur), test par simulation, puis documentation (technique, code ou configuration des règles, captures des alertes).

### Job 06 – Réponse automatisée

Un EDR ne fait pas que détecter, il permet aussi d'agir. Une alerte des jobs 04 ou 05 déclenche une réponse active sur la machine concernée, avec explication de la logique mise en place et de son importance pour un SOC.

### Pour aller plus loin

Intégration de Wazuh avec Elastic Stack (SIEM).

## Compétences visées

Administrer et sécuriser les infrastructures systèmes

Participer à la mesure et à l'analyse du niveau de sécurité de l'infrastructure

Mettre en œuvre et optimiser la supervision des infrastructures

## Rendu

Évaluation sous forme de **présentation en soutenance** avec support, devant l'équipe pédagogique.

## Environnement du laboratoire

| **Élément** | **Détail** |
| --- | --- |
| EDR | Wazuh 4.14 |
| Serveur | Indexer + manager + dashboard (installation tout-en-un) |
| Agents | VM Debian 13 sans interface graphique |
| Réseau | VM sur le même sous-réseau (réseau pont) |

## Base de connaissances

[Implémenter un EDR en entreprise – Lockself](https://www.lockself.com/blog/implementer-edr-entreprise-guide)

[Qu'est-ce que l'EDR ? – Trend Micro](https://www.trendmicro.com/fr_fr/what-is/xdr/edr.html)

[FortiEDR – Fortinet](https://www.fortinet.com/fr/products/endpoint-security/fortiedr)

[EDR-as-a-Service – Advens](https://www.advens.com/media/securite-operationnelle/edr-informatique/)

[Qu'est-ce que l'EDR ? – IBM](https://www.ibm.com/fr-fr/think/topics/edr)

Job 01 – Documentation sur l'EDR

Projet « Libérer le cyberdétective » – La Plateforme · Novembre 2026

## 1. Qu'est-ce qu'un EDR ?

Un EDR (Endpoint Detection and Response) est une solution de cybersécurité qui surveille en continu les terminaux d'un réseau (postes, serveurs, mobiles, objets connectés), détecte les comportements suspects et permet de réagir rapidement. Contrairement à un antivirus classique, qui repose surtout sur des signatures de menaces connues, l'EDR analyse l'activité en temps réel et sait repérer des attaques inconnues ou « sans fichier » qui s'exécutent uniquement en mémoire (IBM, Trend Micro). Le terme a été reconnu pour la première fois par Gartner en 2013 (IBM).

## 2. Pourquoi c'est important

- Les terminaux sont le point d'entrée de la majorité des attaques : selon certaines études citées par IBM, jusqu'à 90 % des cyberattaques et 70 % des violations de données réussies partent d'un terminal.
- Les outils traditionnels ne voient pas les menaces avancées qui restent cachées des semaines ou des mois dans un réseau avant de déclencher un ransomware ou un exploit zero-day.
- L'EDR donne aux équipes du SOC une visibilité continue (24h/24) et accélère le temps de détection et de réponse (Trend Micro).

## 3. Architecture d'un EDR

D'après Lockself, un EDR repose sur trois composants :

1. **Les agents**, installés sur chaque terminal, qui collectent en continu la télémétrie et les logs système.
2. **Le serveur central** (cloud ou data center de l'entreprise), qui stocke et analyse les données avec de l'analyse heuristique et du machine learning.
3. **La console d'administration**, où les analystes consultent les alertes, investiguent les incidents et déclenchent des réponses (isolement d'un poste, suppression d'un fichier malveillant…).

## 4. Fonctionnalités principales

IBM distingue cinq grandes fonctions, que l'on retrouve chez les autres éditeurs :

| Fonction | Ce que ça couvre |
| --- | --- |
| Collecte continue | Processus, connexions réseau, modifications de configuration ou de registre, transferts de fichiers, comportements des utilisateurs |
| Détection en temps réel | Recherche d'IOC (indicateurs de compromission) et d'IOA (indicateurs d'attaque), corrélation avec la threat intelligence, mapping sur MITRE ATT\&CK |
| Réponse automatisée | Alerte, priorisation, isolement du terminal, arrêt d'un processus, blocage d'un fichier suspect |
| Investigation et remédiation | Analyse forensique pour trouver la cause racine, suppression des fichiers malveillants, restauration, mise à jour des règles de détection |
| Aide à la chasse aux menaces | Recherches ad hoc et requêtes sur les données collectées |

## 5. EDR, EPP, XDR et MDR

- **EPP** (Endpoint Protection Platform) : vise surtout la **prévention** des menaces connues (antivirus, pare-feu…). L'EDR se concentre sur la **détection et la réponse** à ce qui a déjà franchi la prévention. Les deux sont complémentaires (Lockself, IBM).
- **XDR** (Extended Detection and Response) : étend le principe à toute la surface d'attaque (réseau, e-mails, cloud, applications) en croisant les données de plusieurs sources (Trend Micro, Lockself).
- **MDR** (Managed Detection and Response) : service externalisé où des analystes surveillent et répondent à votre place, utile sans SOC interne (Trend Micro, IBM).

## 6. Intégration avec d'autres outils

L'EDR gagne en efficacité lorsqu'il est couplé à un **SIEM** (centralisation des logs, corrélation, workflows automatisés comme la mise en quarantaine d'un hôte), à un **pare-feu** (blocage des IOC détectés) ou à un outil de gestion des vulnérabilités (Lockself). Il peut aussi s'intégrer à un **SOAR** et à des flux de threat intelligence (Trend Micro). C'est exactement la logique de la partie « Pour aller plus loin » du sujet (Wazuh + Elastic Stack).

## 7. Déployer un EDR : les grandes étapes

Lockself résume le déploiement en quatre temps : installer et configurer les serveurs EDR, déployer les agents sur les terminaux, configurer les politiques et règles (collecte, détection, réponse), puis intégrer l'EDR au reste de l'écosystème de sécurité. Les bonnes pratiques : définir des politiques claires, paramétrer des alertes pertinentes, personnaliser les règles de remédiation et maintenir à jour l'EDR et ses bases.

## 8. Limites et points de vigilance

- **Faux positifs et fatigue d'alertes** : Advens a mesuré à l'installation des taux de faux positifs très variables (de l'ordre de 20 % à 90 %), qui peuvent descendre sous 4 % après une phase de paramétrage (exclusions sur les applications métiers, apprentissage du contexte).
- **La remédiation n'est pas magique** : Advens recommande de ne pas tout automatiser. Une décision humaine reste nécessaire sur les actifs critiques, vu les impacts possibles.
- **Impact sur les performances** : surveillance temps réel et collecte de logs consomment CPU et mémoire (Lockself). Fortinet met en avant, pour FortiEDR, un agent léger sans redémarrage et un mode simulation avant le mode protection.
- **Compétences nécessaires** : l'outil se rapproche d'un « SIEM pour endpoints » et demande des analystes formés, d'où l'offre d'EDR managé (EDR-as-a-Service).

## 9. Exemples de solutions du marché

| Solution | Particularité citée dans les sources |
| --- | --- |
| FortiEDR (Fortinet) | Réponse automatisée par scénarios personnalisables, règles liées à MITRE ATT\&CK, intégration à la Fortinet Security Fabric, support Windows, macOS et Linux |
| SentinelOne | Déploiement très rapide, restauration de fichiers, configuration très fine (Advens) |
| Microsoft Defender for Endpoint | Pertinent dans les environnements récents, forte dimension cloud Azure (Advens) |
| Cybereason | Interface pensée contre la cyber-fatigue (Advens) |
| Harfang Lab | EDR souverain français certifié ANSSI (Advens) |

## 10. Lien avec le projet Wazuh

Le laboratoire reprend cette architecture : un serveur Wazuh central, des agents sur les VM Debian sans interface graphique, et une console pour consulter les alertes. Les Jobs 03 à 06 illustrent les fonctions vues plus haut : surveillance des fichiers, processus et connexions réseau (collecte), règles de détection personnalisées (détection), réponse active (réponse automatisée) et intégration à Elastic Stack (SIEM).

## Sources

- Lockself – Implémenter un EDR en entreprise : https://www.lockself.com/blog/implementer-edr-entreprise-guide
- Trend Micro – Qu'est-ce que l'EDR ? : https://www.trendmicro.com/fr\_fr/what-is/xdr/edr.html
- Fortinet – FortiEDR : https://www.fortinet.com/fr/products/endpoint-security/fortiedr
- Advens – L'EDR-as-a-Service : https://www.advens.com/media/securite-operationnelle/edr-informatique/
- IBM – Qu'est-ce que l'EDR ? : [https://www.ibm.com/fr-fr/think/topics/edr](https://www.ibm.com/fr-fr/think/topics/edr)

# Job 02 – Installation de Wazuh (EDR) sur Debian 13

## Sommaire

[Objectif](#1-objectif)

[Architecture du laboratoire](#2-architecture-du-laboratoire)

[Prérequis](#3-prérequis)

[Préparation du système](#4-préparation-du-système)

[Installation de Wazuh](#5-installation-de-wazuh)

[Vérification](#6-vérification)

[Accès à l'interface web](#7-accès-à-linterface-web)

[Sécuriser après installation](#8-sécuriser-après-installation)

[Dépannage](#9-dépannage)

[Sources](#11-sources)

---

## 1. Objectif

Installer une solution EDR compatible Debian : **Wazuh**. Cette étape déploie les composants centraux de Wazuh sur une machine virtuelle. Les agents seront installés sur d'autres VM Debian lors du Job 03.

## 2. Architecture du laboratoire

Wazuh se compose de trois composants centraux, installés ici sur le **même hôte** (installation « tout-en-un ») :

| **Composant** | **Rôle** |
| --- | --- |
| **Wazuh indexer** | Stocke et indexe les alertes et événements |
| **Wazuh server (manager)** | Reçoit les données des agents, applique les règles de détection |
| **Wazuh dashboard** | Interface web de visualisation et d'investigation |

Les terminaux surveillés exécutent un **agent Wazuh** (Job 03).

## 3. Prérequis

### Matériel de la VM

La documentation officielle recommande, pour un déploiement de 1 à 25 agents : **4 vCPU, 8 Go de RAM et 50 Go de stockage**.

Vérification :

```
free -h && nproc && df -h /
```

### Système d'exploitation

⚠️ **Debian ne figure pas dans la liste des systèmes recommandés** par Wazuh pour les composants centraux (RHEL, CentOS Stream, Ubuntu 16.04 à 24.04, etc.). L'installateur affiche d'ailleurs un avertissement sur Debian. L'installation peut fonctionner, mais elle n'est pas officiellement garantie. Voir le [plan B](#10-plan-b--serveur-sur-ubuntu-server-2404-lts).

Debian reste pleinement adapté pour les **agents**.

### Réseau

Une adresse IP fixe ou stable pour la VM (`hostname -I`).

Si la VM est en NAT, la passer en **réseau pont (bridge)** ou rediriger le port 443.

Ports utilisés : **443** (dashboard) et **1514 / 1515** (communication avec les agents).

## 4. Préparation du système

Mise à jour et installation des dépendances :

```
sudo apt update && sudo apt full-upgrade -y
sudo apt install -y curl tar gnupg apt-transport-https libcap2-bin debhelper
sudo reboot
```

Après le redémarrage, noter l'adresse IP de la VM :

```
hostname -I
```

Vérifier qu'aucune installation précédente ne traîne (le résultat doit être vide) :

```
dpkg -l | grep -i -E "wazuh|filebeat"
```

## 5. Installation de Wazuh

Téléchargement et exécution de l'assistant d'installation :

```
curl -sO https://packages.wazuh.com/4.14/wazuh-install.sh
sudo bash ./wazuh-install.sh -a -o -v
```

| **Option** | **Rôle** |
| --- | --- |
| `-a` | Installation tout-en-un (indexer + server + dashboard) |
| `-o` | Écrase une installation existante |
| `-v` | Affiche la sortie complète |

L'installation dure environ 5 à 10 minutes. **Ne pas fermer le terminal.**

À la fin, l'assistant affiche l'utilisateur `admin` et son mot de passe. Les noter. Ils sont aussi récupérables avec :

```
sudo tar -O -xvf wazuh-install-files.tar wazuh-install-files/wazuh-passwords.txt
```

## 6. Vérification

```
sudo systemctl status wazuh-indexer wazuh-manager filebeat wazuh-dashboard --no-pager
```

Les quatre services doivent être **`active (running)`**.

## 7. Accès à l'interface web

Depuis un navigateur : [`https://IP_DE_LA_VM`](https://IP_DE_LA_VM)`:443`

Utilisateur : `admin`

Mot de passe : celui affiché à la fin de l'installation

Au premier accès, le navigateur signale un certificat non émis par une autorité de confiance. C'est normal (certificat auto-signé généré par l'assistant) : il suffit de l'accepter.

## 8. Sécuriser après installation

La documentation Wazuh recommande de **désactiver le dépôt** après installation pour éviter une mise à jour accidentelle qui casserait l'environnement. Sur Debian :

```
sudo sed -i "s/^deb /#deb /" /etc/apt/sources.list.d/wazuh.list
```

## 9. Dépannage

### L'installation du dashboard échoue

L'assistant désinstalle automatiquement tout en cas d'erreur. Avant de relancer, conserver une copie du journal :

```
sudo cp /var/log/wazuh-install.log ~/wazuh-install-echec.log
sudo grep -n -E "ERROR|WARNING" /var/log/wazuh-install.log
sudo tail -n 60 /var/log/wazuh-install.log
```

Causes à vérifier en priorité :

**RAM / CPU insuffisants** : voir le [point 3](#3-prérequis).

**Dépendances manquantes** : réinstaller celles du [point 4](#4-préparation-du-système).

**Téléchargement interrompu** (réseau instable) : relancer l'installation.

**OS non supporté** : tenter le [plan B](#10-plan-b--serveur-sur-ubuntu-server-2404-lts).

### Désinstaller Wazuh

```
sudo bash ./wazuh-install.sh -u
```

## 10. Sources

[Wazuh – Quickstart (installation guide)](https://documentation.wazuh.com/current/quickstart.html)

[Wazuh – Dashboard troubleshooting](https://documentation.wazuh.com/current/user-manual/wazuh-dashboard/troubleshooting.html)

# Job 03 – VM Debian, agents Wazuh et règles de détection

Projet : *Libérer le cyberdétective : créer une expérience de laboratoire EDR immersive* Prérequis : serveur Wazuh opérationnel (voir [Job 02](./JOB02_installation_wazuh_debian13.md)) Agents : plusieurs VM **Debian 13 sans interface graphique**

## Sommaire

[Objectif](#1-objectif)

[Architecture du laboratoire](#2-architecture-du-laboratoire)

[Informations à préparer](#3-informations-à-préparer)

[Création des VM Debian](#4-création-des-vm-debian)

[Installation de l'agent Wazuh](#5-installation-de-lagent-wazuh)

[Vérification de l'enrôlement](#6-vérification-de-lenrôlement)

[Détection des fichiers (FIM)](#7-détection-des-fichiers-fim)

[Détection des processus](#8-détection-des-processus)

[Détection des connexions réseau](#9-détection-des-connexions-réseau)

[Règles de détection côté serveur](#10-règles-de-détection-côté-serveur)

[Tests et résultats](#11-tests-et-résultats)

[Dépannage](#12-dépannage)

[Sources](#13-sources)

---

## 1. Objectif

Créer plusieurs machines virtuelles Debian **sans interface graphique**.

Installer et configurer l'**agent Wazuh** sur chacune pour les enrôler auprès du serveur.

Configurer la surveillance des **fichiers**, des **processus** et des **connexions réseau**, et écrire les règles qui génèrent les alertes correspondantes.

## 2. Architecture du laboratoire

```
                 ┌──────────────────────────────┐
                 │   Serveur Wazuh (Job 02)     │
                 │ indexer + manager + dashboard│
                 │        IP : <IP_MANAGER>     │
                 └──────────────▲───────────────┘
                                │ 1514/tcp (événements)
                                │ 1515/tcp (enrôlement)
              ┌─────────────────┴─────────────────┐
              │                                   │
     ┌────────┴────────┐                 ┌────────┴────────┐
     │     agent1      │                 │     agent2      │
     │  agent Wazuh    │                 │  agent Wazuh    │
     └─────────────────┘                 └─────────────────┘
```

| **Machine** | **Nom d'agent** | **Rôle** |
| --- | --- | --- |
| Serveur | – | Wazuh indexer, manager, dashboard |
| VM 1 | `agent1` | Terminal surveillé (cible) |
| VM 2 | `agent2` | Terminal surveillé (peut servir d'attaquant au Job 04) |

## 3. Informations à préparer

Sur le **serveur Wazuh**, relever :

```
hostname -I                                   # IP du serveur
sudo /var/ossec/bin/wazuh-control info        # version exacte de Wazuh
```

⚠️ La compatibilité agent / serveur n'est garantie que si la version du **serveur est supérieure ou égale** à celle de l'agent. On installera donc l'agent **dans la même version que le serveur** (exemple dans ce document : `4.14.10`, à adapter).

| **Variable** | **Valeur** |
| --- | --- |
| `<IP_MANAGER>` | IP du serveur Wazuh |
| `<VERSION>` | Version du serveur, par exemple `4.14.10` |

## 4. Création des VM Debian

### 4.1 Paramètres recommandés par VM

| **Ressource** | **Valeur** |
| --- | --- |
| CPU | 1 vCPU |
| RAM | 1 Go |
| Disque | 10 Go |
| Réseau | **Pont (bridge)**, même sous-réseau que le serveur Wazuh |

### 4.2 Installation de Debian 13 sans GUI

Démarrer sur l'ISO **Debian 13 netinst**.

Choisir *Install* (mode texte, pas *Graphical install*).

À l'étape **Sélection des logiciels**, **décocher** « environnement de bureau Debian » et « GNOME », puis **cocher** :

**Serveur SSH**

**Utilitaires usuels du système**

Terminer l'installation et redémarrer.

Remarque : si un mot de passe `root` est défini à l'installation, le paquet `sudo` n'est pas installé. Dans ce cas : `su -` puis `apt install -y sudo && usermod -aG sudo <utilisateur>`, puis se reconnecter.

### 4.3 Préparer la VM de base

```
sudo apt update && sudo apt full-upgrade -y
sudo apt install -y curl gnupg apt-transport-https netcat-openbsd
```

### 4.4 Cloner pour obtenir plusieurs VM

Si les VM sont créées par **clonage** d'une VM de base, le faire **avant** d'installer l'agent Wazuh, puis sur chaque clone :

```
# Nom de machine unique
sudo hostnamectl set-hostname agent2

# Identifiant machine unique
sudo rm -f /etc/machine-id /var/lib/dbus/machine-id
sudo systemd-machine-id-setup

# Clés SSH uniques
sudo rm -f /etc/ssh/ssh_host_*
sudo dpkg-reconfigure openssh-server

sudo reboot
```

Vérifier que chaque VM a une **IP différente** (`hostname -I`) et peut joindre le serveur :

```
ping -c 2 <IP_MANAGER>
timeout 3 bash -c '</dev/tcp/<IP_MANAGER>/1514' && echo "1514 OK"
timeout 3 bash -c '</dev/tcp/<IP_MANAGER>/1515' && echo "1515 OK"
```

## 5. Installation de l'agent Wazuh

À faire sur **chaque VM**, en adaptant `WAZUH_AGENT_NAME`.

```
sudo -i
```

**1. Ajouter la clé GPG et le dépôt Wazuh**

```
curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | gpg --no-default-keyring --keyring gnupg-ring:/usr/share/keyrings/wazuh.gpg --import && chmod 644 /usr/share/keyrings/wazuh.gpg
echo "deb [signed-by=/usr/share/keyrings/wazuh.gpg] https://packages.wazuh.com/4.x/apt/ stable main" | tee /etc/apt/sources.list.d/wazuh.list
apt-get update
```

**2. Installer l'agent (version identique au serveur) et l'enrôler**

```
WAZUH_MANAGER="<IP_MANAGER>" WAZUH_AGENT_NAME="agent1" apt-get install -y wazuh-agent=<VERSION>-1
```

Les variables `WAZUH_MANAGER` et `WAZUH_AGENT_NAME` renseignent l'adresse du serveur et le nom de l'agent dans sa configuration.

**3. Démarrer l'agent**

```
systemctl daemon-reload
systemctl enable --now wazuh-agent
```

**4. Empêcher les mises à jour accidentelles**

```
echo "wazuh-agent hold" | dpkg --set-selections
exit
```

## 6. Vérification de l'enrôlement

**Sur l'agent :**

```
sudo systemctl status wazuh-agent --no-pager
sudo tail -n 30 /var/ossec/logs/ossec.log
```

Le service doit être `active (running)` et le journal doit indiquer la connexion au serveur.

**Sur le serveur :**

```
sudo /var/ossec/bin/agent_control -l
```

Les agents doivent apparaître avec le statut **Active**. Ils sont aussi visibles dans l'interface web, section **Agents**.

## 7. Détection des fichiers (FIM)

Le module **syscheck** (File Integrity Monitoring) de l'agent surveille les modifications de fichiers. Par défaut, il analyse des répertoires système (par exemple `/etc`, `/usr/bin`, `/usr/sbin`) lors de **scans périodiques** (toutes les 12 heures par défaut). Pour une détection immédiate dans le laboratoire, on ajoute un répertoire en **temps réel**.

### 7.1 Créer le répertoire surveillé

Le répertoire doit exister **avant** le redémarrage de l'agent :

```
sudo mkdir -p /srv/fim-test
```

### 7.2 Configurer syscheck

```
sudo nano /var/ossec/etc/ossec.conf
```

Dans le bloc `<syscheck>` existant, ajouter la ligne suivante, sans supprimer le reste :

```
<syscheck>
  <!-- ... configuration par défaut ... -->

  <!-- Surveillance en temps réel du répertoire de test -->
  <directories check_all="yes" realtime="yes" report_changes="yes">/srv/fim-test</directories>
</syscheck>
```

| **Attribut** | **Rôle** |
| --- | --- |
| `check_all="yes"` | Vérifie taille, permissions, propriétaire, date, inode et empreintes (MD5, SHA1, SHA256) |
| `realtime="yes"` | Détection immédiate des changements |
| `report_changes="yes"` | Enregistre le contenu modifié des fichiers texte (à utiliser avec précaution : les fichiers surveillés sont copiés) |

Appliquer :

```
sudo systemctl restart wazuh-agent
sudo tail -n 20 /var/ossec/logs/ossec.log
```

Aucune erreur de configuration ne doit apparaître dans le journal.

### 7.3 Option : savoir qui a modifié le fichier (who-data)

L'attribut `whodata="yes"` remplace `realtime="yes"` et ajoute l'utilisateur et le processus à l'origine du changement. Il s'appuie sur le sous-système **auditd**.

```
sudo apt install -y auditd
sudo auditctl -l | grep -- "-a never,task"
```

Si la seconde commande affiche une règle `-a never,task`, la supprimer de `/etc/audit/rules.d/audit.rules`, puis :

```
sudo systemctl restart auditd
```

Remplacer ensuite `realtime="yes"` par `whodata="yes"` dans la ligne `/srv/fim-test`, puis :

```
sudo systemctl restart wazuh-agent
sudo auditctl -l | grep wazuh_fim
```

La règle d'audit sur `/srv/fim-test` doit apparaître.

## 8. Détection des processus

Le module de **surveillance de commandes** (`localfile`) exécute périodiquement une commande et envoie sa sortie au serveur. Ici : la liste des processus actifs, dédoublonnée (utilisateur + nom du processus). Le serveur compare chaque sortie à la précédente (`check_diff`, voir section 10) et alerte si un processus apparaît ou disparaît.

Dans `/var/ossec/etc/ossec.conf`, ajouter **à l'intérieur de** **`<ossec_config>`**, au même niveau que les autres blocs `<localfile>` :

```
<localfile>
  <log_format>full_command</log_format>
  <command>ps -eo user,comm --no-headers | sort -u</command>
  <alias>process list</alias>
  <frequency>60</frequency>
</localfile>
```

| **Balise** | **Rôle** |
| --- | --- |
| `full_command` | Envoie la sortie complète de la commande comme un seul événement |
| `alias` | Nom utilisé dans le message, repris par la règle |
| `frequency` | Intervalle d'exécution en secondes |

Note : cette surveillance peut être bruyante (tâches planifiées, processus éphémères). Pour un usage réel, on filtrerait la commande ou on ajusterait la règle.

## 9. Détection des connexions réseau

Deux commandes sont ajoutées : les **ports en écoute** et les **connexions établies** (adresses distantes uniquement, pour éviter le bruit lié aux ports éphémères). On utilise `ss`, présent par défaut sur Debian, contrairement à `netstat`.

```
<localfile>
  <log_format>full_command</log_format>
  <command>ss -H -tuln | awk '{print $1, $5}' | sort -u</command>
  <alias>listening ports</alias>
  <frequency>60</frequency>
</localfile>

<localfile>
  <log_format>full_command</log_format>
  <command>ss -H -tn state established | awk '{print $4}' | sed 's/:[0-9]*$//' | sort -u</command>
  <alias>established connections</alias>
  <frequency>60</frequency>
</localfile>
```

Tester les commandes à la main avant de redémarrer l'agent :

```
ps -eo user,comm --no-headers | sort -u | head
ss -H -tuln | awk '{print $1, $5}' | sort -u
ss -H -tn state established | awk '{print $4}' | sed 's/:[0-9]*$//' | sort -u
```

Puis redémarrer l'agent et contrôler le journal :

```
sudo systemctl restart wazuh-agent
sudo tail -n 20 /var/ossec/logs/ossec.log
```

Le fichier `ossec.conf` par défaut peut déjà contenir un bloc de surveillance des ports en écoute (alias `netstat listening ports`) associé à la règle Wazuh 533. Les deux peuvent alerter en parallèle : c'est sans conséquence.

## 10. Règles de détection côté serveur

Les sorties de commandes arrivent au serveur sous la forme `ossec: output: '<alias>': ...` et sont d'abord traitées par la règle native **530**. Les règles personnalisées s'appuient sur elle (`if_sid`). L'option `check_diff` ne déclenche l'alerte que si la sortie **a changé** depuis la dernière exécution.

Sur le **serveur Wazuh** :

```
sudo nano /var/ossec/etc/rules/local_rules.xml
```

Ajouter à la fin du fichier (les identifiants 100000 et plus sont réservés aux règles personnalisées) :

```
<group name="local,edr_lab,">

  <rule id="100100" level="7">
    <if_sid>530</if_sid>
    <match>ossec: output: 'process list'</match>
    <check_diff />
    <description>EDR-LAB : liste des processus modifiée (processus apparu ou disparu).</description>
    <group>process_monitor,</group>
  </rule>

  <rule id="100110" level="7">
    <if_sid>530</if_sid>
    <match>ossec: output: 'listening ports'</match>
    <check_diff />
    <description>EDR-LAB : ports en écoute modifiés (port ouvert ou fermé).</description>
    <group>network_monitor,</group>
  </rule>

  <rule id="100120" level="7">
    <if_sid>530</if_sid>
    <match>ossec: output: 'established connections'</match>
    <check_diff />
    <description>EDR-LAB : connexions réseau établies modifiées (nouvelle destination ou fermeture).</description>
    <group>network_monitor,</group>
  </rule>

</group>
```

Redémarrer le serveur pour charger les règles :

```
sudo systemctl restart wazuh-manager
sudo systemctl status wazuh-manager --no-pager
```

Si le service ne redémarre pas, il y a une erreur de syntaxe XML : consulter `sudo tail -n 30 /var/ossec/logs/ossec.log`.

### Récapitulatif des détections

| **Surveillance** | **Mécanisme** | **Règle(s)** | **Niveau** |
| --- | --- | --- | --- |
| Fichiers | syscheck (FIM) | 554 (fichier ajouté), 550 (modifié), 553 (supprimé) | 5 à 7 |
| Processus | `localfile` + règle perso | 100100 | 7 |
| Ports en écoute | `localfile` + règle perso | 100110 (et 533 native si présente) | 7 |
| Connexions établies | `localfile` + règle perso | 100120 | 7 |

## 11. Tests et résultats

Les alertes de type commande apparaissent après le prochain cycle (60 s au maximum). La première exécution d'une commande sert de référence de comparaison : lancer les tests après quelques minutes.

### 11.1 Fichiers (sur `agent1`)

```
echo "version 1" | sudo tee /srv/fim-test/secret.txt
echo "version 2" | sudo tee -a /srv/fim-test/secret.txt
sudo rm /srv/fim-test/secret.txt
```

Alertes attendues : fichier ajouté, somme de contrôle modifiée, fichier supprimé.

### 11.2 Processus (sur `agent1`)

```
sleep 600 &
```

Alerte attendue : règle `100100` (apparition d'un processus `sleep`). Elle se déclenche aussi à sa disparition.

### 11.3 Ports et connexions (entre les deux VM)

Sur `agent2` :

```
nc -l 4444
```

Sur `agent1` (laisser la connexion ouverte) :

```
nc <IP_DEBIAN_VM2> 4444
```

Alertes attendues :

`agent2` : règle `100110` (nouveau port en écoute 4444) et `100120` (nouvelle connexion établie)

`agent1` : règle `100120` (nouvelle destination)

### 11.4 Consulter les alertes

Dans le dashboard : **Threat Hunting** (ou **File Integrity Monitoring** pour le FIM), puis filtrer par exemple :

```
rule.id:(100100 OR 100110 OR 100120)
rule.id:(550 OR 553 OR 554)
```

Sur le serveur, en ligne de commande :

```
sudo grep -E '"id":"(100100|100110|100120)"' /var/ossec/logs/alerts/alerts.json | tail -n 3
```

### 11.5 Tester une règle sans attendre

Sur le serveur, l'outil `wazuh-logtest` permet de vérifier une règle en lui soumettant un événement :

```
sudo /var/ossec/bin/wazuh-logtest
```

## 12. Dépannage

| **Symptôme** | **Cause probable** | **Action** |
| --- | --- | --- |
| Agent « Never connected » | Serveur injoignable ou ports fermés | Tester `1514` et `1515` depuis la VM (section 4.4), vérifier `WAZUH_MANAGER` dans `/var/ossec/etc/ossec.conf` |
| Agent « Disconnected » | Service arrêté ou réseau coupé | `systemctl status wazuh-agent`, `tail /var/ossec/logs/ossec.log` |
| Nom d'agent déjà utilisé | Deux VM avec le même nom, ou clone | Renommer la VM et `WAZUH_AGENT_NAME`, supprimer l'ancien agent depuis le dashboard |
| Incompatibilité de version | Agent plus récent que le serveur | Réinstaller l'agent à la version du serveur |
| L'agent ne redémarre plus | Erreur XML dans `ossec.conf` | Lire `/var/ossec/logs/ossec.log`, corriger la balise indiquée |
| Pas d'alerte FIM en temps réel | Répertoire inexistant au démarrage | Créer `/srv/fim-test` puis redémarrer l'agent |
| Pas d'alerte sur processus ou réseau | Règle non chargée ou attente du cycle | Vérifier `local_rules.xml`, redémarrer `wazuh-manager`, attendre 60 s |
| Manager qui ne redémarre pas | Erreur XML dans `local_rules.xml` | Lire `/var/ossec/logs/ossec.log` sur le serveur |

## 13. Sources

[Wazuh – Déploiement de l'agent sur Linux](https://documentation.wazuh.com/current/installation-guide/wazuh-agent/wazuh-agent-package-linux.html)

[Wazuh – Configuration du File Integrity Monitoring](https://documentation.wazuh.com/current/user-manual/capabilities/file-integrity/index.html)

[Wazuh – Surveillance de commandes](https://documentation.wazuh.com/current/user-manual/capabilities/command-monitoring/index.html)
