# Import och moduler

För ett simpelt hej världen program i D behövs `import` satsen.
`import` satsen gör alla publika funktioner samt typer
ifrån den angivna **modulen** tillgängliga.

Standard biblioteket vid namn [Phobos](https://dlang.org/phobos/)
finns under  **paketet** `std`
och dess moduler hänvisas till genom `import std.MODUL`.

`import` satsen kan också användas selektivt
för att importera specifika delar av en modul:

    import std.stdio : writeln, writefln;

Selektiva imports kan också användas för att förbättra läsbarheten
genom att göra det uppenbart varifrån en symbol kommer ifrån,
det är också ett sätt att förhindra konflikter mellan symboler som har
samma namn men inte tillhör samma modul.

En `import` sats behöver inte befinna sig i början av en källfil.
Den kan också användas lokalt inom funktioner eller inom någon
annan omfattning.

## {SourceCode}

```d
void main()
{
    import std.stdio;
    // eller import std.stdio: writeln;
    writeln("Hej Världen!");
}
```
