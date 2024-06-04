# DB Videogames Query

Dato il DB, esegui le seguenti query: 

## SELECT
- Selezionare tutte le software house americane (3)

`SELECT * FROM software_houses WHERE country = "United States";`

- Selezionare tutti i giocatori della città di 'Rogahnland' (2)

`SELECT * FROM players WHERE city = "Rogahnland";`

- Selezionare tutti i giocatori il cui nome finisce per "a" (220)

`SELECT * FROM players WHERE name LIKE "%a";`

- Selezionare tutte le recensioni scritte dal giocatore con ID = 800 (11)

`SELECT * FROM reviews WHERE player_id = 800;`

- Contare quanti tornei ci sono stati nell'anno 2015 (9)

`SELECT COUNT(*) as tournaments FROM tournaments WHERE year = 2015;`

- Selezionare tutti i premi che contengono nella descrizione la parola 'facere' (2)

`SELECT * FROM awards WHERE description LIKE "%facere%";`

- Selezionare tutti i videogame che hanno la categoria 2 (FPS) o 6 (RPG), mostrandoli una sola volta (del videogioco vogliamo solo l'ID) (287)

SELECT videogames.id FROM videogames  
INNER JOIN category_videogame ON category_videogame.videogame_id = videogames.id  
INNER JOIN categories ON categories.id = category_videogame.category_id  
WHERE categories.id IN (2, 6)  
GROUP BY videogames.id;  

- Selezionare tutte le recensioni con voto compreso tra 2 e 4 (2947)

`SELECT * FROM reviews WHERE rating BETWEEN 2 AND 4;`

- Selezionare tutti i dati dei videogiochi rilasciati nell'anno 2020 (46)

`SELECT * FROM videogames WHERE YEAR(release_date) = 2020;`

- Selezionare gli id dei videogame che hanno ricevuto almeno una recensione da 5 stelle, mostrandoli una sola volta (443)

`SELECT videogames.id FROM videogames INNER JOIN reviews on reviews.videogame_id = videogames.id WHERE rating = 5 GROUP BY videogames.id;`

### BONUS

- Selezionare il numero e la media delle recensioni per il videogioco con ID = 412 (review number = 12, avg_rating = 3.16 circa) 

`SELECT COUNT(*) as review_number, AVG(rating) as avg_rating FROM reviews WHERE videogame_id = 412;`

- Selezionare il numero di videogame che la software house con ID = 1 ha rilasciato nel 2018 (13)

`SELECT COUNT(*) FROM videogames WHERE software_house_id = 1 AND YEAR(release_date) = 2018;`

## GROUP BY
- Contare quante software house ci sono per ogni paese (3)

`SELECT country, COUNT(*) FROM software_houses GROUP BY country;`

- Contare quante recensioni ha ricevuto ogni videogioco (del videogioco vogliamo solo l'ID) (500)

`SELECT videogames.id, COUNT(*) FROM reviews INNER JOIN videogames ON reviews.videogame_id = videogames.id GROUP BY videogames.id;`

- Contare quanti videogiochi hanno ciascuna classificazione PEGI (della classificazione PEGI vogliamo solo l'ID) (13)

`SELECT categories.id, COUNT(*) FROM category_videogame INNER JOIN categories ON category_videogame.category_id = categories.id GROUP BY categories.id;`

- Mostrare il numero di videogiochi rilasciati ogni anno (11)

`SELECT YEAR(release_date), COUNT(*) FROM videogames GROUP BY YEAR(release_date);`

- Contare quanti videogiochi sono disponbiili per ciascun device (del device vogliamo solo l'ID) (7)

`SELECT devices.id FROM device_videogame INNER JOIN devices ON device_videogame.device_id = devices.id GROUP BY devices.id;`

- Ordinare i videogame in base alla media delle recensioni (del videogioco vogliamo solo l'ID) (500)

`SELECT videogames.id, AVG(rating) FROM reviews INNER JOIN videogames ON reviews.videogame_id = videogames.id GROUP BY videogames.id ORDER BY AVG(rating) DESC;`

## JOIN
- Selezionare i dati di tutti giocatori che hanno scritto almeno una recensione, mostrandoli una sola volta (996)

`SELECT DISTINCT players.* FROM players INNER JOIN reviews ON players.id = reviews.player_id;`


- Sezionare tutti i videogame dei tornei tenuti nel 2016, mostrandoli una sola volta (226)

`SELECT DISTINCT videogames.* FROM videogames INNER JOIN tournament_videogame ON tournament_videogame.videogame_id = videogames.id INNER JOIN tournaments ON tournaments.id = tournament_videogame.tournament_id WHERE tournaments.year = 2016;`

- Mostrare le categorie di ogni videogioco (1718)

`SELECT videogames.id AS videogame_id, categories.* FROM videogames INNER JOIN category_videogame ON category_videogame.videogame_id = videogames.id INNER JOIN categories ON categories.id = category_videogame.category_id;`

- Selezionare i dati di tutte le software house che hanno rilasciato almeno un gioco dopo il 2020, mostrandoli una sola volta (6)

`SELECT DISTINCT software_houses.* FROM software_houses INNER JOIN videogames ON videogames.software_house_id = software_houses.id WHERE YEAR(videogames.release_date) > 2020;`

- Selezionare i premi ricevuti da ogni software house per i videogiochi che ha prodotto (55)

`SELECT awards.* FROM awards INNER JOIN award_videogame ON award_videogame.award_id = awards.id INNER JOIN videogames ON videogames.id = award_videogame.videogame_id;`

- Selezionare categorie e classificazioni PEGI dei videogiochi che hanno ricevuto recensioni da 4 e 5 stelle, mostrandole una sola volta (3363)

- Selezionare quali giochi erano presenti nei tornei nei quali hanno partecipato i giocatori il cui nome inizia per 'S' (474)

`SELECT DISTINCT videogames.* FROM videogames INNER JOIN tournament_videogame ON tournament_videogame.videogame_id = videogames.id INNER JOIN tournaments ON tournaments.id = tournament_videogame.tournament_id INNER JOIN player_tournament ON player_tournament.tournament_id = tournaments.id INNER JOIN players ON players.id = player_tournament.player_id WHERE players.name LIKE 'S%';`

- Selezionare le città in cui è stato giocato il gioco dell'anno del 2018 (36)



- Selezionare i giocatori che hanno giocato al gioco più atteso del 2018 in un torneo del 2019 (991)



### BONUS

- Selezionare i dati della prima software house che ha rilasciato un gioco, assieme ai dati del gioco stesso (software house id : 5)

- Selezionare i dati del videogame (id, name, release_date, totale recensioni) con più recensioni (videogame id : potrebbe uscire 449 o 398, sono entrambi a 20)

- Selezionare la software house che ha vinto più premi tra il 2015 e il 2016 (software house id : potrebbe uscire 3 o 1, sono entrambi a 3)

- Selezionare le categorie dei videogame i quali hanno una media recensioni inferiore a 2 (10)
