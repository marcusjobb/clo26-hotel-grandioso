# Exempel: en databaskontext (EF Core)

Det här exemplet visar hur en `DbContext` kopplar klasser till en databas. Det behövs paketet `Microsoft.EntityFrameworkCore.Sqlite` (`dotnet add package Microsoft.EntityFrameworkCore.Sqlite`).

Först en `DbSet` som berättar för EF Core att det finns en tabell med böcker:

```csharp
using Microsoft.EntityFrameworkCore;

public class LibraryContext : DbContext
{
    public DbSet<Book> Books => Set<Book>();
}
```

Reflektion: en `DbSet<Book>` motsvarar en tabell. Varje rad är ett `Book`-objekt.

Sedan konfigurationen. Connectionstring ligger aldrig i koden, utan i en miljövariabel:

```csharp
protected override void OnConfiguring(DbContextOptionsBuilder options)
{
    // Connectionstring hämtas från miljövariabel, aldrig i koden
    string? connectionString = Environment.GetEnvironmentVariable("LIBRARY_DB");

    // Vakt: stanna tidigt om den saknas
    if (string.IsNullOrEmpty(connectionString))
    {
        throw new InvalidOperationException("Miljövariabeln LIBRARY_DB saknas.");
    }

    options.UseSqlite(connectionString);
}
```

Reflektion: felet syns direkt vid start, inte senare när något försöker spara. Värdet kan vara `Data Source=bibliotek.db`.

## Hela koden

```csharp
using Microsoft.EntityFrameworkCore;

public class LibraryContext : DbContext
{
    public DbSet<Book> Books => Set<Book>();

    protected override void OnConfiguring(DbContextOptionsBuilder options)
    {
        // Connectionstring hämtas från miljövariabel, aldrig i koden
        string? connectionString = Environment.GetEnvironmentVariable("LIBRARY_DB");

        // Vakt: stanna tidigt om den saknas
        if (string.IsNullOrEmpty(connectionString))
        {
            throw new InvalidOperationException("Miljövariabeln LIBRARY_DB saknas.");
        }

        options.UseSqlite(connectionString);
    }
}
```
