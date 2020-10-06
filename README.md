
Exercices 1 : 
Créer une base de donnée "db_1" qui contient une table "users" qui correspond à la database que nous avons créé dans le cour précédent sur express

```
postgres=> CREATE DATABASE db_1;
CREATE DATABASE
postgres=> \c db_1;
You are now connected to database "db_1" as user "db_user".
db_1=> CREATE TABLE users (id SERIAL PRIMARY KEY, name VARCHAR(30), password VARCHAR(30));
CREATE TABLE
db_1=> INSERT INTO users (name, password) VALUES ('Alice', '123'), ('Bob', '456'), ('Charlie', '789');
INSERT 0 3
db_1=> SELECT \* FROM users;
id | name | password
----+---------+----------
1 | Alice | 123
2 | Bob | 456
3 | Charlie | 789
(3 rows)
```

Exercices 2 : 
Ajouter 3 utilisateurs 'dan', 'eve', 'faythe' qui auront respectivement les password '101112', '131415', '161718'.
Affichez toutes les lignes de la table "users" de la base de donnée "db_1".

```
db_1=> INSERT INTO users (name, password) VALUES ('Dan', '101112'), ('Eve', '131415'), ('Faythe', '161718');
INSERT 0 3
db_1=> SELECT \* FROM users;
id | name | password
----+---------+----------
1 | Alice | 123
2 | Bob | 456
3 | Charlie | 789
4 | Dan | 101112
5 | Eve | 131415
6 | Faythe | 161718
(6 rows)
```

Exercice 3 : 
Affichez toutes les lignes de la table "users" de la base de donnée "db_1" dont le password possède plus de 3 caractères. Pour cela il vous faudra utiliser la fonction LENGTH.

```
db_1=> SELECT * FROM users WHERE length(password) > 3;
id | name | password
----+--------+----------
4 | Dan | 101112
5 | Eve | 131415
6 | Faythe | 161718
(3 rows)
```

Exercice 4 : 
Modifiez la table "users" afin d'ajouter une nouvelle colonne "bio" qui contiendra une description a propos de l'utilisateur. Ce champ "bio" sera du texte avec un nombre de caractères illimités et sa valeur par défaut sera "Hello, world!" Vous devrez fournir les commandes SQL entrées ainsi que tous les outputs de ces commandes

```
db_1=> ALTER TABLE users ADD COLUMN bio TEXT DEFAULT 'Hello, World !';
ALTER TABLE
db_1=> SELECT \* FROM users;
id | name | password | bio
----+---------+----------+----------------
1 | Alice | 123 | Hello, World !
2 | Bob | 456 | Hello, World !
3 | Charlie | 789 | Hello, World !
4 | Dan | 101112 | Hello, World !
5 | Eve | 131415 | Hello, World !
6 | Faythe | 161718 | Hello, World !
(6 rows)
```

Exercice 5 :
Modifiez toutes les lignes existantes pour que la "bio" de chacun affiche, "Hello, i am PRENOM_DU_USER".
Il faudra remplacer PRENOM_DU_USER par le véritable login de l'utilisateur.

```
db_1=> UPDATE users SET bio = 'Hello, i am Alice' WHERE name = 'Alice';
UPDATE 1
db_1=> UPDATE users SET bio = 'Hello, i am Bob' WHERE name = 'Bob';
UPDATE 1
db_1=> UPDATE users SET bio = 'Hello, i am Charlie' WHERE name = 'Charlie';
UPDATE 1
db_1=> UPDATE users SET bio = 'Hello, i am Dan' WHERE name = 'Dan';
UPDATE 1
db_1=> UPDATE users SET bio = 'Hello, i am Eve' WHERE name = 'Eve';
UPDATE 1
db_1=> UPDATE users SET bio = 'Hello, i am Faythe' WHERE name = 'Faythe';
UPDATE 1
db_1=> SELECT \* FROM users;
id | name | password | bio
----+---------+----------+---------------------
1 | Alice | 123 | Hello, i am Alice
2 | Bob | 456 | Hello, i am Bob
3 | Charlie | 789 | Hello, i am Charlie
4 | Dan | 101112 | Hello, i am Dan
5 | Eve | 131415 | Hello, i am Eve
6 | Faythe | 161718 | Hello, i am Faythe
(6 rows)
```

Exercice 6 : 
Afficher les 2 lignes qui ont les "id" les plus grands par ordre décroissant. Vous devrez fournir les commandes SQL entrées ainsi que tous les outputs de ces commandes.

```
db_1=> SELECT \* FROM users ORDER BY id DESC LIMIT 2;
id | name | password | bio
----+--------+----------+--------------------
6 | Faythe | 161718 | Hello, i am Faythe
5 | Eve | 131415 | Hello, i am Eve
(2 rows)
```

Exercice 7 : 
Afficher toutes les lignes de la table "users" dont les "id" sont impairs par ordre croissant.

```
db_1=> SELECT \* FROM users WHERE id % 2 = 1;
id | name | password | bio
----+---------+----------+---------------------
1 | Alice | 123 | Hello, i am Alice
3 | Charlie | 789 | Hello, i am Charlie
5 | Eve | 131415 | Hello, i am Eve
(3 rows)
```

Exercice 8 : 
Effacez toutes les lignes de la table "users dont les "id" sont pairs. Affichez toutes les lignes de la table users.

```
db_1=> DELETE FROM users WHERE id % 2 = 0;
DELETE 3
db_1=> SELECT \* FROM users;
id | name | password | bio
----+---------+----------+---------------------
1 | Alice | 123 | Hello, i am Alice
3 | Charlie | 789 | Hello, i am Charlie
5 | Eve | 131415 | Hello, i am Eve
(3 rows)
```

Exercice 9 : 
Effacer la TABLE "user".
Effacer la DATABASE "db_1".

```
db_1=> DROP TABLE users;
DROP TABLE
db_1=> \c postgres
You are now connected to database "postgres" as user "db_user".
postgres=> DROP DATABASE db_1;
DROP DATABASE
postgres=> \list
List of databases
Name | Owner | Encoding | Collate | Ctype | Access privileges
-----------+--------+----------+---------+-------+-------------------
postgres | lsn971 | UTF8 | C | C |
template0 | lsn971 | UTF8 | C | C | =c/lsn971 +
| | | | | lsn971=CTc/lsn971
template1 | lsn971 | UTF8 | C | C | =c/lsn971 +
| | | | | lsn971=CTc/lsn971
(3 rows)

postgres=>
```
