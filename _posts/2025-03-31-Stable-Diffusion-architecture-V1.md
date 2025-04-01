---
layout: post
title: "Stable Diffusion architecture V1"
date: 2025-03-31
categories: Architectures
---

This article proviend what we need to understand an architecture which integre diffusion modele to generate image base on textual prompte instruction.
   



## Sommaire

- [Introduction on what does Stable diffusion](#Introduction on what does Stable diffusion)
- [What is  a diffusion model](#What is  a diffusion model)
- [How can we reduce the difmension of the problem without degrade performance](#How can we reduce the difmension of the problem without degrade performance)
- [How can we tell the model what to generate](#How can we tell the model what to generate)
- [Understand the differents paramter of the model (temperature, step ...)](#Understand the differents paramter of the model (temperature, step ...))


## Introduction on what does Stable diffusion

Les modèles de diffusion permttent de générer des données ( des images par exemple) à partir de bruit simple bruit. Ils s'avèrent être très performant et permette de générer des images de grande calité et ont su s'imposer fasse aux GAN qui était alors l'état de l'art dans ce domain. 
Néanmoins pour être réellement util il faudrait que l'on soit capable de pouvoir choisir.
Pour ce faire on va venir insérer un signal dans le bruit qui va permettre d'orienter le modèle à sampler à certains endroit de la distributin modèliser par le modèle.

Voici ci-dessous l'architecture tel que dans le papier original de OpanIA : 

![Schéma architecture](/assets/images/stable_diffusion/schéma_architecture.jpg)


Le schéma peut être à première vu un peu compliquer à avaler mais en réalité on peut découper l'architecture en 3 parties :
- Une modèle qui réduit la taille de l'image pour passer du pixel space au latent space
- Un modèle de conditinnement qui permet d'intégrer des instructions et indications sur ce q ui doit être générer
- Un modèle Unet qui transorme le bruit en une image latente.

## What is  a diffusion model

Les modèles de diffusion sont des modèles composer de 2 mécanisme :
- le forward process : on ajoute progressivement du bruit gaussien à nos données d'origine jusqu'à les transformer en bruit pur.
- le reverse process : on apprend à inverser ce processus, en partant du bruit pour reconstruire des données structurées.


### Forward process

C'est un mécanisme stocastique qui permet de progressivement passer d'une image par exmple à une données complétement bruité à l'aide de bruit gaussien.


### Reverse process


On a un réseaude neuronne, un Unet plus particulièrement qui a pour tache de surprimer le bruit rajouter lors d'une étape de forward


Mettre une image avec une image de plus en plus bruiter puis de plus en pus débruitée.

## How can we reduce the difmension of the problem without degrade performance


Expliquer qu'entrainer un Unet sur des images de grande taille est trop coûteux, les data set doivent être trop gros et en bref l'entrianemnt est alors trop long.
Il faut alors un moyen de réduire la complexité de cette tache sans dégrader les performances : un auto encoder

Explication de l'intérête des auto encoder pour projeter nos données sur un espaces de plus petite dimension => réductions de la taille des données et donc plus facile à traiter 
Mais aussi que cet espaces latent à d'autes propriété car on peut faire du sampling directement dans cette espace beacoup plus facilement
Cet espace permet aussi de répartir le dataset dans l'espace suivant différentes caractéristique apprise par le réseau 

## How can we tell the model what to generate


Expliquer le principe de modèle CLIP pour avoir du texte to image
Expliquer aussi comment faire du image to image

## Understand the differents paramter of the model (temperature, step ...)


Bon là c'est dans le titre c'est plutôt explicite

température
inference step 
cfg_scale
sampler_name
seed
tokenizer
tes rajoutfdfdf