# Stripe, infrastructure de paiement en ligne.

## Plan du cours

### Stripe, c'est quoi ?

#### Se créer un compte sur Stripe

#### Les clés API

#### Installer Stripe PHP (SDK) via Composer

#### Configurer Stripe.js

#### Initier un paiement Stripe via PHP

---

# Stripe, c'est quoi ?

Stripe est une solution de paiement en ligne disponible dans une majorité de pays, est par conséquent très utilisé pour plusieurs de ces services (paiement par carte, abonnement, paiement via lien, ... ).

Autant d'intégration possible pour les développeurs via leur API documentée (https://stripe.com/docs/api) et un ensemble de guides (https://stripe.com/docs) 

Les languages de programmation utilisés actuellement pour intéragir avec Stripe sont : PHP, JS, React, iOS, Android, React Native.


## Se créer un compte sur Stripe

En premier lieu, il est bien entendu nécessaire de se créer un compte sur Stripe (https://stripe.com/) et de remplir les informations demandées, pour pouvoir accéder à l'onglet Développeurs et aux clés API.


## Les clés API

En tant que développeur afin de pouvoir intéragir avec Stripe via votre code source vous allez devoir utiliser les clés d'API mises à votre disposition dans l'onglet ``Developpers`` de votre compte Stripe.

En mode Test les clés sont toujours préfixé de ``pk_test`` ou ``sk_test``. Et en production les clés sont toujours préfixées par ``pk_live`` ou ``sk_live``.


## Installer Stripe PHP via Composer

Composer est un outil de gestion des dépendances : il permet de récupérer/installer des versions précises de biliothèques extérieures à votre projet et tout composant nécessaire à leur bon fonctionnement.

Dans notre cas voici la commande à écrire dans votre terminal à la racine d'un projet pour récupérer la librairie PHP de Stripe

```shell
composer require stripe/stripe-php
```
PHP est un language s'exécutant côté Serveur donc cette librairie permet à votre serveur PHP de communiquer avec Stripe.

## Intégrer Stripe.js sur une page de paiement

Pour pouvoir faire appel à Stripe via Javascript, voici un exemple de balise header sur une page de paiement intégrant Stripe :

```html
<head>
    <title>Checkout</title>
    <script src="https://js.stripe.com/v3/"></script>
</head>
```

Cette librairie va se mettre en action côté Client, lorsque votre utilisateur va consulter la page et permettre de communiquer avec Stripe dans ce contexte. 

## Initier un paiement Stripe via PHP

Dans la version 13.10 de Stripe PHP l'Objet utilisé pour faire appel à Stripe afin de créer un paiement est ``PaymentIntends``. 

Il représente votre intention d’encaisser le paiement d’un client et suit les tentatives de débit et changements d’état tout au long du processus de paiement.

```php
$stripe = new \Stripe\StripeClient("[VOTRE_CLE_TEST]");
    $intent = $stripe->paymentIntents->create(
      [
        'amount' => 4200,
        'currency' => 'eur',
      ]
    );
```

Pour sa définition complète : https://stripe.com/docs/api/payment_intents