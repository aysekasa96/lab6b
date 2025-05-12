# Microsoft Fabric Data Warehouse Installatie en Beheer

Dit **README**-bestand beschrijft de stappen voor het maken, bevragen, valideren, opslaan en opruimen van een Data Warehouse in Microsoft Fabric.

## 1. Werkruimte maken
Voordat je met gegevens in Fabric werkt, moet je een werkruimte maken.  
1. Ga naar de Microsoft Fabric-startpagina: [Microsoft Fabric](https://app.fabric.microsoft.com/home?experience=fabric)  
2. Klik op **Workspaces** en maak een **Nieuwe Werkruimte** aan.  
3. Geef de werkruimte een naam en kies een licentiemodus met Fabric-capaciteit (**Trial**, **Premium** of **Fabric**).  
4. Zodra de werkruimte is aangemaakt, is deze leeg en klaar voor gebruik.

## 2. Voorbeeld Data Warehouse maken
Zodra de werkruimte is aangemaakt, kun je een voorbeeldgegevensmagazijn toevoegen.  
1. Klik op **Create**.  
2. Kies **Sample warehouse** onder **Data Warehouse**.  
3. Geef het warehouse de naam **sample-dw**.  
4. Na een korte wachttijd wordt een database gevuld met voorbeeldgegevens voor een taxi-analysescenario.

## 3. Het Data Warehouse bevragen
Gebruik de SQL-query editor om gegevens te analyseren.  
1. Open **sample-dw** en kies **New SQL Query**.  
2. Voer de volgende query uit om maandelijkse gegevens te bekijken:

```sql
SELECT D.MonthName, COUNT(*) AS TotalTrips, SUM(T.TotalAmount) AS TotalRevenue
FROM dbo.Trip AS T 
JOIN dbo.[Date] AS D ON T.[DateID] = D.[DateID]
GROUP BY D.MonthName;

4. Gegevensconsistentie controleren
Controleer op inconsistenties in de gegevens met de volgende queries:

Ritten met onrealistische duur (>24 uur) zoeken

sql
SELECT COUNT(*) FROM dbo.Trip WHERE TripDurationSeconds > 86400;
Negatieve reistijden identificeren en verwijderen

sql
SELECT COUNT(*) FROM dbo.Trip WHERE TripDurationSeconds < 0;

DELETE FROM dbo.Trip WHERE TripDurationSeconds < 0;
5. Query opslaan als een View
Je kunt een filter toepassen en de gegevens opslaan als een view.

Open New SQL Query en voer deze query uit:

sql
SELECT D.DayName, AVG(T.TripDurationSeconds) AS AvgDuration, AVG(T.TripDistanceMiles) AS AvgDistance
FROM dbo.Trip AS T 
JOIN dbo.[Date] AS D ON T.[DateID] = D.[DateID]
WHERE D.Month = 1
GROUP BY D.DayName;
Klik op Save as view en geef de view de naam vw_JanTrip.

6. Resources opruimen
Als je de werkruimte en het warehouse niet meer nodig hebt, kun je ze verwijderen:

Ga naar Workspace settings.

Klik op Remove this workspace en bevestig de verwijdering.
# lab6b
