# Project from SQL

Projekt z ENGETO datové akademie k získání certifikátu.
Discord name: JakubInIT.

## Zadání:

### Úvod do projektu:
Na vašem analytickém oddělení nezávislé společnosti, která se zabývá životní úrovní občanů, jste se dohodli, že se pokusíte odpovědět na pár definovaných výzkumných otázek, které adresují dostupnost základních potravin široké veřejnosti. Kolegové již vydefinovali základní otázky, na které se pokusí odpovědět a poskytnout tuto informaci tiskovému oddělení. Toto oddělení bude výsledky prezentovat na následující konferenci zaměřené na tuto oblast.
Potřebují k tomu od vás připravit robustní datové podklady, ve kterých bude možné vidět porovnání dostupnosti potravin na základě průměrných příjmů za určité časové období.
Jako dodatečný materiál připravte i tabulku s HDP, GINI koeficientem a populací dalších evropských států ve stejném období, jako primární přehled pro ČR.

### Datové sady, které je možné požít pro získání vhodnéhp datového podkladu:
#### Primární tabulky:
czechia_payroll – Informace o mzdách v různých odvětvích za několikaleté období. Datová sada pochází z Portálu otevřených dat ČR.
czechia_payroll_calculation – Číselník kalkulací v tabulce mezd.
czechia_payroll_industry_branch – Číselník odvětví v tabulce mezd.
czechia_payroll_unit – Číselník jednotek hodnot v tabulce mezd.
czechia_payroll_value_type – Číselník typů hodnot v tabulce mezd.
czechia_price – Informace o cenách vybraných potravin za několikaleté období. Datová sada pochází z Portálu otevřených dat ČR.
czechia_price_category – Číselník kategorií potravin, které se vyskytují v našem přehledu.
#### Číselníky sdílených informací o ČR:
czechia_region – Číselník krajů České republiky dle normy CZ-NUTS 2.
czechia_district – Číselník okresů České republiky dle normy LAU.
#### Dodatečné tabulky:
countries - Všemožné informace o zemích na světě, například hlavní město, měna, národní jídlo nebo průměrná výška populace.
economies - HDP, GINI, daňová zátěž, atd. pro daný stát a rok.

### Výzkumné otázky:
1) Rostou v průběhu let mzdy ve všech odvětvích, nebo v některých klesají?
2) Kolik je možné si koupit litrů mléka a kilogramů chleba za první a poslední srovnatelné období v dostupných datech cen a mezd?
3) Která kategorie potravin zdražuje nejpomaleji (je u ní nejnižší percentuální meziroční nárůst)?
4) Existuje rok, ve kterém byl meziroční nárůst cen potravin výrazně vyšší než růst mezd (větší než 10 %)?
5) Má výška HDP vliv na změny ve mzdách a cenách potravin? Neboli, pokud HDP vzroste výrazněji v jednom roce, projeví se to na cenách potravin či mzdách ve stejném nebo následujícím roce výraznějším růstem?

### Výstupy z projektu:
Pomozte kolegům s daným úkolem. Výstupem by měly být dvě tabulky v databázi, ze kterých se požadovaná data dají získat. Tabulky pojmenujte t_{jmeno}_{prijmeni}_project_SQL_primary_final (pro data mezd a cen potravin za Českou republiku sjednocených na totožné porovnatelné období – společné roky) a t_{jmeno}_{prijmeni}_project_SQL_secondary_final (pro dodatečná data o dalších evropských státech).
Dále připravte sadu SQL, které z vámi připravených tabulek získají datový podklad k odpovězení na vytyčené výzkumné otázky. Pozor, otázky/hypotézy mohou vaše výstupy podporovat i vyvracet! Záleží na tom, co říkají data.
Na svém GitHub účtu vytvořte veřejný repozitář, kam uložíte všechny informace k projektu – hlavně SQL skript generující výslednou tabulku, popis mezivýsledků (průvodní listinu) a informace o výstupních datech (například kde chybí hodnoty apod.).
Neupravujte data v primárních tabulkách! Pokud bude potřeba transformovat hodnoty, dělejte tak až v tabulkách nebo pohledech, které si nově vytváříte.

## Struktura projektu:
- Tabulka cen potravin a mezd pro jednotlivá odvětví - t_jakub_taclik_project_SQL_primary_final
- Tabulka s dodatečnými daty evropských států - t_jakub_taclik_project_SQL_secondary_final
- SQL dotaz na první otázku - SQL_first_task
- SQL dotaz na druhou otázku - SQL_second_task
- SQL dotaz na třetí otázku - SQL_third_task
- SQL dotaz na čtvrtou otázku - SQL_fourth_task
- SQL dotaz na pátou otázku - SQL_fifth_task

## Postup:
### Vytvoření tabulky cen potravin a mezd pro jednotlivá odvětví:
Nejdříve je potřeba pomocí funkce LEFT JOIN spojit tabulku czechia_price přes sloupec category_code s tabulkou czechia_price_category přes sloupec code, kterou si nazvu prices. Spojením těchto dvou tabulek získám především data o názvu a kódu potravin a jejich cen za dané období.
Poté je potřeba pomocí funkce LEFT JOIN spojit tabulku czechia_payroll přes sloupec industry_branch_code s tabulkou czechia_payroll_industry_branch přes sloupec code, kterou si nazvu payrolls. Spojením těchto dvou tabulek získám především data o názvu a kódu odvětví a jejich mezd za dané období. Zároveň si funkcí WHERE vyfiltruji sloupec value_type_code s hodnotou 5958.
Klauzulí SELECT vyberu sloupce category_name, price_value, industry_name, payroll_year a year.
Tabulky prices a payrolls vytvořené pod příkazem WITH spojím pomocí funkce JOIN do jedné společné tabulky přes sloupec year.

### Vytvoření tabulky s dodatečnými daty o dalších evropských státech:
Pomocí příkazu JOIN si spojím tabulky economies a countries přes sloupec country.
Klauzulí SELECT vyberu sloupce country, continent, gdp, gini, population a year.
Funkcí WHERE si vyfiltruju pouze země v Evropě a data pro období od roku 2006 až 2018.

### SQL dotaz na první otázku:

### SQL dotaz na druhou otázku:

### SQL dotaz na třetí otázku:

### SQL dotaz na čtvrtou otázku:

### SQL dotaz na pátou otázku:

## Výsledky:

### 1) Rostou v průběhu let mzdy ve všech odvětvích, nebo v některých klesají?

### 2) Kolik je možné si koupit litrů mléka a kilogramů chleba za první a poslední srovnatelné období v dostupných datech cen a mezd?

### 3) Která kategorie potravin zdražuje nejpomaleji (je u ní nejnižší percentuální meziroční nárůst)?

### 4) Existuje rok, ve kterém byl meziroční nárůst cen potravin výrazně vyšší než růst mezd (větší než 10 %)?

### 5) Má výška HDP vliv na změny ve mzdách a cenách potravin? Neboli, pokud HDP vzroste výrazněji v jednom roce, projeví se to na cenách potravin či mzdách ve stejném nebo následujícím roce výraznějším růstem?
