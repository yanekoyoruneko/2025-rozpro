% Air Hockey
% Autor: Grupa 1A
% Data: \today

# Wprowadzenie do gry Air Hockey

## 1. Podstawowe zasady gry

Air Hockey to dynamiczna gra zręcznościowa rozgrywana między dwoma graczami, w której celem jest zdobywanie punktów poprzez umieszczenie krążka w bramce przeciwnika.

### 1.1. Cel gry
- Każdy gracz kontroluje wirtualną paletkę
- Zadaniem jest odbijanie krążka tak, by trafił do bramki przeciwnika
- Gra toczy się do osiągnięcia określonej liczby punktów (np. 7)

### 1.2. Elementy gry:
- **Boisko**: Prostokątna powierzchnia z wyznaczonymi bramkami
- **Krążek**: Mobilny element, który gracze odbijają
- **Paletki**: Elementy sterowane przez graczy
- **System punktacji**: Licznik punktów dla każdego gracza

---

## 2. Model komunikacji z serwerem

W celu komunikacji z serwerem zastosowaliśmy protokół **TCP (Transmission Control Protocol)**. Główne zalety tego rozwiązania:

1. **Niezawodność transmisji**:
   - Automatyczne wykrywanie i retransmisja zgubionych pakietów
   - Gwarancja dostarczenia danych w prawidłowej kolejności
   - Mechanizmy kontroli integralności danych

2. **Kontrola przepływu**:
   - Dynamiczne dostosowanie szybkości transmisji
   - Zapobieganie przeciążeniom sieci
   - Optymalizacja wykorzystania dostępnego pasma

3. **Dopasowanie do wymagań projektu**:
   - Idealne rozwiązanie dla gier 2-4 graczy
   - Wystarczająca przepustowość dla gry typu air hockey
   - Niskie opóźnienia w sieciach lokalnych

4. **Bezpieczeństwo**:
   - Nawiązywanie połączeń z potwierdzeniem
   - Mechanizmy unikania przeciążeń (congestion control)
   - Możliwość łatwej integracji z warstwą szyfrującą (TLS)

---

### **Schemat działania**

1. **Dołączenie do gry:**
   - Gracze (`Client_1`, `Client_2`) łączą się z lobby gry (`joinLobby()`).
   - System lobby sprawdza dostępność miejsc i tworzy nową sesję gry.

2. **Inicjalizacja rozgrywki:**
   - Serwer (`Server`) inicjalizuje grę (`initGame()`), tworząc środowisko (boisko, krążek, graczy).
   - Gracze otrzymują potwierdzenie rozpoczęcia gry (`startGameLoop()`).

3. **Przebieg rozgrywki:**
   - Gracze przesyłają swoje ruchy (`sendInput()`) – np. pozycje paletek.
   - Serwer aktualizuje stan gry (pozycja krążka, kolizje, punkty) i wysyła synchronizację (`sendGameUpdate()`).
   - Proces powtarza się w pętli, aż do zakończenia meczu.

4. **Zakończenie gry:**
   - Serwer ogłasza wyniki (`displayResults()`), np. po osiągnięciu limitu punktów.
   - Gracze mogą ponownie dołączyć do lobby (`joinLobby()`), aby zagrać kolejną rundę.

---

### **Diagram sekwencyjny**
![diagram sekwencyjny](diagram1.png)

### **Diagram klas**
![diagram klas](diagram2.png)
