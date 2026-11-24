# Job 01 – Documentation sur l'EDR

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
| Détection en temps réel | Recherche d'IOC (indicateurs de compromission) et d'IOA (indicateurs d'attaque), corrélation avec la threat intelligence, mapping sur MITRE ATT&CK |
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
| FortiEDR (Fortinet) | Réponse automatisée par scénarios personnalisables, règles liées à MITRE ATT&CK, intégration à la Fortinet Security Fabric, support Windows, macOS et Linux |
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
- IBM – Qu'est-ce que l'EDR ? : https://www.ibm.com/fr-fr/think/topics/edr
