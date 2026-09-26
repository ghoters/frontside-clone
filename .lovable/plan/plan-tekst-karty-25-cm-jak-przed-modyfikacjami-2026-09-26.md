# Plan: tekst karty 25 cm jak przed modyfikacjami

## Cel
Karta „25 cm" z grafiką tła ma mieć tekst (tytuł, opis, cena) w dokładnie takim samym miejscu i układzie jak karty bez grafiki (15 cm, 20 cm). Boks pozostaje bez żadnej nakładki.

## Stan obecny (zweryfikowany w kodzie)
- Nakładki/gradientu na boksie nie ma — grafika jest czystym tłem karty (pełny boks, `background-image` na całej powierzchni). Nic do usuwania w tej kwestii.
- Tekst karty z grafiką tła jest jednak zwężony do 62% szerokości (`max-w-[62%]`), podczas gdy pozostałe karty nie mają takiego ograniczenia. To powoduje, że tekst układa się inaczej niż przed dodaniem grafiki.

## Zmiana
- W `src/routes/oferta.tsx` (komponent `ChoiceCard`) usunąć zwężenie `max-w-[62%]` dla kart z pełnym tłem graficznym, aby kolumna tekstu miała identyczny układ jak w kartach 15 cm i 20 cm (bez zmian pozycji, odstępów i wyśrodkowania ceny).
- Grafika tła pozostaje bez zmian (oryginał, bez odbicia, bez nakładki).

## Weryfikacja
- Zrzut ekranu sekcji „Rozmiar figurki" w podglądzie: tekst na karcie 25 cm w tym samym miejscu co na kartach 15/20 cm, grafika widoczna jako tło.
- Sprawdzenie logu budowania (build OK).
