# Exempel: en modellklass (Book)

Det här exemplet visar hur en modellklass ser ut. Den innehåller data och enkel logik, men vet inget om hur den sparas.

Först en enkel klass med egenskaper:

```csharp
public class Book
{
    public int Id { get; set; }
    public string Title { get; set; } = "";
    public string Author { get; set; } = "";
    public bool IsOnLoan { get; set; }
}
```

Lägg märke till att klassen bara beskriver en bok. Inga anrop till databasen, ingen utskrift.

Logiken om utlåning ligger i klassen, och vakten kommer först:

```csharp
public void Lend()
{
    // Vakt: kontrollera innan vi ändrar något
    if (IsOnLoan)
    {
        throw new InvalidOperationException("Boken är redan utlånad.");
    }

    IsOnLoan = true;
}
```

Reflektion: vakten gör att boken aldrig kan hamna i ett ogiltigt läge. Det är ett exempel på att en klass ansvarar för sina egna regler.

## Hela koden

```csharp
public class Book
{
    public int Id { get; set; }
    public string Title { get; set; } = "";
    public string Author { get; set; } = "";
    public bool IsOnLoan { get; set; }

    public void Lend()
    {
        // Vakt: kontrollera innan vi ändrar något
        if (IsOnLoan)
        {
            throw new InvalidOperationException("Boken är redan utlånad.");
        }

        IsOnLoan = true;
    }
}
```
