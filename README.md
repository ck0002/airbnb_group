# Projekt Czyszczenia Danych Airbnb

## Airbnb Group - Członkowie zespołu:
* Cyprian Księżopolski
* Kacper Marciniak
* Michał Szumny
* Jakub Klimek

---

## O projekcie
Projekt polega na kompleksowym przygotowaniu surowego zbioru danych o ofertach Airbnb do dalszej analizy. Skupiamy się na eliminacji błędów, konwersji typów oraz inżynierii cech, aby stworzyć wiarygodną bazę wyjściową. Czyste dane pozwolą na rzetelne badanie zjawisk rynkowych, takich jak wpływ lokalizacji na cenę czy analiza popytu na poszczególne typy zakwaterowania.

---

## Plan Czyszczenia Zbioru Danych

### Faza 1: Zrzucenie Balastu (Quick Wins)
W tej fazie pozbywamy się śmieci, które tylko zżerają pamięć i zaburzają statystyki.
- [ ] **Usunięcie bezużytecznych kolumn:** Wyrzucenie kolumny `Unnamed: 0` (pozostałość po starym indeksie).
- [ ] **Usunięcie klonów:** Sprawdzenie i usunięcie zduplikowanych wierszy w skali 1:1 (ta sama oferta skopiowana dwa razy).

### Faza 2: Transformacja Typów Danych (Rzutowanie)
W tej fazie zmuszamy Pandas do poprawnego rozumienia liczb i dat.
- [ ] **`price`:** Wycięcie symbolu waluty (`$`) i konwersja kolumny ze zmiennej tekstowej na liczbową (`float`).
- [ ] **`number_of_stays`:** Konwersja na liczby całkowite (`int`) – usunięcie wartości po przecinku.
- [ ] **`listing_added` & `last_review`:** Konwersja ze zwykłego tekstu na format daty (`datetime`).

### Faza 3: Inżynieria Cech (Rozbijanie tekstu)
W tej fazie wyciągamy użyteczne informacje z brudnych ciągów znaków.
- [ ] **`coordinates`:** Rozbicie nawiasu i podział na dwie osobne kolumny numeryczne: `latitude` i `longitude`.
- [ ] **`neighbourhood_full`:** Rozdzielenie tekstu po przecinku na dwie nowe kolumny: `city` oraz `neighbourhood`.
- [ ] **`room_type`:** Ujednolicenie kategorii (np. "private room" i "private" -> jedna nazwa).

### Faza 4: Obsługa Braków Danych (Missing Values)
W tej fazie łatamy dziury w bazie.
- [ ] **Weryfikacja 2075 braków:** Sprawdzenie, czy braki w ocenach wynikają z braku recenzji (`number_of_reviews == 0`).
- [ ] **Uzupełnianie luk:** Decyzja o uzupełnieniu lub usunięciu braków w `price` (238), `name` (5) i `host_name` (2).

### Faza 5: Walidacja Logiki Biznesowej (Sanity Checks)
W tej fazie sprawdzamy, czy dane nie łamią praw fizyki i logiki ekonomicznej.
- [ ] **Test kalendarza:** Sprawdzenie `availability_365` pod kątem wartości ujemnych lub > 365.
- [ ] **Test chronologii:** Sprawdzenie, czy `last_review` nie jest starsze niż `listing_added`.
- [ ] **Test skali ocen:** Sprawdzenie, czy `rating` i `5_stars` mieszczą się w poprawnym przedziale (np. 1-5).

---

## Pliki w repozytorium
* `AirBnb.ipynb` - główny notatnik Jupyter zawierający kod wykonujący powyższe kroki czyszczenia danych oraz nasze odpowiedzi na pytania projektowe.
