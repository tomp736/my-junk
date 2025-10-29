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
2. **IMPORTANT:** Include the item ID marker in the listing description: `#!#item-id#!#`
   - Example for item "tefal-blender-001": `#!#tefal-blender-001#!#`
   - You can put it anywhere in the description (beginning, middle, or end)
   - The marker can be on its own line or mixed with other text
   - This unique format ensures validation accuracy
3. Publish the listing

Właściciel repozytorium (lub przypisana osoba) musi:
1. Utworzyć ogłoszenie na platformie sprzedażowej (OLX, Allegro, Facebook Marketplace, itp.)
2. **WAŻNE:** Umieścić znacznik ID przedmiotu w opisie ogłoszenia: `#!#id-przedmiotu#!#`
   - Przykład dla przedmiotu "tefal-blender-001": `#!#tefal-blender-001#!#`
   - Możesz umieścić go w dowolnym miejscu opisu (na początku, w środku lub na końcu)
   - Znacznik może być w osobnej linii lub razem z innym tekstem
   - Ten unikalny format zapewnia dokładność walidacji
3. Opublikować ogłoszenie

### 3. Submit Listing URL / Przesłanie URL Ogłoszenia

Once the listing is live:
1. Add a comment to the listing issue with the URL
2. Use the format: `Listing URL: https://...`
3. The validation will start automatically - no need to close the issue!

Po opublikowaniu ogłoszenia:
1. Dodaj komentarz do zgłoszenia z URL
2. Użyj formatu: `Listing URL: https://...`
3. Walidacja rozpocznie się automatycznie - nie musisz zamykać zgłoszenia!

**Example comment / Przykład komentarza:**
```
Listing URL: https://www.olx.pl/d/oferta/tefal-blender-xyz123
```

**Important:** The issue will remain open until the validation PR is merged.
**Ważne:** Zgłoszenie pozostanie otwarte do momentu zatwierdzenia PR z walidacją.

### 4. Automatic Validation / Automatyczna Walidacja

When you add a comment with "Listing URL:", a GitHub Action automatically:
1. Extracts the listing URL from your comment
2. Fetches the listing page
3. Verifies that the item ID marker (`#!#item-id#!#`) appears in the listing
4. Updates the item JSON with:
   - `listingUrl`: The marketplace URL
   - `listedDate`: When the listing was created
   - `status`: Changes from "available" to "listed"
5. Creates a PR with these updates

Gdy dodasz komentarz z "Listing URL:", GitHub Action automatycznie:
1. Wyciąga URL ogłoszenia z komentarza
2. Pobiera stronę ogłoszenia
3. Weryfikuje, czy znacznik ID przedmiotu (`#!#id-przedmiotu#!#`) pojawia się w ogłoszeniu
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
- **The issue remains open** until the PR is merged

Jeśli walidacja się powiedzie:
- Zgłoszenie otrzymuje etykietę "listing-verified"
- Tworzony jest PR z aktualizacją przedmiotu
- Komentarz z potwierdzeniem jest dodawany do zgłoszenia
- **Zgłoszenie pozostaje otwarte** do momentu zatwierdzenia PR

### 6. PR Merge and Issue Closure / Zatwierdzenie PR i Zamknięcie Zgłoszenia

When the validation PR is merged:
- A final success comment is added to the issue
- The issue is automatically closed
- The item is now fully listed and tracked!

Gdy PR walidacyjny zostaje zatwierdzony:
- Ostatni komentarz z potwierdzeniem jest dodawany do zgłoszenia
- Zgłoszenie jest automatycznie zamykane
- Przedmiot jest teraz w pełni wystawiony i śledzony!

### 7. Validation Failure / Niepowodzenie Walidacji

If validation fails (URL inaccessible or item ID marker not found):
- An error comment explains what went wrong
- The issue remains open
- You can add another comment with the corrected URL to try again

Jeśli walidacja się nie powiedzie (URL niedostępny lub znacznik ID przedmiotu nie znaleziony):
- Komentarz z błędem wyjaśnia, co poszło nie tak
- Zgłoszenie pozostaje otwarte
- Możesz dodać kolejny komentarz z poprawionym URL aby spróbować ponownie

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

1. **Always include the marker** `#!#item-id#!#` in your listing description - this is required for validation
   **Zawsze umieszczaj znacznik** `#!#id-przedmiotu#!#` w opisie ogłoszenia - jest to wymagane do walidacji

2. **The marker can be placed anywhere** - at the end, in the middle, or even hidden in formatting
   **Znacznik może być umieszczony gdziekolwiek** - na końcu, w środku lub nawet ukryty w formatowaniu

3. **Use the exact format** when posting the URL: `Listing URL: https://...`
   **Używaj dokładnego formatu** przy dodawaniu URL: `Listing URL: https://...`

4. **Wait for the listing to be live** before closing the issue
   **Poczekaj aż ogłoszenie będzie aktywne** przed zamknięciem zgłoszenia

5. **Check the validation results** - if it fails, you can fix and retry
   **Sprawdź wyniki walidacji** - jeśli się nie powiedzie, możesz naprawić i spróbować ponownie

## Troubleshooting / Rozwiązywanie Problemów

### "No listing URL found in comments"
- Make sure you used the format: `Listing URL: https://...`
- The URL must be in a comment, not just the issue description

### "Item ID marker not found in listing"
- Verify that the marker `#!#item-id#!#` is included in the listing description
- Check that you used the correct item ID with the exact marker format
- Example: for item "tefal-blender", use `#!#tefal-blender#!#`
- The marker must be present in the HTML of the listing page (visible or hidden)

### "Failed to fetch listing"
- Check that the URL is correct and accessible
- Some marketplaces may require authentication or have rate limiting
- Try accessing the URL in a browser to verify it works

## Example Full Workflow / Przykład Pełnego Przepływu

1. PR #3 merged: Item `tefal-blender-001` added to repository
2. Issue #5 auto-created: "Create listing for: Tefal Blender" (status: open, label: listing-needed)
3. Owner creates listing on OLX with description:
   ```
   Sprzedam blender Tefal w doskonałym stanie.
   Moc: 1200W, pojemność: 2L

   #!#tefal-blender-001#!#
   ```
4. Owner adds comment to issue #5: `Listing URL: https://www.olx.pl/d/oferta/tefal-blender-xyz`
5. GitHub Action automatically validates the listing (finds marker `#!#tefal-blender-001#!#`)
6. Issue #5 gets "listing-verified" label, remains open
7. PR #6 auto-created: "Add listing URL for tefal-blender-001"
8. Owner reviews and merges PR #6
9. Issue #5 automatically closed with success message
10. Item JSON now has listing URL and status "listed"

**Note:** The marker can be hidden at the end of your description or placed anywhere. It will be found by the validation system.

**Key Points:**
- Issue stays open from step 2 until step 9
- Validation happens automatically when you comment (no need to close issue)
- Issue only closes after the validation PR is merged
