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

Jeśli `services.json` nie istnieje lub jest nieprawidłowy, na stronie pojawi się komunikat z prośbą o sprawdzenie pliku.
