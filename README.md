# Fly_Buzz


## Requêtes

Afficher les aéroports dans l'ordre alphabétique des villes :
````sql
SELECT * FROM destination ORDER BY ville
````
Le pilote Clarence Oveur est malade le 23/06/2019 et est remplacé, sur son vol, par Ted Striker :
````sql
UPDATE vol SET pilot_2=1 WHERE depart_vol_date='2019-06-23'
````

Ajouter une nouvelle destination, l'aéroport de  Pochentong à Phnom Penh :
````sql
INSERT INTO destination(ville, aeroport) VALUES('Phnom Penh', 'Pochentong')
````
