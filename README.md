# perra the dog — landing

Landing dla psiej behawiorystki z sekcjami: hero, usługi, formularz zgłoszeniowy (Google Forms), social media.

## Jak uruchomić

Otwórz plik `index.html` w przeglądarce (np. dwuklik) lub uruchom lokalny serwer:

```bash
# Python 3
python3 -m http.server 8000

# lub npx
npx serve .
```

Wejdź na: http://localhost:8000

## Konfiguracja — config.json

Wszystko sterowane jest z pliku **config.json**: kolejność i widoczność sekcji, linki do formularzy, social media i dane w stopce.

### Sekcje (kolejność i widoczność)

W `sections` ustawiasz dla każdej sekcji:
- **id** — identyfikator (hero, uslugi, galeria, opinie, formularz-zgloszeniowy, kontakt)
- **visible** — `true` / `false` (czy sekcja ma być widoczna)
- **order** — liczba (kolejność na stronie; mniejsza = wyżej)
- **label** — tekst w menu i w nawigacji kropkowej

Przykład: żeby ukryć Galerię i dać Opinie przed Usługami:
```json
"sections": [
  { "id": "hero", "visible": true, "order": 0, "label": "Start" },
  { "id": "opinie", "visible": true, "order": 1, "label": "Opinie" },
  { "id": "uslugi", "visible": true, "order": 2, "label": "Usługi" },
  { "id": "galeria", "visible": false, "order": 3, "label": "Galeria" },
  ...
]
```

### Formularze, social media, stopka

- **forms** — tablica `{ "title", "description", "url" }` (np. linki do Google Forms)
- **socials** — tablica `{ "name", "url", "icon": "instagram" | "facebook" }`
- **footer** — `{ "email", "phoneHref", "phoneDisplay" }` (phoneHref bez spacji, np. +48123456789)

Linki i dane kontaktowe edytujesz wyłącznie w **config.json**. Przy otwarciu strony z dysku (file://) używany jest wbudowany domyślny config (placeholdery).

## Przełącznik koloru akcentu

W menu (nav) jest przełącznik **Czarny / Miętowy**. Odwiedzający może wybrać kolor akcentu (czarny lub miętowy); wybór jest zapisywany w przeglądarce (localStorage) i zostaje po odświeżeniu strony. Strona ma jasne, bezowe tło.

## Usługi z pliku JSON

Sekcja „Usługi” jest ładowana z pliku **services.json** (w tym samym folderze co `index.html`). Możesz edytować ten plik, aby zmieniać, dodawać lub usuwać pozycje.

Format każdej usługi:

- `num` — numer (np. `"01"`); opcjonalny (domyślnie 01, 02, …)
- `title` — tytuł karty
- `description` — krótki opis (możesz też użyć pola `desc`)

Przykład jednej pozycji:

```json
{
  "num": "01",
  "title": "Konsultacja behawioralna",
  "description": "Spotkanie diagnostyczne, analiza zachowań i indywidualny plan pracy."
}
```

Jeśli `services.json` nie istnieje lub jest nieprawidłowy, wyświetlą się domyślne usługi wbudowane w stronę.

## Galeria zdjęć

Sekcja **Galeria** pokazuje boxy ze zdjęciami. Lista zdjęć jest w pliku **gallery.json**.

Format każdej pozycji:

- `src` — ścieżka do zdjęcia (np. `images/foto1.jpg`) lub pełny URL
- `alt` — krótki opis (opcjonalny, wyświetla się po najechaniu)

Przykład **gallery.json**:

```json
[
  { "src": "images/foto1.jpg", "alt": "Spacer z psem" },
  { "src": "images/foto2.jpg", "alt": "Konsultacja" }
]
```

Zdjęcia wstaw do folderu **images/** (np. `images/foto1.jpg`). Jeśli nie ma `gallery.json` albo strona jest otwarta z dysku (file://), pokażą się zdjęcia zastępcze z internetu.

## Opinie (testimoniale)

Sekcja **Opinie** pokazuje cytaty od klientów. Lista jest w pliku **testimonials.json**.

Format każdej opinii:

- `quote` — treść wypowiedzi
- `author` — imię (i inicjał) lub pseudonim
- `context` — opcjonalnie: np. „opieka nad Borysem”, „uczestnik warsztatów”

Przykład **testimonials.json**:

```json
[
  {
    "quote": "Po kilku spotkaniach nasz pies w końcu przestał ciągnąć na smyczy. Polecam.",
    "author": "Anna K.",
    "context": "opieka nad Borysem, border collie"
  }
]
```

Wszystkie opinie bierz z **testimonials.json**. Przy błędzie ładowania pojawi się komunikat „Brak danych”.

---

## Co zostało poprawione / dodane (analiza kodu)

- **SEO**: meta description, Open Graph (og:title, og:description, og:type) — lepsze podglądy w Google i przy udostępnianiu linku.
- **Favicon**: tymczasowa ikona (emoji 🐕) w SVG; możesz ją zastąpić plikiem `favicon.ico` w głównym folderze i zmienić `<link rel="icon">` w `index.html`.
- **Dostępność**: link „Przejdź do treści” (widoczny po Tab na początku strony), wyraźne obrysy `:focus-visible` dla linków i przycisków (nawigacja klawiaturą).
- **Redukcja ruchu**: przy ustawieniu systemowym „reduce motion” animacje są ograniczone (m.in. sekcje, scroll hint).
- **Wydajność**: obsługa scrollu przy kropkach nawigacji używa `requestAnimationFrame`, żeby nie blokować przewijania.

## Co można jeszcze dodać (pomysły)

- **Sekcja „O mnie”** — zdjęcie + krótki bio, np. ładowane z `about.json` lub na stałe w HTML.
- **Kontakt w stopce** — e-mail lub telefon (np. w config/JSON albo na stałe w `index.html`).
- **Formularze z JSON** — linki do Google Forms w pliku `forms.json`, tak jak usługi i galeria.
- **Własny favicon** — zamiana emoji na plik `favicon.ico` lub PNG (np. 32×32).
- **Canonical URL** — po wrzuceniu na domenę: `<link rel="canonical" href="https://twoja-domena.pl">` w `<head>`.
