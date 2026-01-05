# Microcontroleur

Ce dépôt GitHub correspond au **dépôt du code source** du projet de mini-serre intelligente basé sur un microcontrôleur.  
Le système permet de piloter automatiquement ou manuellement une pompe et un ventilateur selon la température et l’humidité mesurées.  
Le dépôt contient l’ensemble du code source nécessaire au fonctionnement du système.

# Introduction

Dans le cadre de ce projet, il a été demandé de concevoir et de mettre en œuvre un système embarqué basé sur un microcontrôleur.  
L’objectif principal est de développer une solution fonctionnelle intégrant à la fois une partie matérielle et une partie logicielle, permettant d’assurer le pilotage et le contrôle de différents composants électroniques.

Ce projet s’appuie sur la réalisation d’un câblage matériel précis reliant le microcontrôleur aux différents périphériques utilisés, tels que les capteurs et les actionneurs.  
Le fonctionnement global du système repose sur un programme embarqué assurant l’initialisation des composants, le traitement des informations et la commande des sorties en fonction des conditions définies.

Afin de garantir la compréhension et la reproductibilité du système, ce document présente une explication détaillée du code source afin de mettre en évidence l’architecture logicielle et le rôle des principales fonctions développées.

L’ensemble de ces éléments permet de justifier les choix techniques effectués et de démontrer le bon fonctionnement du système lors de la démonstration finale.

# Code Source


# main.h — Définition matérielle et interface globale

##  Rôle du fichier

Le fichier `main.h` définit l’interface matérielle globale du projet de mini-serre intelligente.
Il établit le lien entre le câblage électronique réel et le programme embarqué en associant
chaque périphérique (boutons, capteurs, actionneurs) aux broches du microcontrôleur STM32.

Ce fichier agit comme un **contrat matériel** utilisé par l’ensemble des autres modules du projet.

---

##  Protection contre les inclusions multiples

#ifndef __MAIN_H
#define __MAIN_H

Cette protection empêche le fichier d’être inclus plusieurs fois lors de la compilation, ce qui évite les erreurs de redéfinition.
C’est une bonne pratique standard en langage C.

