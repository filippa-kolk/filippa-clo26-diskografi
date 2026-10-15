# SQL-inlämning — Diskografi

**Namn:** Filippa van der Kolk

**Artist:** Frenna

**Datum:** 14 October 2026

---

 ER-diagram här:
 
<img width="1536" height="927" alt="ERDiscography" src="https://github.com/user-attachments/assets/ea90502a-cec8-40f7-baae-b44dfd221748" />


---

## 1. Skapa databasen — CREATE TABLE

```sql
--- skriv din SQL-kod här ---
CREATE TABLE Artist(
artist_id INTEGER PRIMARY KEY,
name TEXT
);

CREATE TABLE ALbum(
album_id INTEGER PRIMARY KEY,
title TEXT,
release_year INTEGER,
artist_id INTEGER,
FOREIGN KEY (artist_id) REFERENCES Artist(artist_id)
);

CREATE TABLE Song(
song_id INETEGER PRIMARY KEY,
title TEXT,
length_seconds INTEGER,
album_id INTEGER,
FOREIGN KEY (album_id) REFERENECES Album(album_id)
);

CREATE TABLE Genre(
genre_id INTEGER PRIMARY KEY,
name TEXT
);

Kopplingstabell - SongGenre
CREATE TABLE SongGenre(
song_id INTEGER,
genre_id INTEGER,
PRIMARY KEY (song_id, genre_id),
FOREIGN KEY (song_id) REFERENCES Song(song_id),
FOREIGN KEY (genre_id) REFERENCES Genre(genre_id)
);

```

---

## 2. Seeda med data — INSERT

```sql
--- skriv din SQL-kod här ---
INSERT INTO Artist (artist_id, name)
VALUES (1, 'Frenna');

INSERT INTO Album (album_id, title, release_year, artist_id)
VALUES (1, 'Highest', 2021, 1);
INSERT INTO Album (album_id, title, release_year, artist_id)
VALUES (2, 'PINK SUMMER', 2024, 1);
INSERT INTO Album (album_id, title, release_year, artist_id)
VALUES (3, 'bLoOdLine', 2025, 1);

INSERT INTO Song (song_id, title, length_seconds, album_id)
VALUES (1, 'Dragon Roll', 156, 1);
INSERT INTO Song (song_id, title, length_seconds, album_id)
VALUES (2, 'Cant Play Us', 171, 1);
INSERT INTO Song (song_id, title, length_seconds, album_id)
VALUES (3, 'Maandag', 187, 1);
INSERT INTO Song (song_id, title, length_seconds, album_id)
VALUES (4, 'Dichtbij Me', 191, 1);
INSERT INTO Song (song_id, title, length_seconds, album_id)
VALUES (5, 'Guestlist', 234, 1);
INSERT INTO Song (song_id, title, length_seconds, album_id)
VALUES (6, 'PRETTY GIRLS', 145, 2);
INSERT INTO Song (song_id, title, length_seconds, album_id)
VALUES (7, 'MARADONA', 145, 2);
INSERT INTO Song (song_id, title, length_seconds, album_id)
VALUES (8, 'SPONSA', 155, 2);
INSERT INTO Song (song_id, title, length_seconds, album_id)
VALUES (9, 'PICO BELLO', 169, 2);
INSERT INTO Song (song_id, title, length_seconds, album_id)
VALUES (10, 'NIEMAND ANDERS', 184, 2);
INSERT INTO Song (song_id, title, length_seconds, album_id)
VALUES (11, 'MONACO', 137, 3);
INSERT INTO Song (song_id, title, length_seconds, album_id)
VALUES (12, 'picture perfect', 145, 3);
INSERT INTO Song (song_id, title, length_seconds, album_id)
VALUES (13, 'hopi amor', 150, 3);
INSERT INTO Song (song_id, title, length_seconds, album_id)
VALUES (14, 'ZAAZAA', 154, 23;
INSERT INTO Song (song_id, title, length_seconds, album_id)
VALUES (15, 'CHAMPION FLOW', 160, 3);


INSERT INTO Genre (genre_id, name)
VALUES (1, 'Hip Hop');
INSERT INTO Genre (genre_id, name)
VALUES (2, 'Afrobeat');
INSERT INTO Genre (genre_id, name)
VALUES (3, 'R&B');


INSERT INTO SongGenre(song_id, genre_id)
VALUES (1, 1);
INSERT INTO SongGenre(song_id, genre_id)
VALUES (2, 1);
INSERT INTO SongGenre(song_id, genre_id)
VALUES (3, 3);
INSERT INTO SongGenre(song_id, genre_id)
VALUES (4, 3);
INSERT INTO SongGenre(song_id, genre_id)
VALUES (5, 2);
INSERT INTO SongGenre(song_id, genre_id)
VALUES (6, 3);
INSERT INTO SongGenre(song_id, genre_id)
VALUES (7, 1);
INSERT INTO SongGenre(song_id, genre_id)
VALUES (8, 2);
INSERT INTO SongGenre(song_id, genre_id)
VALUES (9, 2);
INSERT INTO SongGenre(song_id, genre_id)
VALUES (10, 3);
INSERT INTO SongGenre(song_id, genre_id)
VALUES (11, 1);
INSERT INTO SongGenre(song_id, genre_id)
VALUES (12, 3);
INSERT INTO SongGenre(song_id, genre_id)
VALUES (13, 3);
INSERT INTO SongGenre(song_id, genre_id)
VALUES (14, 2);
INSERT INTO SongGenre(song_id, genre_id)
VALUES (15, 1);

```

---

## 3. Söka — SELECT

```sql
--- query 1: Lista alla album, sorterade efter år ---
SELECT * FROM Album
ORDER BY release_year;


--- query 2: Lista alla låtar på ett specifikt album ---
SELECT title FROM Song WHERE album_id = 1;


--- query 3: Antal låtar per album ---
SELECT ALbum.title, COUNT(song_id) AS Antal FROM Album
JOIN Song on Album.album_id = Song.album_id
GROUP BY Album.album_id;

--- query 4: Längsta låten ---
SELECT title, length_seconds FROM Song
ORDER BY length_seconds DESC;


--- query 5: Alla låtar sorterade alfabetiskt ---
SELECT title FROM Song
ORDER BY title ASC;

```

---

## 4. Lägg till en ny rad — INSERT

```sql
--- lägg till ett nytt album eller en ny låt ---
INSERT INTO Song (song_id, title, length_seconds, album_id)
VALUES (1, 'picture perfect', 145, 3);

```

---

## 5. Ta bort en rad — DELETE

```sql
--- ta bort en rad ur valfri tabell ---
DELETE FROM SongGenre
WHERE song_id = 15;

```

---

## 6. Uppdatera en rad — UPDATE

```sql
--- uppdatera minst en rad i valfri tabell ---
UPDATE Song
SET length_seconds = 190 WHERE song_id=3;

```

---

## 7. VG-queries (om du siktar på VG)

```sql
--- query 6: Snittlängd på låtar per album ---
SELECT Album.title, AVG(Song.length_seconds) AS Snittlängd FROM Album
JOIN Song on Album-album_id = Song.album_id
GROUP BY Album.album_id;


--- query 7: Albumet med flest låtar ---
SELECT Album.title, COUNT(Song.song_id) AS antal_låtar FROM Album
JOIN Song ON Album.album_id = Song.album_id
GROUP BY Album.album_id
ORDER BY antal_låtar DESC;



--- query 8: Alla låtar längre än 4 minuter (240 sekunder), med albumtitel ---
SELECT Song.title, Song.length_seconds, Album.title AS album FROM Song
JOIN Album ON Song.album_id = Album.album_id
WHERE Song.length_seconds > 240;


```
