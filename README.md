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

````sql
create view pilote_avion
as select pilotes.nom, appareils.numero from pilotes
join vol_pilote on vol_pilote.id_pilote = pilotes.id_pilote
join vols on vols.id_vol = vol_pilote.id_vol
join appareils on vols.id_appareil = appareils.id_appareil;


select * from pilote_avion order by nom
````

````sql
DELIMITER //
CREATE PROCEDURE afficher_avions_avant (IN date_arg YEAR)
BEGIN
SELECT * FROM appareils AS a WHERE a.date_entree_service < date_arg;
END //
DELIMITER
````

````sql
DELIMITER //
CREATE PROCEDURE vols_avion
(IN numero_avion CHAR(5))
BEGIN
SELECT numero, (SELECT ville FROM destinations WHERE depart = id) AS ville_depart, (SELECT ville FROM destinations WHERE arrivee = id) AS ville_arrivee, date_depart, date_arrivee
FROM vols
WHERE avion = (SELECT id from appareils WHERE numero = numero_avion);
END //
DELIMITER ;
````

````sql
DELIMITER |

CREATE PROCEDURE duree_vol2 
(IN p_num_vol VARCHAR(5)) 
BEGIN 
SELECT *, TIMEDIFF((ADDTIME(date_arrivee, heure_arrivee)), (ADDTIME(date_depart, heure_depart))) AS duree_vol FROM vols WHERE num_vol = p_num_vol;
END|
DELIMITER

CALL duree_vol2('MS293')
````
