# Listing Workflow / Przepływ Tworzenia Ogłoszeń

This document explains the automated listing workflow for items in the repository.

Ten dokument wyjaśnia zautomatyzowany przepływ tworzenia ogłoszeń dla przedmiotów w repozytorium.

## Overview / Przegląd

The listing workflow ensures that items added to the repository are actually listed on marketplaces and that the listings are properly tracked and validated.

Przepływ ogłoszeń zapewnia, że przedmioty dodane do repozytorium są rzeczywiście wystawione na platformach sprzedażowych i że ogłoszenia są prawidłowo śledzone i weryfikowane.

## Workflow Steps / Kroki Przepływu

### 1. Item Added to Repository / Przedmiot Dodany do Repozytorium

When a new item PR is merged:
- A GitHub Action automatically creates a "listing-needed" issue
- The issue contains all item details including the unique item ID
- The issue is assigned to the repository owner

Gdy nowy PR z przedmiotem zostaje zatwierdzony:
- GitHub Action automatycznie tworzy zgłoszenie z etykietą "listing-needed"
- Zgłoszenie zawiera wszystkie szczegóły przedmiotu, w tym unikalny ID przedmiotu
- Zgłoszenie jest przypisane do właściciela repozytorium

### 2. Create Marketplace Listing / Utworzenie Ogłoszenia

The repository owner (or assigned person) must:
1. Create a listing on a marketplace (OLX, Allegro, Facebook Marketplace, etc.)
2. **IMPORTANT:** Include the item ID in the listing description (e.g., `Item ID: tefal-blender-001`)
3. Publish the listing

Właściciel repozytorium (lub przypisana osoba) musi:
1. Utworzyć ogłoszenie na platformie sprzedażowej (OLX, Allegro, Facebook Marketplace, itp.)
2. **WAŻNE:** Umieścić ID przedmiotu w opisie ogłoszenia (np. `Item ID: tefal-blender-001`)
3. Opublikować ogłoszenie

### 3. Submit Listing URL / Przesłanie URL Ogłoszenia

Once the listing is live:
1. Add a comment to the listing issue with the URL
2. Use the format: `Listing URL: https://...`
3. Close the issue

Po opublikowaniu ogłoszenia:
1. Dodaj komentarz do zgłoszenia z URL
2. Użyj formatu: `Listing URL: https://...`
3. Zamknij zgłoszenie

**Example comment / Przykład komentarza:**
```
Listing URL: https://www.olx.pl/d/oferta/tefal-blender-xyz123
```

### 4. Automatic Validation / Automatyczna Walidacja

When the issue is closed, a GitHub Action automatically:
1. Extracts the listing URL from the comment
2. Fetches the listing page
3. Verifies that the item ID appears in the listing
4. Updates the item JSON with:
   - `listingUrl`: The marketplace URL
   - `listedDate`: When the listing was created
   - `status`: Changes from "available" to "listed"
5. Creates a PR with these updates

Gdy zgłoszenie jest zamykane, GitHub Action automatycznie:
1. Wyciąga URL ogłoszenia z komentarza
2. Pobiera stronę ogłoszenia
3. Weryfikuje, czy ID przedmiotu pojawia się w ogłoszeniu
4. Aktualizuje JSON przedmiotu o:
   - `listingUrl`: URL platformy sprzedażowej
   - `listedDate`: Kiedy ogłoszenie zostało utworzone
   - `status`: Zmienia z "available" na "listed"
5. Tworzy PR z tymi aktualizacjami

### 5. Validation Success / Sukces Walidacji

If validation succeeds:
- The issue gets a "listing-verified" label
- A PR is created to update the item
- A success comment is posted on the issue

Jeśli walidacja się powiedzie:
- Zgłoszenie otrzymuje etykietę "listing-verified"
- Tworzony jest PR z aktualizacją przedmiotu
- Komentarz z potwierdzeniem jest dodawany do zgłoszenia

### 6. Validation Failure / Niepowodzenie Walidacji

If validation fails (URL inaccessible or item ID not found):
- The issue is automatically reopened
- An error comment explains what went wrong
- You can fix the issue and try again

Jeśli walidacja się nie powiedzie (URL niedostępny lub ID przedmiotu nie znaleziono):
- Zgłoszenie jest automatycznie ponownie otwierane
- Komentarz z błędem wyjaśnia, co poszło nie tak
- Możesz naprawić problem i spróbować ponownie

## Item Status Values / Wartości Statusu Przedmiotu

- `available` - Item added to repository, not yet listed / Przedmiot dodany do repozytorium, jeszcze nie wystawiony
- `listed` - Item has verified marketplace listing / Przedmiot ma zweryfikowane ogłoszenie na platformie
- `pending` - Sale in progress / Sprzedaż w toku
- `sold` - Item sold / Przedmiot sprzedany
- `removed` - Listing removed / Ogłoszenie usunięte

## Supported Marketplaces / Obsługiwane Platformy

The validation works with any marketplace URL, including:
- OLX.pl
- Allegro.pl
- Facebook Marketplace
- Vinted
- Custom websites

Walidacja działa z każdym URL platformy sprzedażowej, w tym:
- OLX.pl
- Allegro.pl
- Facebook Marketplace
- Vinted
- Własne strony internetowe

## Tips / Wskazówki

1. **Always include the item ID** in your listing description - this is required for validation
   **Zawsze umieszczaj ID przedmiotu** w opisie ogłoszenia - jest to wymagane do walidacji

2. **Use the exact format** when posting the URL: `Listing URL: https://...`
   **Używaj dokładnego formatu** przy dodawaniu URL: `Listing URL: https://...`

3. **Wait for the listing to be live** before closing the issue
   **Poczekaj aż ogłoszenie będzie aktywne** przed zamknięciem zgłoszenia

4. **Check the validation results** - if it fails, you can fix and retry
   **Sprawdź wyniki walidacji** - jeśli się nie powiedzie, możesz naprawić i spróbować ponownie

## Troubleshooting / Rozwiązywanie Problemów

### "No listing URL found in comments"
- Make sure you used the format: `Listing URL: https://...`
- The URL must be in a comment, not just the issue description

### "Item ID not found in listing"
- Verify that the item ID is included in the listing description
- Check that you used the correct item ID
- The item ID must be visible in the HTML of the listing page

### "Failed to fetch listing"
- Check that the URL is correct and accessible
- Some marketplaces may require authentication or have rate limiting
- Try accessing the URL in a browser to verify it works

## Example Full Workflow / Przykład Pełnego Przepływu

1. PR merged: Item `tefal-blender-001` added to repository
2. Issue #5 created: "Create listing for: Tefal Blender"
3. Owner creates listing on OLX including "Item ID: tefal-blender-001"
4. Owner comments: `Listing URL: https://www.olx.pl/d/oferta/tefal-blender-xyz`
5. Owner closes issue #5
6. GitHub Action validates the listing
7. PR #6 created: "Add listing URL for tefal-blender-001"
8. PR merged: Item JSON updated with listing URL and status "listed"
