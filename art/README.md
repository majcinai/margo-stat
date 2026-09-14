# Grafika — katalog zasobów

Gra sama sprawdza przy starcie, które pliki tu leżą. Plik, którego nie ma,
nie jest problemem: ten stwór rysuje się proceduralnie, tak jak dotąd.
Można więc uzupełniać bestiariusz po jednej sztuce.

## Nazwy plików

| Co            | Nazwa                   | Format                         |
|---------------|-------------------------|--------------------------------|
| zwykły potwór | `mob-<klucz>.png`       | przezroczysty PNG, kwadrat     |
| boss krainy   | `boss-<kraina>.png`     | przezroczysty PNG, kwadrat     |
| Wędrowny Heros| `hero.png`              | przezroczysty PNG, kwadrat     |
| tło areny     | `arena-<kraina>.jpg`    | 16:9, bez postaci              |

`<klucz>` to klucz z obiektu `MONSTERS`, a `<kraina>` — `id` z tablicy `ZONES`
w pliku `kroniki-eldrenu.html`. Zamiast `.png` działa też `.webp`,
a dla aren `.jpg`, `.png` lub `.webp`.

Pełna lista nazw wraz z gotowymi promptami jest w pakiecie produkcyjnym
(artefakt „Prompty Bestiariusza Eldrenu").

## JPG a przezroczystość

JPG **nie umie w przezroczystość**. Sprite zapisany jako JPG wyświetli się
w grze jako kwadrat z tłem — nawet jeśli w generatorze wyglądał na wycięty.
Są dwa wyjścia:

1. **Zapisz sprite'y jako PNG** — najlepsza jakość, żadnych obwódek.
2. **Wgraj JPG przez grę**: ⚙️ → „Grafika i zasoby" → przeciągnij pliki.
   Gra wytnie jednolite tło (także szachownicę z podglądu przezroczystości)
   i zapamięta grafikę w przeglądarce. Tego samego nie da się zrobić dla
   plików z tego katalogu: przeglądarka nie pozwala czytać pikseli obrazka
   wczytanego z dysku, a przy przeciąganiu pliku — pozwala.

Wycinanie tła z JPG bywa nieidealne przy samej krawędzi (kompresja JPEG
rozmywa kontur), więc jeśli masz wybór — PNG.

Tła aren mogą być JPG bez żadnych zastrzeżeń: mają być nieprzezroczyste.

## Wymagania

- sprite: kwadrat 512 × 512 (lub 1024), tło **w pełni przezroczyste**,
  bez podłoża i bez cienia rzucanego — silnik dokłada własny,
- stopy przy dolnej krawędzi kadru: sprite jest kotwiczony do dołu
  (`object-position: center bottom`), więc puste miejsce pod postacią
  podnosi ją nad arenę,
- kontur ciepły brąz `rgba(28,16,6,.55)`, nigdy czysta czerń,
- światło z góry od lewej,
- arena: jasna i mało kontrastowa w środku kadru — tam stają walczący;
  silnik sam przyciemnia górę i dół, żeby HUD i log zostały czytelne.

## Sprawdzenie

Otwórz `kroniki-eldrenu.html` i wejdź w dowolną walkę w danej krainie.
Jeśli zasób został znaleziony, gra przerysowuje się automatycznie
kilkaset milisekund po starcie.
