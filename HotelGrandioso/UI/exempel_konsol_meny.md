# Exempel: en konsolmeny som använder ett repository

Det här exemplet visar hur gränssnittet pratar med repositoryt, och inte med databasen direkt. Texten till användaren är på svenska.

Först kopplas delarna ihop:

```csharp
using var context = new LibraryContext();
IBookRepository repository = new BookRepository(context);
```

Reflektion: gränssnittet känner bara till `IBookRepository`. Det är den raden som bestämmer vilken implementation som används.

Sedan menyn, som visas i en loop tills användaren väljer att avsluta:

```csharp
bool running = true;

while (running)
{
    Console.WriteLine("1. Visa alla böcker");
    Console.WriteLine("2. Lägg till bok");
    Console.WriteLine("0. Avsluta");

    string? choice = Console.ReadLine();

    if (choice == "1")
    {
        foreach (Book book in repository.GetAll())
        {
            Console.WriteLine($"{book.Title} av {book.Author}");
        }
    }
    else if (choice == "2")
    {
        Console.Write("Titel: ");
        string title = Console.ReadLine() ?? "";

        Console.Write("Författare: ");
        string author = Console.ReadLine() ?? "";

        repository.Add(new Book { Title = title, Author = author });
        Console.WriteLine("Boken är tillagd.");
    }
    else if (choice == "0")
    {
        running = false;
    }
    else
    {
        Console.WriteLine("Okänt val, försök igen.");
    }
}
```

Reflektion: menyn sköter bara inmatning och utskrift. Logiken ligger i repositoryt, och klassen `Book` vet ingenting om konsolen.

## Hela koden

```csharp
using var context = new LibraryContext();
IBookRepository repository = new BookRepository(context);

bool running = true;

while (running)
{
    Console.WriteLine("1. Visa alla böcker");
    Console.WriteLine("2. Lägg till bok");
    Console.WriteLine("0. Avsluta");

    string? choice = Console.ReadLine();

    if (choice == "1")
    {
        foreach (Book book in repository.GetAll())
        {
            Console.WriteLine($"{book.Title} av {book.Author}");
        }
    }
    else if (choice == "2")
    {
        Console.Write("Titel: ");
        string title = Console.ReadLine() ?? "";

        Console.Write("Författare: ");
        string author = Console.ReadLine() ?? "";

        repository.Add(new Book { Title = title, Author = author });
        Console.WriteLine("Boken är tillagd.");
    }
    else if (choice == "0")
    {
        running = false;
    }
    else
    {
        Console.WriteLine("Okänt val, försök igen.");
    }
}
```
