## 1. Contourner une connexion sans mot de passe (SQL Injection)



**Problème** : le formulaire de connexion fait confiance à ce que l'utilisateur tape, sans le vérifier.



**Ce que j'ai fait** : j'ai intercepté la requête de connexion avec Burp Suite et remplacé l'email par `' or 1=1--` :



![Requête interceptée avec le payload SQL](/screenshots/01-sql-injection.png)



**Résultat** : connecté instantanément en tant qu'administrateur, sans connaître le mot de passe.



![Connexion réussie sur le compte admin](/screenshots/02-admin-login-success.png)



**Pourquoi ça marche** : le `'` referme la requête SQL plus tôt que prévu, `OR 1=1` ajoute une condition toujours vraie, et `--` commente la fin de la requête (dont la vérification du mot de passe).



---



## 2. Deviner un mot de passe automatiquement (Broken Authentication)



**Problème** : aucune limite sur le nombre d'essais de connexion.



**Ce que j'ai fait** : j'ai testé automatiquement 1000 mots de passe courants avec Burp Intruder sur le compte admin.



![Résultats Burp Intruder, code 200 trouvé](/screenshots/03-brute-force-intruder.png)



**Résultat** : le mot de passe `admin123` trouvé en quelques minutes.



---



## 3. Réinitialiser le mot de passe de quelqu'un via une recherche Google (Broken Authentication)



**Problème** : la question de sécurité est devinable avec une simple recherche.



**Ce que j'ai fait** : un avis client m'a mené à un personnage de Star Trek, j'ai trouvé le nom de son frère sur Google.



![Recherche Google sur la famille du personnage](/screenshots/04-star-trek-family.png)



**Résultat** : mot de passe changé sans jamais connaître l'original.



![Formulaire de réinitialisation rempli](/screenshots/05-forgot-password.png)



---



## 4. Trouver un document confidentiel caché (Sensitive Data Exposure)



**Problème** : un dossier du serveur était accessible publiquement sans y penser.



**Ce que j'ai fait** : en explorant une simple URL, je suis tombé sur une liste de fichiers.



![Listing du dossier /ftp/](/screenshots/06-ftp-listing.png)



**Résultat** : accès à un document interne marqué confidentiel.



![Contenu du document confidentiel](/screenshots/07-acquisitions-confidential.png)



---



## 5. Accéder au panier d'un autre client (Broken Access Control — IDOR)



**Problème** : le site ne vérifie pas que le panier demandé appartient bien à la personne connectée.



**Ce que j'ai fait** : changé un simple chiffre dans l'URL de la requête (`basket/1` → `basket/2`).



![Requête Burp modifiée](/screenshots/08-idor-basket.png)



**Résultat** : accès au panier d'un autre utilisateur.



---



## 6. Faire exécuter du code dans le navigateur (XSS)



**Problème** : le site réaffiche ce qu'on tape sans le filtrer.



**Ce que j'ai fait** : tapé un petit bout de code dans la barre de recherche : <iframe src="javascript:alert('test injection xss')"> ```



Résultat : une fenêtre d’alerte s’est déclenchée, preuve qu’un pirate pourrait exécuter du code arbitraire.



![Pop-up XSS](/screenshots/09-popup-xss.png)



# Conclusion



Ces tests m’ont permis de comprendre concrètement les failles les plus courantes du

Top 10 OWASP et comment les développeurs doivent s’en protéger : validation côté

serveur, limitation des tentatives de connexion, et échappement systématique des

entrées utilisateur.

