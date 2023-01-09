### CREATE A TABLE

This project further helped me to get familiarized with the basic SQL commands by creating a list of movies. For this exercise, I also generated the corresponding sql file on the postgresql software called "Movies_DB_Queries.sql".

- First, create a movies table.
  
  ```
  CREATE TABLE IF NOT EXISTS movies (id INTEGER, name TEXT);
  SELECT * FROM movies;
  ```

- Add columns. 
  
  ```
  ALTER TABLE movies ADD COLUMN producer TEXT;
  ALTER TABLE movies ADD COLUMN release_year TEXT;
  ```

- Add movies.
  
  ```
  INSERT INTO movies (id, name, producer, release_year) VALUES (1, 'Dynasty Warriors', 'Netflix', '2021'); 
  
  INSERT INTO movies (id, name, producer, release_year) 
  VALUES (2, 'A Beautiful Mind', ' Universal Pictures; Dreamworks Pictures; Imagine Entertainment', '2001');
  ```

- Change table name.
  
  ```
  ALTER TABLE movies RENAME TO films;
  ```

- Change column name.
  
  ```
  ALTER TABLE films
  RENAME COLUMN producer TO production;
  
  INSERT INTO films (id, name, production, release_year) 
  VALUES (3, 'The Immitation Game', 'The Weinstein Company, Black Bear Pictures, Bristol Automotive', '2014');
  ```

- Add more entries.
  
  ```
  INSERT INTO films (id, name, production, release_year) 
  VALUES (4, 'A Walk to Remember', 'Di Novi Pictures, Gaylord Films, Pandora Cinema', '2002');
  
  INSERT INTO films (id, name, production, release_year) 
  VALUES (5, 'Sweet November', 'Bel Air Entertainment', '2001');
  
  INSERT INTO films (id, name, production, release_year) 
  VALUES (6, 'Charlie and the Chocolate Factory', 'The Zanuck Company, Plan B Entertainment, Village Roadshow Pictures, Theobald Film Productions', '2004');
  
  INSERT INTO films (id, name, production, release_year) 
  VALUES (7, 'Real Steel', 'DreamWorks Pictures, Reliance Entertainment, 21 Laps Entertainment, ImageMovers, Montford Murphy Productions', '2011');
  
  INSERT INTO films (id, name, production, release_year) 
  VALUES (8, 'A.I. Artifical Intelligence', 'Amblin Entertainment, Stanley Kubrick Productions', '2001');
  
  INSERT INTO films (id, name, production, release_year) 
  VALUES (9, 'The Sixth Sense', 'Hollywood Pictures, Spyglass Entertainment, The Kennedy/Marshall Company, Barry Mendel Productions', '1999');
  
  INSERT INTO films (id, name, production, release_year) 
  VALUES (10,'Unbreakable', 'Touchstone Pictures, Blinding Edge Pictures, Barry Mendel Productions, Limited Edition Productions Inc.', '2000');
  ```

- Check all entries.
  
  ```
  SELECT * FROM films;
  ```

- Change release_year column data type.
  
  ```
  ALTER TABLE films ALTER COLUMN release_year TYPE INT
  USING release_year::INTEGER;
  ```

- Filter entries.
  
  ```
  SELECT * FROM films WHERE release_year<=2003;
  ```

- Add constrain to a column attribute.
  
  ```
  ALTER TABLE films
  ADD CONSTRAINT unique_id UNIQUE (id);
  ```

- Try adding a new entry with an existing id.
  
  ```
  INSERT INTO films (id, name, production, release_year) 
  VALUES (10, 'Titanic', 'Paramount Pictures, 20th Century Fox, Lightstorm Entertainment', '1997');
  --Got an error message: ERROR:  duplicate key value violates unique constraint "unique_id"
  ```

- Add the same entry with a different id
  
  ```
  INSERT INTO films (id, name, production, release_year) 
  VALUES (11, 'Titanic', 'Paramount Pictures, 20th Century Fox, Lightstorm Entertainment', '1997');
  ```

- Delete id=11
  
  ```
  DELETE FROM films WHERE id=11;
  ```

- Add new columns
  
  ```
  ALTER TABLE films ADD COLUMN imdb_rating DECIMAL;
  ```

- Update rating for a series of rows only within id=1 thru 4
  
  ```
  UPDATE films 
  SET imdb_rating = CASE id
  WHEN 1 THEN 4.8
  WHEN 2 THEN 8.2 
  WHEN 3 THEN 8
  WHEN 4 THEN 7.5
  END WHERE id IN(1,2,3,4);
  ```

- update only one rating
  
  ```
  UPDATE films SET imdb_rating = 6.7 WHERE id = 5;
  ```

- Update the rest of the ratings only within id=6 thru 10
  
  ```
  UPDATE films 
  SET imdb_rating = CASE id
  WHEN 6 THEN 6.7
  WHEN 7 THEN 7 
  WHEN 8 THEN 7.2
  WHEN 9 THEN 8.2
  WHEN 10 THEN 7.3
  END WHERE id IN(6,7,8,9,10);
  ```

- Check all entries
  
  ```
  SELECT * FROM films;
  ```