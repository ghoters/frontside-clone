# Tło z grafiką dla kart rozmiaru (/oferta, krok 2)

## Cel
Karty wyboru rozmiaru figurki ("15 cm", "20 cm", "25 cm") w kroku 2 konfiguratora na `/oferta` dostają grafikę figurki jako tło całego boksa. Układ i treść kart pozostają bez zmian — dodajemy tylko grafikę.

## Zakres
- Karta **25 cm** ("Najbardziej efektowny", +100 zł) dostaje jako tło przesłaną grafikę `Rozmiar_3.jpg` (figurka mężczyzny na białym tle).
- Karty **15 cm** i **20 cm** dostają gotowy mechanizm tła — grafiki dla nich użytkownik prześle później (np. `Rozmiar_1.jpg`, `Rozmiar_2.jpg`).
- Reszta strony bez zmian.

## Kroki

1. **Asset grafiki**
   - Wgraj `user-uploads://Rozmiar_3.jpg` przez `lovable-assets` do `src/assets/rozmiar-3.jpg.asset.json`.

2. **Dane kart rozmiaru** (`src/routes/oferta.tsx`)
   - Rozszerz typ tablicy `sizes` o pola `image?: string` i `imageFull?: boolean`.
   - Wpis "25 cm": `image: rozmiar3Asset.url, imageFull: true`.
   - Wpisy "15 cm" i "20 cm": pola obecne, ale bez grafiki (placeholder placeholder-owy znika dopiero po dodaniu grafiki — do czasu pozostają jak dziś).
   - Import wskaźnika: `import rozmiar3Asset from "@/assets/rozmiar-3.jpg.asset.json"`.

3. **Komponent `ChoiceCard`**
   - Już obsługuje pełne tło (`imageFull` + `image` → absolutny span z `background-image` na całej karcie). Żadnych zmian w layoucie, tekście ani cenie.

4. **Weryfikacja**
   - Screenshot sekcji "Rozmiar figurki" w podglądzie (Playwright) — figurka widoczna jako tło karty 25 cm, tekst i cena czytelne, pozostałe karty bez zmian.
   - Jeśli figurka koliduje z tekstem karty, dopasuję `background-position` grafiki (bez zmiany układu treści).

## Szczegóły techniczne
- Pełne tło renderuje istniejący kod `ChoiceCard` (span `absolute inset-0` z `bg-[length:100%_100%]`), tekst ma `max-w-[62%]`, cena jest wyśrodkowana — grafika jest jasna, więc kontrast tekstu pozostaje dobry.
- Grafika trafia na CDN przez Lovable Assets; do repo trafia tylko plik wskaźnika `.asset.json`.
