# Exempel: ett Repository (BookRepository)

Det här exemplet visar Repository-mönstret. Resten av programmet pratar med ett interface, och bara repositoryt vet hur böckerna sparas.

Först interfacet, som beskriver vad som går att göra:

```csharp
public interface IBookRepository
{
    List<Book> GetAll();
    void Add(Book book);
}
```

Reflektion: interfacet säger *vad*, inte *hur*. Ett annat repository, till exempel med MongoDB, kan implementera samma interface utan att resten av koden ändras.

Sedan implementationen med EF Core:

```csharp
public class BookRepository : IBookRepository
{
    private readonly LibraryContext _context;

    public BookRepository(LibraryContext context)
    {
        _context = context;
    }

    public List<Book> GetAll()
    {
        return _context.Books.ToList();
    }
}
```

Reflektion: klassen tar emot sin kontext i konstruktorn. Då kan den bytas ut eller testas utan att skapa en riktig databas.

Och metoden som sparar. Här kan något gå fel, så den behöver felhantering:

```csharp
public void Add(Book book)
{
    _context.Books.Add(book);

    // Tänk på att lägga till Try Catch, databasen kan vara otillgänglig
    _context.SaveChanges();
}
```

## Hela koden

```csharp
public interface IBookRepository
{
    List<Book> GetAll();
    void Add(Book book);
}

public class BookRepository : IBookRepository
{
    private readonly LibraryContext _context;

    public BookRepository(LibraryContext context)
    {
        _context = context;
    }

    public List<Book> GetAll()
    {
        return _context.Books.ToList();
    }

    public void Add(Book book)
    {
        _context.Books.Add(book);

        // Tänk på att lägga till Try Catch, databasen kan vara otillgänglig
        _context.SaveChanges();
    }
}
```
