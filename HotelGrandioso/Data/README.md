# Data

Här ligger databaskopplingen.

- **EF Core:** en `DbContext`-klass och eventuella migrationer. Connectionstring läses från miljövariabel eller en lokal fil som ligger i `.gitignore`, aldrig i koden.
- **MongoDB:** en klass som samlar anslutningen och en klass per collection.
- **Serverdatabas:** starta med Docker eller använd en gratis onlineinstans. Beskriv hur i projektets README.

Ingen ADO.NET. Använd EF Core eller MongoDB.
