# Reflektion — Inlämning 1

**Namn:** Filippa van der Kolk

**Datum:** 15 October 2026

---

## Vad var svårast?

Det svaraste var att hålla koll på relationerna mellan tabellerna, särskilt hur Song kopplas till Album och Album till Artist. I början kändes det förvirrande att en låt inte har en direkt koppling till artisten, utan att man måste gå via albumet. När jag sedan skulle gå vidare till min kopplingstabell häll jag på att tappa det haha. Då var det bara siffror pga av song_id och genre_id och då var det svårt att hålla koll på vad som va vad.
Det var även lite klurigt att förstå när JOIN, GROUP BY och ORDER BY skulle användas tillsammans.
Jag tyckte också att det var svårt när man fick felmeddelanden då dessa var svårare att läsa och förstå i gjämförelse med Visual Studio.

---

## Vad lärde du dig?

Jag lärde mig hur viktigt det är att ha en tydlig och logisk databasstruktur innan man börjar skriva SQL-frågor. När tabellerna är rätt designade blir frågarna mycket enklare. Jag lärde mig också hur JOIN fungerar i praktiken och att SQL är väldigt strikt - små detaljer som kommatecken eller fel ordning kan göra att hela kommandot faller.

---

## Hur använde du SQL i praktiken — vad kändes naturligt och vad var förvirrande?

Det som kändes mest naturligt var att skriva SELECT frågor. Det känns mest tydligt och logiskt: du väljer kolumner, tabell och eventuell sortering. Och det som var mest förvirrande i början var JOIN. Jag behövde tänka igenom relationerna för att förstå varför vissa tabeller måste kopplas ihop för att få fram rätt data. UPDATE och DELETE kändes också lite ovant, men när jag förstod strukturen (UPDATE --> SET --> WHERE) blev det mycket enklare!

---

## Om du hade mer tid — vad hade du lagt till eller gjort annorlunda?

Om jag hade mer tid hade jag lagt till fler genrer och fler kopplingar i SongGenre för att se hur databasen med ännu mer N:M data.
Jag hade också velat lägga till fler artister. Vissa låtar har fler än Frenna som artist, och då hade det vara roligt att skapa en ArtistSong-kopplingstabell fär att hantera medverkande artister. Det hade gjort min databas ännu mer realtiskts och skapat möjligheten att lägga till de medverkande artisternas egna diskografi.
Det hade även varit kul att bygga ett litet C#-program som läser från databasen för att se hur SQL fungerar ihop med kod och hur man kan presentera datan i ett riktigt program.

---

## (VG) Varför valde du just den här tabellstrukturen?

Resonera kring ditt designval: Vad hade hänt om du löst det på ett annat sätt? Vilka för- och nackdelar ser du med din lösning jämfört med ett alternativ?

Jag valde denna strukturen eftersom den följer 3NF och gör databasen flexibel, tydlig och enkla att jobba inom.

Jag har två stycken 1:N-relationer. Artist --> Album och Album --> Song.
En artist kan ha flera album, ett album kan ha flera låtar. Det är en naturlig relation som speglar verkligheten och undviker duplicering av data.

Sedan har jag en N:M-relation. Genre och SongGenre.
En låt kan ha flera genrer och en genre kan användas av flera låtar (för enkelhetensskull hade jag i databasen bara en genre per låt). Härmed behövs en kopplingstabell.
Det gör databasen mer skalbar och man kan undvika att lägga flera genrer i samma kolumn.

