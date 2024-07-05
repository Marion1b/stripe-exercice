# Exercice Donate For Ducks

## Le but
L'objectif de cet exercice est de mettre en place une page de donations utilisant la solution Stripe pour contribuer à l'amélioration des conditions de vie des canards de debug. 

Les paiements seront effectués via l'environnement de test fourni par Stripe, ce qui permettra de simuler les paiements sans avoir à dépenser du "vrai" argent.

## Étape 0

- Créez un repository public avec un README sur GitHub, appelez-le `bre02-php-donate-for-ducks`
- Clonez le dans le dossier `sites/php` de votre IDE.

## Étape 0 - bis

Créez un compte sur www.stripe.com avec votre adresse e-mail 3WA

## Étape 1 - Récupération des sources du projet

Importez le code source d'une implémentation (non-fonctionnelle) d'un tunnel de paiement personnalisé Stripe qui est mise à votre disposition sur Discord. 

Ajoutez ces sources à votre projet sur l'IDE et familiarisez-vous avec son architecture de dossiers.

## Étape 2 - Création du .env

Dans le dossier `./config`, ajoutez un fichier `.env` contenant une variable d'environnement avec votre clé API secrète d'environnement de test Stripe.

**Sécurité :** Ajoutez une règle dans votre `.gitignore` pour que ce fichier ne soit pas versionné sur Github.

## Étape 3 - Installation des librairies

Utilisez Composer pour installer les librairies suivantes à la racine de votre projet :

  - PHP Stripe `v13.10`
  - PHP Dotenv `v5.6`

Assurez-vous que le dossier `./vendor` est créé à la racine de votre projet. Vérifiez également les numéros de versions dans `composer.json`.

## Étape 4 - Configuration de Stripe JS

### Étape 4.1 - Dans le fichier `checkout.html` :
Chargez le javascript distant de la librairie Stripe.js v3 dans la balise `<head>` en vous référant à la documentation adéquate.
### Étape 4.2 - Dans le fichier `checkout.js` : 

En lieu et place de :
```javascript
const stripe;
````
 Initialisez une instance de Stripe dans la variable constante `stripe` avec votre clé publique de test. 
 Dans le but de permettre au code Javascript de communiquer avec Stripe.

---


Puis dans la fonction associée à la soumission du formulaire de paiement, spécifiez l'url absolue de retour après la confirmation d'un paiement au format : `https://VOTRELOGIN.sites.3wa.io/php/bre02-php-donate-for-ducks/public/app/views/checkout.html`

 Dans le but de retourner sur la page du formulaire de donation une fois un paiement effectué.

## Étape 5 - Configuration de Stripe PHP

Au début du fichier `create.php`, utilisez la librairie PHP Dotenv pour récupérer votre clé secrète contenue dans votre fichier `.env` afin de créer une instance de `StripeClient` dans une variable nommée `$stripe`. 

Cette instance sera utilisée en étape 7.2 pour interagir avec l'API de Stripe via PHP.

## Étape 6 - Récupération du montant de la donation
Dans la partie Javascript de l'application ajoutez un comportement lorsque l'utilisateur change son montant de donation.

En lieu et place des lignes : 
```javascript
let amount;
initialize();
```
Comportements attendu :
- Lorsque le montant change, mettez à jour la valeur de la variable `amount` avec le nouveau montant choisi.
- Si le montant est égal ou supérieur à 1€, appelez la fonction "initialize()" à ce moment précis de l'exécution.

## Étape 7 - Retour côté serveur
Dans la partie PHP de l'application, ajoutez un comportement pour que lorsque l'utilisateur change son montant de donation.

### Étape 7.1 - Calcul du montant à transmettre à Stripe

Révision de la fonction calculateOrderAmount :
- Assurez-vous que la fonction `calculateOrderAmount` retourne de manière sécurisée le bon montant de donation sans changer sa définition.

### Étape 7.2 - Création de l'intention de paiement
En lieu et place de :
```php
// TODO : Create a PaymentIntent with amount and currency in '$paymentIntent'
````
Instanciation du paymentIntent :
- Créez un `paymentIntent` en renseignant le montant de la transaction et sa devise.
- Utilisez la fonction `calculateOrderAmount` pour transmettre le montant de la donation dans le bon format au `paymentIntent`.

## Étape 8 - Testez votre application
Votre application de donation étant désormais 100% fonctionnelle en théorie. 

Je vous invite tester son comportement en contrôlant les évènements qui se produisent sur : 
- la page des évènements Stripe https://dashboard.stripe.com/test/events 
- ou celle des logs de tout vos appels à l'API https://dashboard.stripe.com/test/logs

Pour considérer une transaction réussie vous devez obtenir dans les évènements les messages suivant :

- `La tentative de paiement REFERENCE de 42,00 € a réussi`
- `Un montant de 42,00 € a été débité à REFERENCE`
---

> En cas de besoin, n'oubliez pas de vous concerter avec votre 🦆 ou de lire les documentations
>### Liens utiles :
>- Documentation Stripe JS : https://stripe.com/docs/js
>- Documentation Stripe PHP : https://stripe.com/docs/api?lang=php
>- Documentation Stripe Testing : https://stripe.com/docs/testing?locale=fr-FR
>- Votre ami : https://www.google.com
