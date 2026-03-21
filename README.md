# perra the dog — landing

Landing dla psiej behawiorystki z sekcjami: hero, oferta, galeria, opinie, formularz zgłoszeniowy i kontakt.

## Jak uruchomić

Otwórz plik `index.html` w przeglądarce (np. dwuklik) lub uruchom lokalny serwer:

```bash
# Python 3
python3 -m http.server 8000

# lub npx
npx serve .
```

Wejdź na: [http://localhost:8000](http://localhost:8000)

## Konfiguracja — config.json

Wszystko sterowane jest z pliku **config.json**: kolejność i widoczność sekcji, linki do formularzy, social media i dane w stopce.

### Sekcje (kolejność i widoczność)

W `sections` ustawiasz dla każdej sekcji:
- **id** — identyfikator (hero, oferta, galeria, opinie, formularz-zgloszeniowy, kontakt)
- **visible** — `true` / `false` (czy sekcja ma być widoczna)
- **order** — liczba (kolejność na stronie; mniejsza = wyżej)
- **label** — tekst w menu i w nawigacji kropkowej
- **sectionLabel** — opcjonalnie: mały napis nad tytułem sekcji (np. „Co oferuję”)
- **title** — tytuł sekcji (h1 w hero, h2 w pozostałych). W hero możesz użyć `\n` dla łamania linii.
- **intro** — opcjonalnie: krótki opis pod tytułem (paragraf). Pusty string lub brak = opis jest ukryty.

Przykład:
```json
"sections": [
  { "id": "hero", "visible": true, "order": 0, "label": "Start", "sectionLabel": "Behawiorystka psów", "title": "Spokojne życie z psem?\nTo możliwe!", "intro": "Cześć, jestem Paulina..." },
  { "id": "oferta", "visible": true, "order": 1, "label": "Oferta", "sectionLabel": "Co oferuję", "title": "Oferta", "intro": "" },
  { "id": "galeria", "visible": false, "order": 2, "label": "Galeria", "sectionLabel": "Zdjęcia", "title": "Galeria", "intro": "Kadry z konsultacji..." }
]
```

### Canonical URL (SEO)

- **canonicalUrl** — kanoniczny adres strony (aktualnie: `"https://perrathedog.pl/"`).

### Formularze, social media, stopka

- **forms** — tablica `{ "title", "description", "url" }` (np. linki do Google Forms)
- **socials** — tablica `{ "name", "url", "icon": "instagram" | "facebook" }`
- **footer** — `{ "email", "phoneHref", "phoneDisplay" }` (phoneHref bez spacji, np. +48123456789)

Linki i dane kontaktowe edytujesz wyłącznie w **config.json**. Plik `config.json` jest wymagany do poprawnego działania strony.

## Oferta z pliku JSON

Sekcja „Oferta” jest ładowana z pliku **services.json** (w tym samym folderze co `index.html`). Możesz edytować ten plik, aby zmieniać, dodawać lub usuwać pozycje.

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

- `src` — ścieżka do zdjęcia (np. `images/dog_pic_1.webp`) lub pełny URL
- `alt` — krótki opis (opcjonalny, wyświetla się po najechaniu)

Przykład **gallery.json**:

```json
[
  { "src": "images/dog_pic_1.webp", "alt": "Kawa" },
  { "src": "images/dog_pic_2.webp", "alt": "Jordan" }
]
```

Zdjęcia trzymaj w folderze **images/**. W projekcie obrazy galerii zostały zoptymalizowane i przepięte na format **WebP**.

Dodatkowo galeria ma **lightbox**: kliknięcie zdjęcia otwiera powiększenie (zamknięcie: `Esc`, klik w tło, przycisk `×`).

## Opinie (testimoniale)

Sekcja **Opinie** pokazuje cytaty od klientów. Lista jest w pliku **testimonials.json**.

Format każdej opinii:

- `quote` — treść wypowiedzi
- `author` — imię (i inicjał) lub pseudonim
- `context` — opcjonalnie: np. „9 opinii • rok temu”

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

## SEO i publikacja

W projekcie są już dodane:
- `canonical` + `canonicalUrl` ustawione na `https://perrathedog.pl/`
- Open Graph + Twitter Cards
- JSON-LD (`ProfessionalService`)
- `robots.txt`
- `sitemap.xml`

Po wdrożeniu na hosting sprawdź:
- czy strona działa pod `https://perrathedog.pl/`
- czy `https://perrathedog.pl/robots.txt` i `https://perrathedog.pl/sitemap.xml` zwracają `200`
- czy podgląd linku pobiera `og:image`
