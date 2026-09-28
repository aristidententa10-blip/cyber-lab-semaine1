# cyber-lab-semaine1
Mise en place d'un laboratoire de virtualisation sous VMware Workstation : déploiement d'Ubuntu Server et d'un poste Windows, configuration réseau et analyse BIOS/UEFI / Secure Boot.
Rapport de Lab - Semaine 1 : Architecture & Virtualisation

Ce rapport documente la mise en place de mon laboratoire de virtualisation professionnel sous VMware Workstation, réalisé dans le cadre de mon parcours en administration système et cybersécurité. L'objectif était d'appliquer une approche 80% pratique / 20% théorie en construisant un réseau local virtuel interconnecté et sécurisé.

🛠️ 1. Architecture du Laboratoire

Pour simuler un environnement d'entreprise réaliste (un serveur et un poste de travail), nous avons déployé deux machines virtuelles (VMs) :

VM 1 : Ubuntu Server (Lab-Linux-01)

VM 2 : Poste Client Windows (Lab-Windows-Poste)

Les deux machines ont été configurées sur le même sous-réseau virtuel VMware, permettant les échanges de paquets.

💻 2. Configuration Matérielle & Choix du Disque

Lors de la création de la machine virtuelle Windows, une attention particulière a été portée sur le dimensionnement du stockage :

Capacité allouée : Ajustée à 40.0 Go (avec une recommandation de 60 Go pour une utilisation à long terme sous Windows).

Format de stockage : Sélection de l'option “Store virtual disk as a single file” pour optimiser les performances des entrées/sorties sur un système hôte en NTFS/exFAT.

🌐 3. Validation de l'Environnement Réseau (Test de Connectivité)

L'étape cruciale de ce lab consistait à valider la communication bidirectionnelle entre le serveur Linux et le poste Windows.

A. Récupération des adresses IP

Ubuntu Server (ens33) : 192.168.16.140

Poste Windows : 192.168.16.141

B. Résolution du Pare-feu et Test de Ping Bidirectionnel

Initialement, le ping émanant d'Ubuntu vers Windows était bloqué à 100% de perte en raison des règles de sécurité par défaut de Windows Defender Firewall. Après l'activation de la règle entrante ICMPv4-In (Requête d'écho) sur le poste Windows, la communication a été établie avec succès (0% de perte de part et d'autre).

🛡️ 4. Théorie & Application : BIOS/UEFI & Secure Boot

La partie théorique de la semaine a porté sur la Root of Trust (racine de confiance) au démarrage de la machine :

BIOS vs UEFI : Passage du micrologiciel traditionnel BIOS au standard moderne UEFI, permettant la gestion des disques de grande capacité (GPT) et un amorçage sécurisé.

Secure Boot : Vérification cryptographique des signatures du chargeur de démarrage avant le lancement de l'OS pour contrer les attaques de type bootkit.

Dans les paramètres avancés de nos VMs VMware, nous avons pu constater et configurer ces différences :

Lab-Linux-01 configuré en mode BIOS traditionnel.

Lab-Windows-Poste configuré en mode UEFI avec Secure Boot activé.

🎯 Conclusion

Ce premier lab m'a permis de maîtriser le déploiement d'un hyperviseur de Type 2 (VMware Workstation), de configurer un réseau virtuel inter-machines, de dépanner des règles de pare-feu réseau et d'appliquer les bonnes pratiques de sécurité matérielle (UEFI/Secure Boot). Environnement prêt pour les prochains modules !
