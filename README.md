# Perra the Dog — landing

Landing dla psiej behawiorystki z sekcjami: hero, usługi, rejestracja (Google Forms), social media.

## Jak uruchomić

Otwórz plik `index.html` w przeglądarce (np. dwuklik) lub uruchom lokalny serwer:

```bash
# Python 3
python3 -m http.server 8000

# lub npx
npx serve .
```

Wejdź na: http://localhost:8000

## Gdzie wkleić swoje linki

W pliku **index.html** znajdź i zamień:

1. **Instagram** — szukaj: `TWOJ_INSTAGRAM`  
   Zamień na np. `twoj_profil` (pełny link: `https://www.instagram.com/twoj_profil/`).

2. **Facebook** — szukaj: `TWOJ_FACEBOOK`  
   Zamień na np. `twoja.strona` lub pełny URL strony.

3. **Google Forms** — szukaj: `TWOJ_LINK_GOOGLE_FORMS_1` i `TWOJ_LINK_GOOGLE_FORMS_2`  
   Wklej linki do formularzy z Google Forms (np. dla konsultacji i dla warsztatów).

4. **Kontakt w stopce** — w **index.html** zamień:
   - `TWOJ_EMAIL` (w dwóch miejscach: w `href="mailto:..."` i w tekście linku) na swój adres e-mail,
   - `+48TWOJ_TELEFON` w `href="tel:..."` na numer z kierunkowym, np. `+48123456789` (same cyfry),
   - `+48 TWOJ_TELEFON` w tekście na wyświetlaną formę, np. `+48 123 456 789`.

Po wklejeniu linków zapisz plik i odśwież stronę.

## Przełącznik koloru akcentu

W menu (nav) jest przełącznik **Biały / Różowy**. Odwiedzający może wybrać kolor akcentu; wybór jest zapisywany w przeglądarce (localStorage) i zostaje po odświeżeniu strony.

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

Jeśli plik nie załaduje się (np. przy file://), wyświetlą się wbudowane przykładowe opinie.

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
