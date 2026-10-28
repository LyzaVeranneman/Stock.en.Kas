# Stocktelling hotels

Webapp voor maandelijkse stocktelling per hotel. Hosting: GitHub Pages (pagina) + Supabase (aanmelden en gedeelde opslag).

- Hotels melden aan met e-mail en wachtwoord en zien alleen hun eigen gegevens. Geen Claude-account nodig.
- Editors zien alle hotels, het overzicht "Alle hotels", kunnen maanden afsluiten en importeren. Een afgesloten maand wordt door de server geweigerd voor hotels.
- De regel "product verwijderen enkel bij begin en eind 0" werkt in de pagina, niet op de server.

## Kassa

Bovenaan schakel je tussen **Stocktelling** en **Kassa**. De kassa volgt dezelfde hotels, maanden en rechten:

- Per maand, opgedeeld in weken van maandag tot zondag. Per dag: geteld, FOLS, ticketjes/nota's en reden.
- Per week: totaal = geteld − nota's + overschot vorige week. Afdracht = naar beneden afgerond op € 5. Het overschot schuift door naar de volgende week en maand.
- Afgedragen op, door wie, bedrag naar de bank, en briefjestelling (controle tegen de afdracht, max. 108 briefjes).
- Totaal in huis (kassa + kluis) en nog in kluis. Het saldo van de vorige maand komt automatisch over; in de eerste maand vul je het zelf in.
- Een afgesloten maand is afgesloten voor stock én kassa. "Alle hotels" toont ook kassa geteld en kassa in huis.
- De kassagegevens zitten in dezelfde tabel (`hotel_months`, veld `kassa`), dus er is geen extra SQL nodig.

## Opzetten

1. Maak een gratis project op https://supabase.com.
2. Open **SQL Editor**, plak de inhoud van `schema.sql` en klik **Run**.
3. Ga naar **Authentication > Sign In / Providers** en zet "Allow new users to sign up" **uit**.
4. Ga naar **Authentication > Users > Add user**. Maak een account (e-mail + wachtwoord, vink "Auto Confirm User" aan) voor jezelf, je collega en elk hotel.
5. Maak jezelf en je collega editor, via **SQL Editor**:
   `insert into editors select id from auth.users where email in ('jij@voorbeeld.be','collega@voorbeeld.be');`
6. Ga naar **Project Settings > API**. Kopieer "Project URL" en de "anon public" key naar `config.js`. Gebruik nooit de service_role key.
7. Maak op GitHub een nieuwe repository en upload alle bestanden uit deze map.
8. Ga naar **Settings > Pages**, kies "Deploy from a branch", branch `main`, map `/ (root)`, en klik Save.
9. Na een minuut staat de pagina op `https://GEBRUIKERSNAAM.github.io/REPONAAM/`. Stuur die link naar de hotels, samen met hun aanmeldgegevens.

## Opmerkingen

- Een hotel vult bij de eerste keer de hotelnaam in.
- Een gratis Supabase-project kan na een langere periode zonder gebruik gepauzeerd worden. Je kan het in het dashboard weer starten.
- Maak af en toe een back-up (Supabase > Database > Backups, of exporteer de tabellen).
