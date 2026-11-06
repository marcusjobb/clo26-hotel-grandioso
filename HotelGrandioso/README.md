# HotelGrandioso — kodmappen

Här ligger själva programmet, Hotel Grandioso. Varje mapp har en egen README som beskriver vad som ska ligga där.

| Mapp | Innehåll |
|------|----------|
| `Models/` | Klasser som representerar det ni hanterar (entiteter) |
| `Data/` | Databaskoppling och kontext (EF Core eller MongoDB) |
| `Services/` | Logik som kopplar ihop modeller och data, till exempel Repository |
| `UI/` | Gränssnittet: konsol, Blazor eller MVC |

`Program.cs` är startpunkten. Den ska vara kort och bara koppla ihop delarna.

## Tips

- Lägg varje klass i sin egen fil, med samma namn som klassen.
- Håll namn på svenska i utskrifter och UI, och på engelska i kod (klasser, metoder, variabler).
- Kommentarer på svenska, och förklara varför snarare än vad.
