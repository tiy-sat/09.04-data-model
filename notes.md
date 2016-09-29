rnorwood=# CREATE TABLE person_data (
full_name varchar(30),
best_friend varchar(30),
age numeric(3),
birth_year numeric(4));
CREATE TABLE
rnorwood=# drop table person_data;
DROP TABLE
rnorwood=# CREATE TABLE person_data (
rnorwood(# id SERIAL PRIMARY KEY,
rnorwood(# full_name varchar(30),
rnorwood(# best_friend varchar(30),
rnorwood(# age numeric(3),
rnorwood(# birth_year numeric(4));
CREATE TABLE
rnorwood=# select * from person_data;
 id | full_name | best_friend | age | birth_year 
----+-----------+-------------+-----+------------
(0 rows)

rnorwood=# INSERT INTO person_data VALUES ('Robin Norwood', 'Kyle', 39, 1977);
ERROR:  invalid input syntax for integer: "Robin Norwood"
LINE 1: INSERT INTO person_data VALUES ('Robin Norwood', 'Kyle', 39,...
                                        ^
(failed reverse-i-search)`INSERTINSER': ^CSERT INTO person_data VALUES ('Robin Norwood', 'Kyle', 39, 1977);
rnorwood=# INSERT INTO person_data (full_name, best_friend, age, birth_year) VALUES ('Robin Norwood', 'Kyle', 39, 1977);
INSERT 0 1
rnorwood=# INSERT INTO person_data (full_name, best_friend, age, birth_year) VALUES ('George Washington CCCLIV', 'His Horse', 2016-1977, 1977);
INSERT 0 1
rnorwood=# SELECT * FROM person_data;
 id |        full_name         | best_friend | age | birth_year 
----+--------------------------+-------------+-----+------------
  1 | Robin Norwood            | Kyle        |  39 |       1977
  2 | George Washington CCCLIV | His Horse   |  39 |       1977
(2 rows)

rnorwood=# DELETE FROM person_data;
DELETE 2
rnorwood=# SELECT * FROM person_data;
 id | full_name | best_friend | age | birth_year 
----+-----------+-------------+-----+------------
(0 rows)

rnorwood=# INSERT INTO person_data (full_name, best_friend, age, birth_year) VALUES ('George Washington CCCLIV', 'His Horse', 2016-1977, 1977);
INSERT 0 1
rnorwood=# INSERT INTO person_data (full_name, best_friend, age, birth_year) VALUES ('Robin Norwood', 'Kyle', 39, 1977);
INSERT 0 1
rnorwood=# SELECT * FROM person_data;
 id |        full_name         | best_friend | age | birth_year 
----+--------------------------+-------------+-----+------------
  3 | George Washington CCCLIV | His Horse   |  39 |       1977
  4 | Robin Norwood            | Kyle        |  39 |       1977
(2 rows)

rnorwood=# CREATE TABLE horsies (id SERIAL PRIMARY KEY, teeth numeric(3), legs (numeric(1), coat_color varchar(32), name varchar(64), horned boolean, owner int references person_data(id));
rnorwood(# )
rnorwood-# ;
ERROR:  syntax error at or near "("
LINE 1: ...es (id SERIAL PRIMARY KEY, teeth numeric(3), legs (numeric(1...
                                                             ^
rnorwood=# CREATE TABLE horsies (id SERIAL PRIMARY KEY, teeth numeric(3), legs numeric(1), coat_color varchar(32), name varchar(64), horned boolean, owner int references person_data(id));
CREATE TABLE
rnorwood=# select * from horsies
rnorwood-# ;
 id | teeth | legs | coat_color | name | horned | owner 
----+-------+------+------------+------+--------+-------
(0 rows)

rnorwood=# INSERT INTO horsies (coat_color, name, owner) VALUES ("palamino", "Snekk", 3);
ERROR:  column "palamino" does not exist
LINE 1: ...RT INTO horsies (coat_color, name, owner) VALUES ("palamino"...
                                                             ^
rnorwood=# INSERT INTO horsies (coat_color, name, owner) VALUES ('palamino', "Snekk", 3);
ERROR:  column "Snekk" does not exist
LINE 1: ...ies (coat_color, name, owner) VALUES ('palamino', "Snekk", 3...
                                                             ^
rnorwood=# INSERT INTO horsies (coat_color, name, owner) VALUES ('palamino', 'Snekk', 3);
INSERT 0 1
rnorwood=# SELECT * FROM horsies
rnorwood-# ;
 id | teeth | legs | coat_color | name  | horned | owner 
----+-------+------+------------+-------+--------+-------
  1 |       |      | palamino   | Snekk |        |     3
(1 row)

rnorwood=# INSERT INTO horsies (legs, coat_color, name, owner) VALUES (4, 'black', 'King George', 3);
INSERT 0 1
rnorwood=# INSERT INTO horsies (legs, coat_color, name, owner) VALUES (3, 'pinto', 'Lambchop', 3);
INSERT 0 1
rnorwood=# SELECT * FROM horsies
rnorwood-# ;
 id | teeth | legs | coat_color |    name     | horned | owner 
----+-------+------+------------+-------------+--------+-------
  1 |       |      | palamino   | Snekk       |        |     3
  2 |       |    4 | black      | King George |        |     3
  3 |       |    3 | pinto      | Lambchop    |        |     3
(3 rows)

rnorwood=# INSERT INTO horsies (legs, coat_color, name, owner) VALUES (4, 'Pink', 'Spirit', 4);
INSERT 0 1
rnorwood=# SELECT * FROM horsies;
 id | teeth | legs | coat_color |    name     | horned | owner 
----+-------+------+------------+-------------+--------+-------
  1 |       |      | palamino   | Snekk       |        |     3
  2 |       |    4 | black      | King George |        |     3
  3 |       |    3 | pinto      | Lambchop    |        |     3
  4 |       |    4 | Pink       | Spirit      |        |     4
(4 rows)

rnorwood=# UPDATE horsies SET horned = 'true' WHERE id = 4;
UPDATE 1
rnorwood=# SELECT * FROM horsies;
 id | teeth | legs | coat_color |    name     | horned | owner 
----+-------+------+------------+-------------+--------+-------
  1 |       |      | palamino   | Snekk       |        |     3
  2 |       |    4 | black      | King George |        |     3
  3 |       |    3 | pinto      | Lambchop    |        |     3
  4 |       |    4 | Pink       | Spirit      | t      |     4
(4 rows)

rnorwood=# UPDATE horsies SET horned = 'false' where id != 4;
UPDATE 3
rnorwood=# SELECT * FROM horsies;
 id | teeth | legs | coat_color |    name     | horned | owner 
----+-------+------+------------+-------------+--------+-------
  4 |       |    4 | Pink       | Spirit      | t      |     4
  1 |       |      | palamino   | Snekk       | f      |     3
  2 |       |    4 | black      | King George | f      |     3
  3 |       |    3 | pinto      | Lambchop    | f      |     3
(4 rows)

rnorwood=# SELECT * FROM horsies WHERE owner = 3;
 id | teeth | legs | coat_color |    name     | horned | owner 
----+-------+------+------------+-------------+--------+-------
  1 |       |      | palamino   | Snekk       | f      |     3
  2 |       |    4 | black      | King George | f      |     3
  3 |       |    3 | pinto      | Lambchop    | f      |     3
(3 rows)

rnorwood=# SELECT pd.full_name, h.name, h.coat_color FROM person_data pd, horsie h WHERE h.owner = pd.id;
ERROR:  relation "horsie" does not exist
LINE 1: ...l_name, h.name, h.coat_color FROM person_data pd, horsie h W...
                                                             ^
rnorwood=# SELECT pd.full_name, h.name, h.coat_color FROM person_data pd, horsies h WHERE h.owner = pd.id;
        full_name         |    name     | coat_color 
--------------------------+-------------+------------
 Robin Norwood            | Spirit      | Pink
 George Washington CCCLIV | Snekk       | palamino
 George Washington CCCLIV | King George | black
 George Washington CCCLIV | Lambchop    | pinto
(4 rows)

rnorwood=# ALTER TABLE horsies ALTER column legs SET DEFAULT 4;
ALTER TABLE
rnorwood=# INSERT INTO horsies (coat_color, name, owner) VALUES ('Brown', 'Spirit', 4);
INSERT 0 1
rnorwood=# SELECT * from horsies;
 id | teeth | legs | coat_color |    name     | horned | owner 
----+-------+------+------------+-------------+--------+-------
  4 |       |    4 | Pink       | Spirit      | t      |     4
  1 |       |      | palamino   | Snekk       | f      |     3
  2 |       |    4 | black      | King George | f      |     3
  3 |       |    3 | pinto      | Lambchop    | f      |     3
  5 |       |    4 | Brown      | Spirit      |        |     4
(5 rows)

rnorwood=# ALTER TABLE horsies ALTER column legs NOT NULL;
ERROR:  syntax error at or near "NOT"
LINE 1: ALTER TABLE horsies ALTER column legs NOT NULL;
                                              ^
rnorwood=# ALTER TABLE horsies ALTER column legs ADD CONSTRAINT NOT NULL;
ERROR:  syntax error at or near "ADD"
LINE 1: ALTER TABLE horsies ALTER column legs ADD CONSTRAINT NOT NUL...
                                              ^
rnorwood=# ALTER TABLE horsies ALTER column legs CONSTRAINT NOT NULL;
ERROR:  syntax error at or near "CONSTRAINT"
LINE 1: ALTER TABLE horsies ALTER column legs CONSTRAINT NOT NULL;
                                              ^
rnorwood=# ALTER TABLE horsies ALTER column legs set NOT NULL;
ERROR:  column "legs" contains null values
rnorwood=# UPDATE h.legs FROM horsies h WHERE id = 1^C
(reverse-i-search)`': ^C
rnorwood=# UPDATE h.legs FROM horsies h WHERE id = 1 SET legs = 0;
ERROR:  syntax error at or near "FROM"
LINE 1: UPDATE h.legs FROM horsies h WHERE id = 1 SET legs = 0;
                      ^
rnorwood=# UPDATE horsies SET legs = 0 WHERE id = 1;
UPDATE 1
rnorwood=# select legs from horsies;
 legs 
------
    4
    4
    3
    4
    0
(5 rows)

rnorwood=# ALTER TABLE horsies ALTER column legs set NOT NULL;
ALTER TABLE
rnorwood=# select * from horsies;
 id | teeth | legs | coat_color |    name     | horned | owner 
----+-------+------+------------+-------------+--------+-------
  4 |       |    4 | Pink       | Spirit      | t      |     4
  2 |       |    4 | black      | King George | f      |     3
  3 |       |    3 | pinto      | Lambchop    | f      |     3
  5 |       |    4 | Brown      | Spirit      |        |     4
  1 |       |    0 | palamino   | Snekk       | f      |     3
(5 rows)

rnorwood=# INSERT INTO horsies (coat_color, name, owner) VALUES ('Brown', 'Spirit', 4);
INSERT 0 1
rnorwood=# INSERT INTO horsies (legs, coat_color, name, owner) VALUES (NULL, 'Brown', 'Spirit', 4);
ERROR:  null value in column "legs" violates not-null constraint
DETAIL:  Failing row contains (7, null, null, Brown, Spirit, null, 4).
rnorwood=# \d horsies;
                                  Table "public.horsies"
   Column   |         Type          |                      Modifiers                       
------------+-----------------------+------------------------------------------------------
 id         | integer               | not null default nextval('horsies_id_seq'::regclass)
 teeth      | numeric(3,0)          | 
 legs       | numeric(1,0)          | not null default 4
 coat_color | character varying(32) | 
 name       | character varying(64) | 
 horned     | boolean               | 
 owner      | integer               | 
Indexes:
    "horsies_pkey" PRIMARY KEY, btree (id)
Foreign-key constraints:
    "horsies_owner_fkey" FOREIGN KEY (owner) REFERENCES person_data(id)

rnorwood=# \d horsies;
                                  Table "public.horsies"
   Column   |         Type          |                      Modifiers                       
------------+-----------------------+------------------------------------------------------
 id         | integer               | not null default nextval('horsies_id_seq'::regclass)
 teeth      | numeric(3,0)          | 
 legs       | numeric(1,0)          | not null default 4
 coat_color | character varying(32) | 
 name       | character varying(64) | 
 horned     | boolean               | 
 owner      | integer               | 
Indexes:
    "horsies_pkey" PRIMARY KEY, btree (id)
Foreign-key constraints:
    "horsies_owner_fkey" FOREIGN KEY (owner) REFERENCES person_data(id)

(reverse-i-search)`CREATE': ^CEATE TABLE horsies (id SERIAL PRIMARY KEY, teeth numeric(3), legs numeric(1), coat_color varchar(32), name varchar(64), horned boolean, owner int references person_data(id));
rnorwood=# INSERT INTO horsies (legs, coat_color, name, owner) VALUES (4, 'Brown', 'Broface', 6);
ERROR:  insert or update on table "horsies" violates foreign key constraint "horsies_owner_fkey"
DETAIL:  Key (owner)=(6) is not present in table "person_data".
rnorwood=# select * from person;
ERROR:  relation "person" does not exist
LINE 1: select * from person;
                      ^
rnorwood=# select * from person_data;
 id |        full_name         | best_friend | age | birth_year 
----+--------------------------+-------------+-----+------------
  3 | George Washington CCCLIV | His Horse   |  39 |       1977
  4 | Robin Norwood            | Kyle        |  39 |       1977
(2 rows)

rnorwood=# delete from person_data where id = 4;
ERROR:  update or delete on table "person_data" violates foreign key constraint "horsies_owner_fkey" on table "horsies"
DETAIL:  Key (id)=(4) is still referenced from table "horsies".
rnorwood=# \q

