# Good to know

## Funkce __CrtDumpMemoryLeaks()_

Tato funkce je součástí knihovny Visual C++ Runtime (CRT) a slouží k detekci paměťových úniků v programu, který je vyvíjen v prostředí _Microsoft Visual C++_ / _Microsoft Visual Studio_.

Funkce `_CrtDumpMemoryLeaks()` slouží k nalezení paměťových úniků, což jsou části paměti, které byly dynamicky alokovány během běhu programu, ale nebyly správně uvolněny před ukončením programu. Tato funkce umožňuje programátorovi zobrazit zprávu o paměťových únicích, které byly detekovány během běhu programu, což může být užitečné při ladění a opravování paměťových chyb.

Použití funkce `_CrtDumpMemoryLeaks()` je obvykle součástí procesu ladění a testování aplikace vyvíjené v jazyce C.

### Ukázka použití

```c
#include <iostream>
#include <cstdlib>
#include <crtdbg.h>

void causeMemoryLeak()
{
    // Alokace paměti bez jejího uvolnění
    int* pInt = new int;
    // Neprovádíme uvolnění paměti
    // Paměťový únik
}

int main()
{
    // Zapnutí detekce paměťových úniků
    _CrtSetDbgFlag(_CRTDBG_ALLOC_MEM_DF | _CRTDBG_LEAK_CHECK_DF);

    // Volání funkce, která způsobí paměťový únik
    causeMemoryLeak();

    // Zobrazení zprávy o paměťových únicích (pokud jsou detekovány)
    _CrtDumpMemoryLeaks();

    return 0;
}

```

V tomto příkladu je funkce `_CrtSetDbgFlag()` použita k zapnutí detekce paměťových úniků, a to pomocí flagů `_CRTDBG_ALLOC_MEM_DF` a `_CRTDBG_LEAK_CHECK_DF`. Následně je volána funkce `causeMemoryLeak()`, která alokuje paměť, ale neprovádí její uvolnění, čímž způsobí paměťový únik. Nakonec je volána funkce `_CrtDumpMemoryLeaks()`, která zobrazí zprávu o detekovaných paměťových únicích, pokud jsou nějaké nalezeny.

Je důležité poznamenat, že používání `_CrtDumpMemoryLeaks()` je především pro účely ladění a testování a nemělo by být používáno v produkčním kódu, protože může generovat falešné pozitivy nebo negativy a může mít negativní dopad na výkon aplikace. Je také důležité zajistit, že vývojový kód je správně uvolňuje všechnu alokovanou paměť před ukončením programu, aby se minimalizovaly paměťové úniky.