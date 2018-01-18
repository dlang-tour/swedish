# Minneshantering

D är ett systemprogrammeringsspråk och tillåter därför manuell
hantering av minnet. Med det sagt är manuell minneshantering en källa
till många fel, så D använder sig av en *skräpsamlare* (garbage collector) som
standardmetod för att hantera minnestilldelningar.

D erbjuder pekartyper `T*` likt som i programmeringsspråket C:

    int a;
    int* b = &a; // b innehåller adressen till a
    auto c = &a; // c är int* och innehåller adressen till a

Ett nytt minnesblock på heapen kan allokeras med uttrycket `new`
som returnerar en pekare till det allokerade minnet.

    int* a = new int;

Så fort minnet adresserat av `a` inte länge hänvisas till av någon variabel
i programmet, frigörs minnet av skräpsamlaren.

Det finns tre säkerhetsnivåer för funktioner i D: `@system`, `@trusted` och `@safe`. Om inget annat anges är `@system` standard. `@safe` är en delmängd av D som förhindrar minnesfel genom att förbjuda vissa operationer. `@safe` kod kan endast anropa andra `@safe` eller `@trusted` funktioner. Vidare är manuell pekararitmetik förbjuden i `@safe` kod:

    void main() @safe {
        int a = 5;
        int* p = &a;
        int* c = p + 5; // Fel
    }

`@trusted` funktioner måste verifieras manuellt av programmeraren och gör det möjligt att skapa en koppling mellan SafeD och den underliggande osäkra lågnivådelen av D-program.

### Fördjupning
**NOTERA:** Följande länkar är på engelska

* [SafeD](https://dlang.org/safed.html)

## {SourceCode}

```d
import std.stdio : writeln;

void safeFun() @safe
{
    writeln("Hej Världen!");
    // Allokering av minne med GC är säkert
    int* p = new int;
}

void unsafeFun()
{
    int* p = new int;
    int* fiddling = p + 5;
}

void main()
{
    safeFun();
    unsafeFun();
}
```