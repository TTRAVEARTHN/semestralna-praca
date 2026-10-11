# semestralna-praca
## MAXPC

Maksym Zadorozhnii

5ZYI33

### Stručný opis projektu

Cieľom projektu je návrh a vytvorenie webovej aplikácie na prezentáciu a predaj hotových počítačov a počítačového príslušenstva. Aplikácia rieši potrebu používateľov mať jednoduchý a prehľadný spôsob, ako si prezrieť dostupné počítačové zostavy, porovnať ich parametre a získať všetky informácie o produktoch na jednom mieste.

Aplikácia je určená zákazníkom, ktorí si chcú vybrať a objednať herný alebo pracovný počítač, resp. periférie. Zároveň pôsobí profesionálne a buduje dôveru zákazníkov prostredníctvom marketingových informácií o firme (prednosti, recenzie, počet predaných počítačov). Dôraz je kladený na prehľadnosť, rýchlu orientáciu a estetický, funkčný dizajn.

### Role v projekte

- **Návštevník (neprihlásený používateľ)** – môže prehliadať produkty a kategórie, filtrovať a triediť ich, porovnávať produkty podľa parametrov a zobraziť detail produktu. Pri pokuse o „Pridať do košíka“ sa zobrazí upozornenie, že sa musí prihlásiť alebo zaregistrovať.
- **Zákazník (prihlásený používateľ)** – má všetky oprávnenia návštevníka a navyše môže pridávať produkty do košíka, vytvárať objednávky, zobraziť históriu objednávok, upravovať svoj profil a označovať produkty ako obľúbené.
- **Administrátor (ADMIN)** – má plnú kontrolu nad obsahom a používateľmi systému cez samostatné administrátorské rozhranie dostupné len pre rolu admin. Zodpovedá za správu produktov, kategórií, používateľov, objednávok a marketingových recenzií a sleduje štatistiky predaja.

### Prípady použitia podľa rolí

**Návštevník**

- prehliada produkty a kategórie (herné PC, pracovné PC, periférie),
- filtruje a triedi produkty podľa ceny, výkonu a značky,
- porovná produkty podľa parametrov (CPU, GPU, RAM, cena),
- zobrazí detail produktu (popis, fotografie, špecifikácie),
- zaregistruje sa a prihlási do systému.

**Zákazník**

- pridá produkt do košíka a upraví jeho množstvo,
- vytvorí objednávku z obsahu košíka,
- zobrazí históriu svojich objednávok,
- upraví svoj profil (meno, e-mail, heslo, adresa),
- označí produkt ako obľúbený.

**Administrátor**

- pridá, upraví alebo zmaže produkt,
- spravuje kategórie produktov,
- zablokuje, zmaže alebo upraví účet používateľa,
- zobrazí detail objednávky a zmení jej stav,
- pridá alebo upraví marketingovú recenziu,
- zobrazí štatistiky predaja.

### Plánované entity

- **User** – používateľ systému. Atribúty: id, name, email, password, address, role (user/admin), created_at, updated_at. Vzťahy: má jeden košík, viac objednávok a viac obľúbených produktov.
- **Category** – logické rozdelenie produktov (herné PC, pracovné PC, periférie). Atribúty: id, name, description. Vzťah: obsahuje viac produktov.
- **Product** – informácie o produkte. Atribúty: id, category_id, name, description, price, specs, main_image, created_at, updated_at. Vzťahy: patrí do jednej kategórie, má viac obrázkov, môže byť v košíkoch, objednávkach a obľúbených.
- **ProductImage** – doplnkové fotografie produktu. Atribúty: id, product_id, image_path.
- **Cart** – nákupný košík používateľa. Atribúty: id, user_id, created_at. Vzťah: patrí jednému používateľovi a obsahuje viac položiek.
- **CartItem** – položka v košíku. Atribúty: id, cart_id, product_id, quantity.
- **Order** – objednávka vytvorená po potvrdení košíka. Atribúty: id, user_id, total_price, status, created_at, updated_at. Vzťah: patrí jednému používateľovi a obsahuje viac položiek.
- **OrderItem** – položka objednávky. Atribúty: id, order_id, product_id, quantity, price (cena v čase objednávky).
- **Favorite** – prepojenie používateľa a obľúbeného produktu. Atribúty: id, user_id, product_id.
- **Review** – marketingová recenzia pridaná administrátorom. Atribúty: id, author_name, text, image_path, created_at.

### Vzťahy medzi entitami

- User – Cart: 1:1 (každý používateľ má jeden aktívny košík).
- Cart – CartItem: 1:N (košík obsahuje viac položiek).
- User – Order: 1:N (používateľ môže vytvoriť viac objednávok).
- Order – OrderItem: 1:N (objednávka obsahuje viac položiek).
- Category – Product: 1:N, resp. Product – Category: N:1 (každý produkt patrí do jednej kategórie).
- Product – ProductImage: 1:N (produkt môže mať viac obrázkov).
- Product – OrderItem: 1:N (produkt môže byť súčasťou viacerých objednávok).
- Product – CartItem: 1:N (produkt môže byť v rôznych košíkoch).
- User – Product (Favorite): M:N, realizované cez tabuľku favorites.
- Review je samostatná entita bez väzby na ostatné tabuľky.

### Hlavné stránky aplikácie

1. **Home page** – úvodná stránka s hlavným bannerom „Build Your Dream PC“, tlačidlom na katalóg a marketingovými údajmi (počet predaných PC, spokojnosť zákazníkov, roky na trhu, hodnotenie), príp. recenziami.
2. **Catalog page** – katalóg produktov v kartách (obrázok, kategória, CPU/GPU/RAM, cena) s filtrovaním a triedením a tlačidlami Details, Add to Cart, obľúbené a porovnať.
3. **Detail produktu** – popis, galéria fotografií, kompletné špecifikácie a možnosť pridať do košíka.
4. **Cart page** – zoznam položiek, zmena množstva, rekapitulácia objednávky (medzisúčet, daň, doprava, spolu) a pokračovanie k objednávke alebo prihláseniu.
5. **Compare page** – porovnanie až 4 produktov vedľa seba (cena, kategória, značka, procesor, grafika, pamäť).
6. **Log In / Sign Up** – prihlásenie a registrácia používateľa.
7. **Účet používateľa** – úprava profilu, história objednávok a obľúbené produkty.
8. **Administrátorské rozhranie** – správa produktov, kategórií, používateľov, objednávok, recenzií a štatistiky predaja.

### Rozdelenie funkcionality

**Základné funkcie**

- registrácia, prihlásenie a odhlásenie (šifrované heslá),
- rozdelenie rolí user/admin a ochrana administrátorského rozhrania,
- prehliadanie kategórií a produktov, detail produktu,
- filtrovanie a triedenie produktov,
- nákupný košík a vytvorenie objednávky,
- história objednávok a úprava profilu,
- administrátorská správa produktov, kategórií a objednávok (zmena stavu).

**Rozširujúce funkcie**

- porovnávanie produktov podľa parametrov,
- obľúbené produkty,
- galéria viacerých obrázkov produktu,
- marketingové recenzie spravované administrátorom,
- administrátorská správa používateľov (blokovanie, mazanie),
- štatistiky predaja,
- dynamické načítanie a filtrovanie pomocou JavaScriptu,
- plná responzivita pre počítače, tablety a mobily.