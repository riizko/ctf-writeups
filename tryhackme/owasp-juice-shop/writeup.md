\## Contourner une connexion sans mot de passe (injection SQL)



Le formulaire de connexion fait confiance à ce que l'utilisateur tape, sans le vérifier.



J'ai intercepté la requête de connexion avec Burp Suite et remplacé l'email par `' or 1=1--` :



! C:\\Users\\laure\\OneDrive\\Pictures\\Screenshots\\Image1.png

! C:\\Users\\laure\\OneDrive\\Pictures\\Screenshots\\Image2.png



Résultat : connecté instantanément en tant qu'administrateur, sans connaître le mot de passe.



! C:\\Users\\laure\\OneDrive\\Pictures\\Screenshots\\Image3.png

