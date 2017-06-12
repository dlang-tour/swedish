# Grundläggande typer

D erbjuder ett antal grundläggande typer som alltid har samma
storlek **oavsett** vilken plattform. Det enda undantaget
är typen `real` som erbjuder den högsta möjliga precision för
flyttal. Det finns inga skillnader för heltals storlekarna oavsett
om programmet är kompilerat för ett 32-bitar eller ett 64-bitars system.

| typ                           | storlek
|-------------------------------|------------
|`byte`                         | 8-bit
|`bool`, `ubyte`, `char`        | 8-bit
|`short`, `ushort`, `wchar`     | 16-bit
|`int`, `uint`, `dchar`         | 32-bit
|`long`, `ulong`                | 64-bit

#### Flyttalstyper:

| typ     | storlek
|---------|--------------------------------------------------
|`float`  | 32-bit
|`double` | 64-bit
|`real`   | >= 64-bit (generellt 64-bit, men 80-bit på Intel x86 32-bit)

Prefixet `u` betecknar en *osignerad* typ. `char` översätter till
ett UTF-8 tecken, `wchar` används i UTF-16 strängar och `dchar`
i UTF-32 strängar.

En omvandling mellan variabler av olika typer är endast
tillåtet av kompilatorn om ingen precision går förlorad.
En konvertering mellan flyttalstyper (T.ex. `double` till `float`)
är dock tillåtet.

En omvandling till en annan typ kan framtvingas genom att
använda `cast(TYP) minVar` uttrycket. Det måste dock användas
med stor försiktighet eftersom `cast` uttrycket tillåts bryta typsystemet.

Det speciella nyckelordet `auto` skapar en variabel och antyder dess typ
från höger sida av uttrycket. `auto minVar = 7` kommer att härleda typen
`int` för `minVar`. Notera att typen fortfarande är satt vid kompilering och
kan inte ändras, precis som med andra variabler med en uttryckligen
angiven typ.

### Typegenskaper

Alla datatyper har en egenskap `.init` som de initialiseras till. För alla
heltal är detta `0` och för flyttal är det `nan` (*not a number*, "Inte ett tal").

Heltalstyper och flyttalstyper har en `.max` egenskap för det högsta värdet
de kan representera. Heltalstyperna har också en `.min` egenskap för det
lägsta värdet de kan representera medan flyttalstyper har en `.min_normal`
egenskap som defineras till det minsta representativa normaliserade värdet
som inte är 0.

Flyttalstyper har också en egenskaperna `.nan` (NaN-värde), `.infinity`
(oändlighetens värde), `.dig` (antal decimaler i precisionen), `.mant_dig`
(antalet bitar i mantissa) och mer.

Varje typ har också en `.stringof` egenskap som ger sitt namn som en
sträng.

### size_t

I D har index oftast alias typen `size_t`, eftersom det är en typ som är
tillräckligt stor för att representera en förskjutning i alla adresserbara
minnen, `uint` för 32-bitars och `ulong` för 64-bitarsarkitekturer.

### Fördjupning
**NOTERA:** Följande länkar är på engelska

#### Grundläggande referenser

- [Tilldelning](http://ddili.org/ders/d.en/assignment.html)
- [Variabler](http://ddili.org/ders/d.en/variables.html)
- [Aritmetik](http://ddili.org/ders/d.en/arithmetic.html)
- [Flyttal](http://ddili.org/ders/d.en/floating_point.html)
- [Grundläggande typer i _Programmering i D_](http://ddili.org/ders/d.en/types.html)

#### Avancerade referenser

- [Översikt över alla grundläggande datatyper i D](https://dlang.org/spec/type.html)
- [`auto` och `typeof` i _Programmering i D_](http://ddili.org/ders/d.en/auto_and_typeof.html)
- [Typegenskaper](https://dlang.org/spec/property.html)
- [Assert uttrycket](https://dlang.org/spec/expression.html#AssertExpression)

## {SourceCode}

```d
import std.stdio;

void main()
{
    // Stora tal kan separeras
    // med ett understreck "_"
    // för att förbättra läsbarheten.
    int b = 7_000_000;
    short c = cast(short) b; // cast nödvändig
    uint d = b; // går bra pga större typ
    int g;
    assert(g == 0);

    auto f = 3.1415f; // f betecknar float

    // typeid(VAR) returnerar
    // typinformationen av ett uttryck.
    writeln("type of f is ", typeid(f));
    double pi = f; // går bra pga större typ
    // för flyttalstyper tillåtet med
    // implicit down-casting
    float demoted = pi;

    // tillgång till typegenskaper
    assert(int.init == 0);
    assert(int.sizeof == 4);
    assert(bool.max == 1);
    writeln(int.min, " ", int.max);
    writeln(int.stringof); // int
}
```
