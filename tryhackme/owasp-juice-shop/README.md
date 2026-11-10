## Contexte

Le serveur cible héberge **OWASP Juice Shop**, une application web volontairement 
truffée de failles de sécurité, utilisée pour s'entraîner à repérer et exploiter 
de vraies vulnérabilités web, sans risque.

### Vulnérabilités traitées dans ce write-up

- **SQL Injection** — contournement d'authentification
- **Broken Authentication** — brute force et réinitialisation de mot de passe
- **Sensitive Data Exposure** — accès à un dossier confidentiel
- **Broken Access Control** — accès admin et IDOR
- **Cross-Site Scripting (XSS)** — DOM, persistant et réfléchi

### Outils utilisés

- **Burp Suite** — interception et modification des requêtes HTTP (Proxy, Intruder)
- **SecLists** — dictionnaire de mots de passe pour le brute force
