# Items for Sale / Przedmioty na Sprzedaż

A bilingual repository for managing and listing items for sale in Poland.

Dwujęzyczne repozytorium do zarządzania i wystawiania przedmiotów na sprzedaż w Polsce.

## Directory Structure / Struktura Katalogów

- `items/` - JSON files containing item listings / Pliki JSON z listami przedmiotów
- `images/` - Product images and media files / Zdjęcia produktów i pliki medialne
- `docs/` - Additional documentation / Dodatkowa dokumentacja
- `.github/ISSUE_TEMPLATE/` - GitHub issue templates / Szablony zgłoszeń GitHub
- `.github/workflows/` - GitHub Actions automation / Automatyzacja GitHub Actions

## Item Schema / Schemat Przedmiotu

Each item listing should follow the schema defined in `docs/item-schema.json`. All text fields (title, description) must be provided in both English and Polish.

Każdy przedmiot powinien być zgodny ze schematem zdefiniowanym w `docs/item-schema.json`. Wszystkie pola tekstowe (tytuł, opis) muszą być podane w języku angielskim i polskim.

## Usage / Użytkowanie

### Method 1: Submit via GitHub Issues (Recommended) / Metoda 1: Zgłoszenie przez GitHub Issues (Zalecane)

1. Click on the "Issues" tab in this repository / Kliknij zakładkę "Issues" w tym repozytorium
2. Click "New Issue" / Kliknij "New Issue"
3. Select "Submit New Item for Sale" / Wybierz "Submit New Item for Sale"
4. Fill out the form with your item details in both English and Polish / Wypełnij formularz danymi przedmiotu w języku angielskim i polskim
5. Submit the issue / Wyślij zgłoszenie

**Automated Process / Automatyczny Proces:**

Once you submit the issue, a GitHub Action will automatically:
Po przesłaniu zgłoszenia, GitHub Action automatycznie:

- Parse your submission and create a JSON file / Przetworzy zgłoszenie i utworzy plik JSON
- Create a new branch for the item / Utworzy nową gałąź dla przedmiotu
- Generate a Pull Request with the item details / Wygeneruje Pull Request ze szczegółami przedmiotu
- Comment on your issue with the PR link / Skomentuje zgłoszenie z linkiem do PR

The item will be added to the repository once the PR is reviewed and merged by a maintainer.

Przedmiot zostanie dodany do repozytorium po sprawdzeniu i zatwierdzeniu PR przez opiekuna.

### Method 2: Direct Commit / Metoda 2: Bezpośredni Commit

1. Create a new JSON file in the `items/` directory / Utwórz nowy plik JSON w katalogu `items/`
2. Follow the item schema template with bilingual content / Postępuj zgodnie z szablonem schematu z dwujęzyczną treścią
3. Add corresponding images to the `images/` directory / Dodaj odpowiednie zdjęcia do katalogu `images/`
4. Reference images using relative paths in the item listing / Odwołuj się do zdjęć używając ścieżek względnych w opisie przedmiotu

## Example / Przykład

See `items/example-item.json` for a sample item listing with bilingual content.

Zobacz `items/example-item.json` jako przykład opisu przedmiotu z dwujęzyczną treścią.

## Currency / Waluta

All items are priced in Polish Złoty (PLN) by default, but other currencies (EUR, USD, etc.) are also supported.

Wszystkie przedmioty są domyślnie wyceniane w polskich złotych (PLN), ale inne waluty (EUR, USD, itp.) są również obsługiwane.

## Automation / Automatyzacja

This repository uses GitHub Actions with a GitHub App to automate the item submission process.

To repozytorium wykorzystuje GitHub Actions z aplikacją GitHub do automatyzacji procesu zgłaszania przedmiotów.

**Setup Required / Wymagana Konfiguracja:**
- A GitHub App must be configured with appropriate permissions
- See `docs/github-app-setup.md` for detailed setup instructions
- Aplikacja GitHub musi być skonfigurowana z odpowiednimi uprawnieniami
- Zobacz `docs/github-app-setup.md` po szczegółowe instrukcje konfiguracji

**Workflow / Przepływ pracy:**

**Phase 1: Item Submission / Faza 1: Zgłoszenie Przedmiotu**
1. User submits an issue using the template / Użytkownik przesyła zgłoszenie używając szablonu
2. User uploads images or provides image URLs / Użytkownik przesyła zdjęcia lub podaje URL-e zdjęć
3. GitHub Action validates and parses the issue / GitHub Action waliduje i przetwarza zgłoszenie
4. GitHub Action automatically downloads all images / GitHub Action automatycznie pobiera wszystkie zdjęcia
5. A new branch is created with the item JSON file and images / Nowa gałąź jest tworzona z plikiem JSON i zdjęciami
6. A Pull Request is automatically generated / Pull Request jest automatycznie generowany
7. Maintainer reviews and merges the PR / Opiekun sprawdza i zatwierdza PR
8. Item becomes available in the repository / Przedmiot staje się dostępny w repozytorium

**Phase 2: Marketplace Listing / Faza 2: Ogłoszenie na Platformie**
9. GitHub Action creates a "listing-needed" issue / GitHub Action tworzy zgłoszenie "listing-needed"
10. Owner creates marketplace listing (OLX, Allegro, etc.) / Właściciel tworzy ogłoszenie na platformie
11. Owner must include marker `#!#item-id#!#` in listing description / Właściciel musi umieścić znacznik `#!#id-przedmiotu#!#` w opisie
12. Owner closes the issue with the listing URL / Właściciel zamyka zgłoszenie z URL ogłoszenia
13. GitHub Action validates the listing (checks for marker) / GitHub Action weryfikuje ogłoszenie (sprawdza znacznik)
14. GitHub Action updates the item with listing URL / GitHub Action aktualizuje przedmiot z URL ogłoszenia

**See `docs/listing-workflow.md` for detailed information about the listing process.**
**Zobacz `docs/listing-workflow.md` po szczegółowe informacje o procesie tworzenia ogłoszeń.**

**Labels / Etykiety:**
- `new-item` - Triggers item creation automation / Uruchamia automatyzację tworzenia przedmiotu
- `pending-review` - Awaiting review / Oczekuje na sprawdzenie
- `processed` - Automation completed successfully / Automatyzacja zakończona pomyślnie
- `listing-needed` - Item needs marketplace listing / Przedmiot wymaga ogłoszenia na platformie
- `listing-verified` - Listing URL has been validated / URL ogłoszenia został zweryfikowany

## Contributing / Współtworzenie

To submit a new item, please use the GitHub issue template. This ensures all required information is provided in both languages and maintains consistency across listings.

Aby zgłosić nowy przedmiot, proszę użyć szablonu zgłoszenia GitHub. To zapewnia, że wszystkie wymagane informacje są podane w obu językach i utrzymuje spójność w całym repozytorium.
