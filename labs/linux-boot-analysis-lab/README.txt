Lab Semaine 1 — Analyse du démarrage d’un système Linux

1. Objectif

Comprendre les étapes du démarrage d’un système Linux :

Firmware (BIOS / UEFI)

Bootloader

Chargement du noyau

Initialisation des services

Session utilisateur

2. Environnement

Plateforme de virtualisation :

VirtualBox

Système installé :

Ubuntu

Configuration :

CPU : 2 vCPU

RAM : 4 GB

Disque : 25 GB

3. Schéma du démarrage
Power
 ↓
Firmware (BIOS / UEFI)
 ↓
Bootloader (GRUB)
 ↓
Kernel Linux
 ↓
systemd
 ↓
Services
 ↓
Session utilisateur


4. Vérification du noyau Linux

Commande utilisée :

uname -r

Résultat observé :

6.5.0-26-generic

Analyse :

Le kernel Linux chargé au démarrage est 6.5.0-26-generic.

📸 Capture recommandée :

screenshots/kernel-version.png

5. Analyse des messages du noyau

Commande utilisée :

dmesg | head

Résultat :

[    0.000000] Linux version 6.5.0-26-generic
[    0.000000] Command line: BOOT_IMAGE=/boot/vmlinuz
[    0.000000] BIOS-provided physical RAM map
[    0.000000] NX (Execute Disable) protection: active

Analyse :

Ces messages montrent :

le chargement du noyau

la détection de la mémoire

l’environnement VirtualBox

📸 Capture :

screenshots/dmesg-output.png

6. Analyse des logs du démarrage

Commande utilisée :

journalctl -b | head

Résultat observé :

Mar 14 10:22:14 ubuntu kernel: Linux version 6.5.0-26-generic
Mar 14 10:22:14 ubuntu kernel: Command line: BOOT_IMAGE=/boot/vmlinuz
Mar 14 10:22:14 ubuntu systemd[1]: Started Journal Service.
Mar 14 10:22:15 ubuntu systemd[1]: Started Network Service.
Mar 14 10:22:15 ubuntu systemd[1]: Reached target Network.

Analyse :

journalctl -b permet de voir :

les événements du démarrage

les services lancés

les éventuelles erreurs

C’est un outil très utile pour analyser un problème de démarrage.

📸 Capture recommandée :

screenshots/journalctl-boot.png

7. Identification du premier processus

Commande :

ps -p 1

Résultat :

PID TTY          TIME CMD
1 ?        00:00:01 systemd

Analyse :

Le processus PID 1 est systemd.

Rôle :

gérer les services

organiser le démarrage du système

📸 Capture :

screenshots/systemd-pid1.png

8. Analyse des services actifs

Commande utilisée :

systemctl list-units --type=service | head

Résultat :

accounts-daemon.service   loaded active running Accounts Service
cron.service              loaded active running Cron Scheduler
dbus.service              loaded active running D-Bus System
networking.service        loaded active running Network Manager
ssh.service               loaded active running SSH Server

Analyse :
Ces services sont lancés automatiquement par systemd.


9. Analyse globale du démarrage

Le processus complet :

Power → alimentation de la machine

Firmware → initialise le matériel

Bootloader → charge le kernel

Kernel → initialise le système

systemd → lance les services

Services → fournissent les fonctionnalités

Session utilisateur → accès au système


10. Ce que j’ai appris

Grâce à ce lab j’ai compris :

comment le kernel est chargé

comment systemd organise le système

comment analyser les logs de démarrage avec journalctl

comment identifier les services actifs


11. Preuves du laboratoire

Captures réalisées :

screenshots/kernel-version.png
screenshots/dmesg-output.png
screenshots/journalctl-boot.png
screenshots/systemd-pid1.png
screenshots/services-list.png


12. Validation

Je peux maintenant expliquer :

Quand j’appuie sur Power :

le firmware initialise le matériel

le bootloader charge le kernel

le kernel initialise les ressources

systemd lance les services

l’utilisateur peut utiliser la machine