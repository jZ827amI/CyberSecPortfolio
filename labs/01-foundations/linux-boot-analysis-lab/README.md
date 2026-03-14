\# Lab Semaine 1 — Analyse du démarrage d’un système Linux



\## 1. Objectif



Comprendre les étapes du démarrage d’un système Linux :



\- Firmware (BIOS / UEFI)  

\- Bootloader (GRUB)  

\- Chargement du noyau (Kernel)  

\- Initialisation des services (`systemd`)  

\- Ouverture de session utilisateur



\---



\## 2. Environnement



\- \*\*Plateforme de virtualisation\*\* : VirtualBox  

\- \*\*Système installé\*\* : Ubuntu  

\- \*\*Configuration VM\*\* :  

&#x20; - CPU : 2 vCPU  

&#x20; - RAM : 4 GB  

&#x20; - Disque : 25 GB  



\---



\## 3. Étapes réalisées



1\. Création de la VM Ubuntu dans VirtualBox  

2\. Installation du système  

3\. Redémarrage pour observer le processus de boot  

4\. Analyse du démarrage avec plusieurs commandes Linux (`uname`, `dmesg`, `journalctl`, `systemctl`)  



\---



\## 4. Schéma du démarrage



```text

Power

&#x20;↓

Firmware (BIOS / UEFI)

&#x20;↓

Bootloader (GRUB)

&#x20;↓

Kernel Linux

&#x20;↓

systemd

&#x20;↓

Services

&#x20;↓

Session utilisateur

5\. Vérification du noyau Linux



Commande :



uname -r



Signification :



uname → informations système



\-r → version du noyau



Résultat observé :



5.4.0-84-generic



Observation :

Le kernel Linux chargé au démarrage est 5.4.0-84-generic.



📸 Capture recommandée :

screenshots/kernel-version.png



6\. Analyse des messages du noyau



Commande :



dmesg | head



Résultat :



\[    0.000000] Linux version 5.4.0-84-generic

\[    0.000000] Command line: BOOT\_IMAGE=/boot/vmlinuz

\[    0.000000] BIOS-provided physical RAM map

\[    0.000000] NX (Execute Disable) protection: active



Observation :



Le kernel est chargé



La mémoire est détectée



VM VirtualBox identifiée



📸 Capture :

screenshots/dmesg-output.png



7\. Analyse des logs du démarrage



Commande :



journalctl -b | head



Résultat :



Mar 14 10:22:14 ubuntu kernel: Linux version 5.4.0-84-generic

Mar 14 10:22:14 ubuntu systemd\[1]: Started Journal Service.

Mar 14 10:22:15 ubuntu systemd\[1]: Started Network Service.

Mar 14 10:22:15 ubuntu systemd\[1]: Reached target Network.



Observation :



Affiche les événements du démarrage



Montre les services lancés automatiquement



Permet de détecter d’éventuelles erreurs



📸 Capture recommandée :

screenshots/journalctl-boot.png



8\. Identification du premier processus



Commande :



ps -p 1



Résultat :



PID TTY          TIME CMD

1 ?        00:00:01 systemd



Observation :

Le processus PID 1 est systemd.



Rôle :



Démarrer et superviser les services



Organiser le démarrage du système



📸 Capture :

screenshots/systemd-pid1.png



9\. Analyse des services actifs



Commande :



systemctl list-units --type=service | head



Résultat :



accounts-daemon.service   loaded active running Accounts Service

cron.service              loaded active running Cron Scheduler

dbus.service              loaded active running D-Bus System

networking.service        loaded active running Network Manager

ssh.service               loaded active running SSH Server



Observation :

Ces services sont lancés automatiquement par systemd pour fournir les fonctionnalités essentielles du système.



📸 Capture :

screenshots/services-list.png



10\. Analyse globale du démarrage

Étape	Fonction

Power	alimentation et démarrage du CPU

Firmware	initialise le matériel et le BIOS/UEFI

Bootloader	charge le kernel Linux

Kernel	initialise le système et le matériel

systemd	lance les services essentiels

Services	fournissent les fonctionnalités

Session utilisateur	permet l’accès au système

11\. Problèmes possibles



Bootloader corrompu → le kernel ne se charge pas



Kernel corrompu → démarrage impossible



systemd absent ou bloqué → services non lancés



12\. Ce que j’ai appris



Comment le kernel est chargé et initialise le système



Le rôle de systemd et des services



Comment analyser les logs de démarrage avec journalctl



Comment identifier et interpréter les services actifs



13\. Preuves du laboratoire



screenshots/kernel-version.png



screenshots/dmesg-output.png



screenshots/journalctl-boot.png



screenshots/systemd-pid1.png



screenshots/services-list.png



14\. Validation



Je peux maintenant expliquer le cycle complet du démarrage :



Le firmware initialise le matériel



Le bootloader charge le kernel



Le kernel initialise les ressources



systemd lance les services



L’utilisateur peut utiliser la machine





\----------------------------------------------------------------------------------





\# Week 1 Lab — Linux System Boot



\## 1. Goal



Understand the steps of Linux system boot:



\- Firmware (BIOS / UEFI)  

\- Bootloader (GRUB)  

\- Kernel loading  

\- Service start (`systemd`)  

\- User login



\---



\## 2. Environment



\- \*\*Virtual platform:\*\* VirtualBox  

\- \*\*OS installed:\*\* Ubuntu  



\*\*VM settings:\*\*



\- CPU: 2 vCPU  

\- RAM: 4 GB  

\- Disk: 25 GB  



\---



\## 3. Steps Done



1\. Created Ubuntu VM in VirtualBox  

2\. Installed Ubuntu  

3\. Rebooted the VM to see boot process  

4\. Checked boot using commands: `uname`, `dmesg`, `journalctl`, `systemctl`



\---



\## 4. Boot Process Diagram



```text

Power

&#x20;↓

Firmware (BIOS / UEFI)

&#x20;↓

Bootloader (GRUB)

&#x20;↓

Linux Kernel

&#x20;↓

systemd

&#x20;↓

Services

&#x20;↓

User login

5\. Check Linux Kernel



Command:



uname -r



Meaning:



uname → system info



\-r → kernel version



Result:



5.4.0-84-generic



Note:

Kernel loaded is 5.4.0-84-generic



📸 Screenshot: screenshots/kernel-version.png



6\. Check Kernel Messages



Command:



dmesg | head



Result:



\[    0.000000] Linux version 5.4.0-84-generic

\[    0.000000] Command line: BOOT\_IMAGE=/boot/vmlinuz

\[    0.000000] BIOS-provided physical RAM map

\[    0.000000] NX (Execute Disable) protection: active



Note:



Kernel loaded



Memory detected



Running in VirtualBox



📸 Screenshot: screenshots/dmesg-output.png



7\. Check Boot Logs



Command:



journalctl -b | head



Result:



Mar 14 10:22:14 ubuntu kernel: Linux version 5.4.0-84-generic

Mar 14 10:22:14 ubuntu systemd\[1]: Started Journal Service.

Mar 14 10:22:15 ubuntu systemd\[1]: Started Network Service.

Mar 14 10:22:15 ubuntu systemd\[1]: Reached target Network.



Note:



Shows events at boot



Shows services started automatically



Helps find boot problems



📸 Screenshot: screenshots/journalctl-boot.png



8\. First Process



Command:



ps -p 1



Result:



PID TTY          TIME CMD

1 ?        00:00:01 systemd



Note: PID 1 is systemd.



Role of systemd:



Start and manage services



Control system boot



📸 Screenshot: screenshots/systemd-pid1.png



9\. Active Services



Command:



systemctl list-units --type=service | head



Result:



accounts-daemon.service   loaded active running Accounts Service

cron.service              loaded active running Cron Scheduler

dbus.service              loaded active running D-Bus System

networking.service        loaded active running Network Manager

ssh.service               loaded active running SSH Server



Note: These services start automatically with systemd.



📸 Screenshot: screenshots/services-list.png



10\. Boot Steps Summary

Step	Function

Power	Turn on CPU

Firmware	Start hardware and BIOS/UEFI

Bootloader	Load Linux kernel

Kernel	Start system resources and hardware

systemd	Start main services

Services	Provide system functions

User login	Allow access to system

11\. Possible Problems



Bootloader damaged → kernel cannot start



Kernel damaged → system cannot boot



systemd fails → services not started



12\. What I Learned



How kernel loads and starts system



Role of systemd and services



How to check boot logs with journalctl



How to see running services



13\. Lab Evidence



screenshots/kernel-version.png



screenshots/dmesg-output.png



screenshots/journalctl-boot.png



screenshots/systemd-pid1.png



screenshots/services-list.png



14\. Validation



I can now explain the full Linux boot process:



Firmware starts hardware



Bootloader loads kernel



Kernel initializes resources



systemd starts services



User can use the system

