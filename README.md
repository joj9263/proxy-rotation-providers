# Proxy rotatif : comment ça marche, comment régler la rotation et quel fournisseur choisir pour le scraping et le multi-comptes

Vous lancez un scraper, les 400 premières requêtes passent, puis votre script commence à recevoir des pages CAPTCHA à la place des données. Le code n'a pas changé. C'est l'adresse IP qui a été identifiée comme un seul client envoyant trop de trafic en trop peu de temps. Un proxy rotatif règle précisément ce problème : au lieu de sortir par une seule adresse, vos requêtes se répartissent sur un pool d'IP qui change selon une règle que vous définissez.

Le reste de l'article parle de ce qui compte vraiment quand on cherche un proxy rotatif en 2026 : la différence entre rotation et session sticky, pourquoi le résidentiel coûte plus cher que le datacenter sans être un luxe, comment se configure la rotation chez 9Proxy, et combien coûtent réellement les différents packs.

## Rotation et sticky : deux comportements, deux problèmes différents

Un proxy rotatif attribue une nouvelle IP selon un déclencheur. Ce déclencheur peut être une requête, une durée, ou un clic manuel. Tout l'intérêt est là : chaque requête semble venir d'un utilisateur distinct.

Le mode sticky fait l'inverse. Il garde la même IP pendant X minutes, parce que certains sites ne regardent pas le nombre de requêtes mais la cohérence de votre identité. Si vous vous connectez à un compte depuis cinq villes différentes en deux minutes, vous êtes plus suspect qu'un utilisateur envoyant dix requêtes depuis une seule IP.

Concrètement, le mauvais choix se voit vite :

- Rotation trop agressive sur un workflow connecté : le panier se vide, la session expire, le formulaire en trois étapes casse à la deuxième.
- Sticky trop long sur du scraping de volume : vous retombez dans le problème initial, la même IP prend le rate limit et se fait bloquer.

La plupart des fournisseurs sérieux laissent les deux modes cohabiter sur le même compte. Chez 9Proxy, le mode rotatif bascule sur une nouvelle IP automatiquement, et le mode sticky conserve l'adresse jusqu'à la fin de la durée de session configurée. Vous pouvez donc faire tourner vos requêtes de collecte et garder vos sessions de compte sur des identifiants séparés, ce qui est la configuration la plus saine dès que vous mélangez scraping et gestion de comptes.

👉 [Commencer avec des IP résidentielles rotatives](https://bit.ly/9-Proxy)

## Résidentiel, datacenter ou mobile : le choix du pool change tout

Le type d'IP compte plus que la taille du pool dans la plupart des échecs réels.

Les IP de datacenter sont rapides et bon marché. Elles appartiennent à des plages connues, répertoriées comme telles, et les protections anti-bot modernes les trient en priorité. Elles restent pertinentes sur du contenu peu protégé ou pour du téléchargement.

Les IP résidentielles sont des adresses attribuées par des fournisseurs d'accès à des connexions domestiques. Du point de vue du serveur cible, votre trafic ressemble à celui d'une personne normale dans une ville donnée. C'est ce qui permet de passer les vérifications de réputation d'IP et, accessoirement, de voir le contenu réellement servi dans cette zone. Un site e-commerce affiche rarement les mêmes prix ni les mêmes stocks selon le pays.

Les IP mobiles sont encore plus difficiles à classer comme suspectes, mais elles coûtent sensiblement plus cher et servent surtout à des cas précis de tests sur réseaux opérateurs.

9Proxy ne propose que du résidentiel : plus de 20 millions d'IP dans plus de 90 pays, avec ciblage jusqu'au pays, à l'État, à la ville, au code postal et au FAI selon le modèle de facturation choisi. Les pools les plus profonds cités côté fournisseur concernent les États-Unis, le Canada, la France, le Royaume-Uni et l'Allemagne. Si vos cibles sont hébergées majoritairement en Amérique du Nord et en Europe de l'Ouest, vous êtes dans la zone la mieux servie.

## Où la rotation change réellement les résultats

Le scraping est le cas d'usage le plus évident, mais pas le seul.

**Suivi de positions SEO.** Les SERP varient d'une ville à l'autre. Tester un classement depuis une ville précise demande une IP qui se trouve réellement dans cette ville, sinon vous mesurez une version du moteur configurée pour votre zone, pas pour celle de votre client.

**Vérification publicitaire.** Contrôler qu'une campagne s'affiche correctement pour un utilisateur d'un pays donné nécessite des IP que la régie traitera comme des utilisateurs locaux. Une IP serveur est souvent exclue de la logique de diffusion.

**Suivi de prix et de stocks.** Les plateformes servent des prix différents selon la géographie. Répartir les vérifications sur plusieurs IP évite de déclencher le rate limiting dès la dixième page produit.

**Multi-comptes et automatisation sociale.** Ici, c'est l'inverse : la rotation agressive est un signal d'alerte. Un compte qui change d'IP à chaque requête est repéré plus vite qu'un compte stable. La session sticky est le réglage correct.

**OSINT et recherche sécurité.** Le pool d'IP fait partie du profil de l'analyste. Répartir les requêtes sur des IP résidentielles de la région cible évite d'apparaître comme un balayage systématique.

Un point qui revient souvent dans les discussions : la rotation ne dispense pas de rythmer vos requêtes. Une IP neuve à chaque requête ne protège pas si vous envoyez cinquante requêtes par seconde. Un délai et une variation aléatoire restent la base.

## Deux façons de payer la rotation chez 9Proxy

C'est le point qui déroute le plus au moment de l'achat, et l'erreur la plus fréquente consiste à choisir un modèle inadapté à sa charge de travail.

**Le modèle par IP** vous donne un nombre fixe d'IP résidentielles avec bande passante illimitée. Vous payez l'adresse, pas les octets. Les IP non utilisées n'expirent pas. En contrepartie, chaque IP a une durée de vie naturelle limitée, de quelques heures à environ 24 heures selon l'adresse, avec une moyenne constatée autour de trois heures. Autre contrainte : ce modèle suppose l'application desktop de 9Proxy, qui fait le transfert de port en local.

**Le modèle par Go** vous facture le trafic consommé. Vous générez autant d'endpoints que nécessaire, sans activer d'IP une par une, et vous choisissez entre rotation automatique ou session sticky. La validité du trafic est de 180 jours (illimitée en Enterprise). L'authentification se fait par identifiant/mot de passe ou par liste blanche d'IP, directement depuis le tableau de bord, sans application à installer.

Une durée de validité de 180 jours change la donne si votre charge est irrégulière : vous ne perdez pas le solde acheté parce que le mois se termine.

| Critère | Par IP | Par Go |
| --- | --- | --- |
| Facturation | Forfait par nombre d'IP | Forfait par volume de Go |
| Bande passante | Illimitée tant que l'IP est active | Limitée aux Go achetés |
| Génération d'endpoints | 1 IP = 1 attribution | Illimitée, seuls les Go sont décomptés |
| Rotation | Pas de rotation naturelle ; via Auto Rotation Proxy sur ports sélectionnés | Rotative (nouvelle IP) ou sticky (IP conservée X minutes) |
| Durée de vie d'une IP | Quelques heures à ~24 h | Pas de durée de vie fixe, l'IP tourne au fil des requêtes |
| Validité | Illimitée jusqu'à épuisement des IP | 180 jours (illimitée en Enterprise) |
| Ciblage | Pays, État, ville | Pays, État, ville, code postal, FAI |
| Authentification | Application 9Proxy (port local) | Identifiant/mot de passe ou liste blanche d'IP |

Règle simple : si votre tâche consomme beaucoup de bande passante mais peu d'adresses distinctes, prenez le mode par IP. Si elle consomme peu de données par requête mais a besoin de milliers d'IP différentes, le mode par Go revient moins cher.

## Tarifs 9Proxy : les plans actuels

9Proxy a annoncé le 18 mai 2026 son premier ajustement tarifaire depuis la création du service, appliqué à partir du 1er juin 2026 sur les packs par IP et les bundles. Les packs par Go n'ont pas bougé.

### Packs facturés par IP (bande passante illimitée)

| Volume | Prix total | Prix unitaire indicatif | Trafic |
| --- | --- | --- | --- |
| 100 IP | 24 $ | 0,24 $/IP | Illimité |
| 500 IP | 72 $ | 0,14 $/IP | Illimité |
| 1 000 IP (+ 500 offertes) | 126 $ | ~0,08 $/IP | Illimité |
| 100 000 IP | 2 300 $ | 0,023 $/IP | Illimité |
| 500 000 IP | 8 625 $ | ~0,017 $/IP | Illimité |

Entre ces paliers, 9Proxy propose d'autres volumes (2 500, 5 000, 15 000, 25 000, 50 000 IP) dont le tarif unitaire suit la même dégressivité. Le prix exact de chaque palier s'affiche dans le tableau de bord au moment de l'achat.

👉 [Voir les packs par IP disponibles](https://bit.ly/9-Proxy)

### Packs facturés au Go (rotation d'IP, validité 180 jours)

| Volume | Prix total | Prix par Go |
| --- | --- | --- |
| 5 Go | 15 $ | 3,00 $/Go |
| 50 Go (+ 5 Go offerts) | 105 $ | 2,10 $/Go |
| 100 Go | 150 $ | 1,50 $/Go |
| 200 Go | 200 $ | 1,00 $/Go |
| 1 000 Go | 800 $ | 0,80 $/Go |
| 2 000 Go | 1 500 $ | 0,75 $/Go |

Au-delà, le tarif continue de descendre et atteint 0,68 $/Go sur les plus gros volumes (à partir du palier 10 000 Go).

👉 [Choisir un pack au Go](https://bit.ly/9-Proxy)

### Bundles IP + Go

| Bundle | Contenu | Prix |
| --- | --- | --- |
| Starter | 100 IP + 5 Go | 30 $ |
| Popular | 1 500 IP + 50 Go | 180 $ |
| Pro | 5 000 IP + 500 Go | 720 $ |

Les bundles combinent les deux logiques dans un seul pack : une partie du travail garde des IP stables, l'autre tourne en volume. Le trafic inclus est valable 180 jours.

👉 [Prendre un pack combiné](https://bit.ly/9-Proxy)

### Enterprise

Offre sur devis, avec validité de données illimitée, mode équipe (1 propriétaire et jusqu'à 5 membres), partage de bande passante sans expiration à l'intérieur de l'équipe, contrôles de trafic par membre, journaux d'activité complets et création illimitée de codes de partage.

👉 [Demander les conditions Enterprise](https://bit.ly/9-Proxy)

## Configurer la rotation : ce qui se règle réellement

Trois mécanismes à connaître chez 9Proxy.

**Le générateur de proxies.** Il permet de sélectionner pays, État, ville, code postal ou FAI, de choisir le mode de session (rotative ou sticky) et d'extraire les endpoints au format souhaité. Tout se passe dans le tableau de bord pour les packs au Go.

**L'Auto Rotation Proxy.** Sur les packs par IP, la rotation naturelle n'existe pas : vous définissez un intervalle de rotation personnalisé sur les ports sélectionnés. C'est ce réglage qui transforme un pack par IP en rotation contrôlée.

**L'Auto-Refresh.** Quand une IP d'un port tombe, le port bascule automatiquement sur une IP vivante. Sur des jobs longs, c'est ce qui évite la cascade de « connection refused » au milieu d'un run.

Deux garde-fous valent la peine d'être cités parce qu'ils ne sont pas standards dans le secteur. La politique de remplacement en 60 secondes : si une IP échoue dans la minute suivant son activation, elle est recréditée automatiquement. Et la « Today List » : les proxies utilisés dans les dernières 24 heures peuvent être réutilisés sans frais supplémentaires si l'adresse est à nouveau disponible, ce qui réduit le gaspillage sur les tests répétés.

## Compatibilité avec vos outils

Les protocoles supportés sont HTTP, HTTPS et SOCKS5. Le SOCKS5 compte : il fonctionne au niveau transport, ce qui le rend nécessaire pour proxyfier du trafic non HTTP et pour maintenir des connexions longues. Puppeteer, Playwright, Scrapy et proxychains s'intègrent sans conversion de protocole.

Le format d'authentification classique `host:port:user:pass` est celui attendu par les navigateurs anti-détection. Les retours d'utilisateurs mentionnent régulièrement AdsPower, Dolphin Anty et BitBrowser. Il existe aussi une API publique pour générer et faire tourner les proxies par code, ce qui évite de repasser par le tableau de bord à chaque session.

## Les limites à connaître avant d'acheter

Aucun fournisseur de proxys résidentiels n'échappe à ces points, mais autant les avoir en tête avant de payer.

Il n'existe pas de plan gratuit permanent. Des IPs de test peuvent être obtenues via le support ou des promotions ponctuelles, mais il n'y a pas d'essai gratuit standard et sans condition. Si vous voulez valider une cible difficile avant d'engager un budget, votre meilleure option reste un petit pack d'entrée et la politique de remplacement à 60 secondes.

Certaines IP tombent. C'est structurel dans un pool résidentiel, pas propre à ce fournisseur. Le remplacement automatique gère les échecs immédiats, mais une IP qui meurt après plusieurs heures demande une intervention manuelle pour demander un remplacement.

La gamme est exclusivement résidentielle. Pas de datacenter, pas de résidentiel statique de type ISP, pas de mobile en produit séparé. Si votre workflow repose sur une IP fixe de longue durée pour des comptes sensibles, il faudra compléter avec un second fournisseur.

Sur la fiabilité, il faut signaler un point d'honnêteté : plusieurs sites tiers ont rapporté des interruptions de service de 9Proxy en juin puis en août 2026, et des utilisateurs se plaignent sur Trustpilot d'IP mortes après une semaine ou de remboursements difficiles à obtenir au-delà de la fenêtre de 60 secondes. La société répond à ces avis. Cela ne change rien à la qualité du service quand il tourne, mais ça justifie une précaution simple : ne verrouillez pas l'intégralité de votre budget chez un seul fournisseur, et testez avec un pack d'entrée avant de passer à l'échelle.

## Comment démarrer

1. Créer le compte et confirmer l'adresse e-mail. Pas de processus KYC bloquant avant de pouvoir générer des identifiants, contrairement aux plateformes enterprise.
2. Choisir le modèle de facturation. Rotation intensive sur du volume faible par requête, c'est le Go. Sessions longues avec trafic imprévisible, c'est l'IP.
3. Générer les endpoints dans le tableau de bord, en sélectionnant le ciblage géographique et le type de session.
4. Coller l'endpoint dans votre outil, en HTTP ou SOCKS5 selon l'intégration.
5. Lancer un petit lot avant le vrai run : vérifiez le taux de blocage par cible et ajustez le rythme des requêtes.

👉 [Ouvrir un compte et tester la rotation](https://bit.ly/9-Proxy)

## Questions fréquentes

**Un proxy rotatif, c'est légal ?**
L'usage de proxys résidentiels est légal dans la plupart des juridictions. Ce qui est encadré, c'est l'usage : respect des conditions d'utilisation des sites cibles, des lois locales et des règles de protection des données.

**Quelle est la différence entre rotation et sticky ?**
La rotation change d'IP automatiquement selon votre règle (par requête ou par session). Le sticky conserve la même IP pendant une durée configurable. La rotation sert au volume et à l'anonymat, le sticky aux workflows connectés.

**Combien de temps vit une IP résidentielle chez 9Proxy ?**
Sur les packs par IP, de quelques heures à environ 24 heures, avec une moyenne constatée autour de trois heures. Sur les packs par Go, il n'y a pas de durée de vie fixe : l'IP tourne quand vous le demandez.

**Le solde non utilisé expire-t-il ?**
Les IP d'un pack par IP ne sont pas perdues tant qu'elles ne sont pas utilisées. Le trafic des packs au Go est valable 180 jours, et sans expiration en Enterprise.

**Ça fonctionne avec AdsPower ou Dolphin Anty ?**
Oui, en SOCKS5 ou HTTP avec authentification par identifiant/mot de passe. La liste blanche d'IP est également prise en charge sur les packs au Go.

## Verdict

Si votre problème est le blocage après quelques centaines de requêtes, la rotation résidentielle est la bonne réponse, et le mode par Go de 9Proxy est le plus direct : vous générez des endpoints illimités, vous payez ce que vous consommez, et les 180 jours de validité enlèvent la pression de consommation.

Si vous gérez des comptes et du volume en parallèle, le pack par IP avec bande passante illimitée revient moins cher au gigaoctet, à condition d'accepter la contrainte de l'application desktop et la durée de vie variable des adresses.

Dans les deux cas, commencez petit. Un pack à 24 $ ou 15 $ suffit pour mesurer le taux de réussite sur vos cibles réelles, et vous saurez en une journée si le pool correspond à vos besoins — ce qui vaut mieux que n'importe quel comparatif, y compris celui-ci.

👉 [Voir les offres actuelles de 9Proxy](https://bit.ly/9-Proxy)
