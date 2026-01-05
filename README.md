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

## Protection contre les inclusions multiples

#ifndef __MAIN_H

#define __MAIN_H


Cette protection empêche le fichier d’être inclus plusieurs fois lors de la compilation, ce qui évite les erreurs de redéfinition.
C’est une bonne pratique standard en langage C.

Accès aux bibliothèques STM32 HAL
#include "stm32g0xx_hal.h"


Cette inclusion permet l’accès à toutes les fonctions de la bibliothèque HAL de STM32, notamment :

la gestion des GPIO

la conversion analogique numérique (ADC)

les timers

la communication série (UART)

la gestion des interruptions

Sans cette bibliothèque, le microcontrôleur ne pourrait pas être piloté.

Gestion globale des erreurs
void Error_Handler(void);


Cette fonction est appelée en cas d’erreur critique (initialisation de l’horloge, mauvaise configuration d’un périphérique, etc.).
Elle permet de placer le système dans un état sûr en bloquant l’exécution.

Définition des boutons utilisateur
#define BTN1_Pin GPIO_PIN_8
#define BTN1_GPIO_Port GPIOB

#define BTN2_Pin GPIO_PIN_8
#define BTN2_GPIO_Port GPIOA

#define BTN3_Pin GPIO_PIN_9
#define BTN3_GPIO_Port GPIOB


Les boutons permettent l’interaction avec l’utilisateur :

BTN1 : changement de mode / accès au mode réglage

BTN2 : commande du ventilateur ou augmentation d’un seuil

BTN3 : commande de la pompe ou diminution d’un seuil

L’utilisation de constantes rend le code plus lisible et plus facile à modifier en cas de changement de câblage.

Définition des capteurs analogiques
#define TEMP_ADC_Pin GPIO_PIN_0
#define HUM_ADC_Pin  GPIO_PIN_1

#define TEMP_ADC_GPIO_Port GPIOA
#define HUM_ADC_GPIO_Port  GPIOA


Deux entrées analogiques sont utilisées :

PA0 : capteur de température

PA1 : capteur d’humidité

Ces signaux sont convertis en valeurs numériques par le module ADC.

Définition du ventilateur
#define FAN_IN1_Pin GPIO_PIN_4
#define FAN_IN2_Pin GPIO_PIN_5

#define FAN_IN1_GPIO_Port GPIOA
#define FAN_IN2_GPIO_Port GPIOA


Le ventilateur est piloté via deux sorties GPIO, ce qui permet :

l’activation

l’arrêt sécurisé

Ce pilotage est utilisé dans le module moteur.c.

Définition de la pompe (PWM + direction)
#define PUMP_PWM_Pin GPIO_PIN_7
#define PUMP_DIR_Pin GPIO_PIN_12

#define PUMP_PWM_GPIO_Port GPIOA
#define PUMP_DIR_GPIO_Port GPIOA


La pompe est contrôlée par :

un signal PWM pour ajuster la puissance

une broche de direction pour définir le sens ou l’activation logique

Le PWM est généré à l’aide du timer TIM14.

Fin du fichier
#endif


Cette directive marque la fin de la protection contre les inclusions multiples.

Résumé fonctionnel

Le fichier main.h centralise toutes les définitions matérielles du projet.
Il permet de séparer clairement le matériel de la logique logicielle, ce qui améliore :

la lisibilité du code

la maintenance

l’évolutivité du système

