CREATE TABLE auteur (nom VARCHAR(90),
                    prenom VARCHAR(90),
                    auteur_id INT PRIMARY KEY);

CREATE TABLE livre (titre VARCHAR(120),
                   auteur_id REFERENCES auteur(auteur_id),
                   editeur VARCHAR(90),
                   annee INT,
                   isbn CHAR(13) PRIMARY KEY);

CREATE TABLE usager (nom VARCHAR(90),
                    prenom VARCHAR(90),
                    adresse VARCHAR(200),
                    cp CHAR(5),
                    ville VARCHAR(200),
                    mail VARCHAR(90),
                    code_barre VARCHAR(15) PRIMARY KEY);

CREATE TABLE emprunt(usager_id VARCHAR(60) REFERENCES usager(code_barre),
                    isbn VARCHAR(60) REFERENCES livre(isbn),
                    retour DATE,
                    PRIMARY KEY(usager_id,isbn));
                    
                    
INSERT INTO auteur VALUES ("Voltaire",null,1);
INSERT INTO auteur VALUES ("Hugo","Victor",2),("Molière",null,3),("Baudelaire","Charles",4);
INSERT INTO auteur (auteur_id,nom,prenom) VALUES (5,"Mainville","Jacques");


INSERT INTO livre VALUES ("Candide",1,"Magnard",2013,'123456790123'),("Zadig",1,"Garnier",1997,"1234657890456");
INSERT INTO livre VALUES ("Les misérables",2,"Gallimard",2021,"9876543210987"),("Notre-Dame de Paris",2,"Hatier",2000,"9876543210654"),("Les contemplations",2,"Hachette",1984,"9876543210321");
INSERT INTO livre VALUES ("Le misanthrope",3,"Gallimard",2013,"0123456789123"),("L'avare",3,"Garnier",1997,"0123456789456"),("Tartuffe",3,"Hatier",1997,"0123456789789"),("Le malade imaginaire",3,"Gallimard",1984,"0123456789147");
INSERT INTO livre VALUES ("Les fleurs du mal",4,"Garnier",2005,"1472583690147"),("Le spleen de Paris",4,"Flammarion",2004,"1472583690258");
INSERT INTO livre VALUES ("Napoléon",5,"Hachette",1967,"0147258369147");

INSERT INTO usager VALUES ("Utilisateur","Prénom","12 rue d'Ornay","76000","Rouen","test@gmail.com","123456789012345"),("Utilisateur","Nom","3 rue chemin de fer","76770","Le Houlme","rouen@laposte.net","012345678912345");
INSERT INTO emprunt VALUES("123456789012345","0123456789789","2023-02-06"),("123456789012345","123456790123","2023-02-06"),("123456789012345","1472583690147","2023-02-06");
INSERT INTO emprunt VALUES("012345678912345","0123456789123","2023-02-13"),("012345678912345","1472583690258","2023-02-13");

/*-- Test --*/

SELECT nom,prenom FROM auteur;
SELECT nom,prenom FROM usager WHERE auteur_id >= 3;
SELECT isbn FROM emprunt WHERE usager_id = "123456789012345";
SELECT livre.titre FROM emprunt JOIN livre ON emprunt.isbn=livre.isbn WHERE usager_id = "123456789012345";
SELECT usager.mail, livre.titre,emprunt.retour FROM emprunt JOIN usager,livre ON emprunt.usager_id=usager.code_barre AND emprunt.isbn=livre.isbn WHERE retour<"2023-02-10";
SELECT auteur.nom,auteur.prenom FROM auteur JOIN livre ON auteur.auteur_id=livre.auteur_id WHERE titre="Les fleurs du mal";
SELECT livre.titre FROM livre,auteur ON livre.auteur_id=auteur.auteur_id WHERE editeur='Gallimard' AND usager.prenom="Molière";
SELECT livre.titre FROM livre WHERE editeur='Garnier';
SELECT titre FROM livre WHERE annee<= (SELECT annee FROM livre WHERE titre="Les fleurs du mal");
SELECT auteur.nom,auteur.prenom FROM auteur JOIN livre ON livre.auteur_id=auteur.auteur_id WHERE annee <= (SELECT annee FROM livre WHERE titre="Les fleurs du mal");
SELECT DISTINCT auteur.nom,auteur.prenom FROM auteur JOIN livre ON livre.auteur_id=auteur.auteur_id WHERE annee <= (SELECT annee FROM livre WHERE titre="Les fleurs du mal");
SELECT COUNT(toto.nom) AS Total FROM (SELECT DISTINCT auteur.nom,auteur.prenom FROM auteur JOIN livre ON livre.auteur_id=auteur.auteur_id WHERE annee <= (SELECT annee FROM livre WHERE titre="Les fleurs du mal")) AS toto;
SELECT l.titre FROM livre AS l WHERE l.isbn IN (SELECT isbn FROM livre WHERE annee>1990);
SELECT l.titre FROM livre AS l WHERE l.annee>1990;
