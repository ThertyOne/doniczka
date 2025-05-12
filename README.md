# 🌱 SmartPlantPot – Inteligentna Doniczka z Twarzą

Inteligentna doniczka dla początkujących miłośników roślin, która komunikuje potrzeby roślinki za pomocą wyrażeń twarzy na ekranie LED, zbiera dane środowiskowe i łączy się z aplikacją mobilną przez Wi-Fi.

---

## 🎯 Cel projektu

Stworzyć urządzenie pomagające użytkownikowi zadbać o roślinę poprzez:
- wyświetlanie stanu rośliny za pomocą graficznych buziek,
- monitorowanie parametrów środowiska (gleba, światło, temperatura, wilgotność, poziom wody),
- przesyłanie danych do aplikacji mobilnej przez Wi-Fi (Firebase),
- możliwość dodawania zdjęć i notatek w aplikacji.

---

## 🧠 Główne funkcje

- Detekcja potrzeb rośliny i pokazanie ich na buźce LED.
- Łączność Wi-Fi i Bluetooth (do pierwszej konfiguracji).
- Zasilanie akumulatorem ładowanym przez USB-C.
- Aplikacja mobilna Flutter z integracją Firebase.
- Możliwość dokumentacji wzrostu (zdjęcia, notatki).

---

## 🔌 Hardware

### 🔧 Główne komponenty

| Komponent | Opis | Link |
|----------|------|------|
| ESP32 | Mikrokontroler z Wi-Fi i Bluetooth | [Link](https://pl.aliexpress.com/item/1005005988953058.html) |
| Wyświetlacz LED | Mini ekran OLED/IPS | [Link](https://pl.aliexpress.com/item/32761097685.html) |
| Czujnik wilgotności gleby | Kapacyjny (niesieciwiejący) | [Link](https://pl.aliexpress.com/item/1005006365881525.html) |
| Czujnik warunków atmosferycznych | BME280 (temp., wilgotność, ciśnienie) | [Link](https://pl.aliexpress.com/item/1005006984793820.html) |
| Akumulator Li-Ion/Li-Po | np. 18650 3.7V 2000-3000 mAh | - |
| Moduł ładowania | TP4056 lub układ z USB-C + zabezpieczenie | [Link](https://pl.aliexpress.com/item/1005005237080994.html) |
| Czujnik światła | Fotorezystor (GL5616) lub TSL2561 (cyfrowy) | [Link](https://pl.aliexpress.com/item/1005007257546981.html) |

---

## 🔋 Zasilanie

- Zasilanie z akumulatora (np. 18650) ładowanego przez port USB-C.
- Można zastosować gotowy moduł ładowania z zabezpieczeniem (np. TP4056 z USB-C).
- ESP32 przechodzi w tryb oszczędzania energii, gdy nie jest aktywny.

---

## 📱 Aplikacja mobilna (Flutter)

### Funkcje:
- Dodawanie nowej doniczki (skan QR, konfiguracja Wi-Fi)
- Monitorowanie parametrów rośliny (gleba, temp., wilgotność itp.)
- Historia i statystyki
- Możliwość dodawania zdjęć i notatek
- Powiadomienia push (Firebase Cloud Messaging)

---

## ☁️ Backend – Firebase

- **Firebase Auth** – logowanie użytkownika
- **Firebase Firestore** – przechowywanie danych roślin i czujników
- **Firebase Storage** – przechowywanie zdjęć rośliny
- **Firebase Functions** – opcjonalnie, do walidacji i przetwarzania danych
- **Firebase Cloud Messaging** – wysyłka powiadomień

---

## 🌐 Proces konfiguracji Wi-Fi

1. ESP32 uruchamia się po raz pierwszy → uruchamia tryb Access Point (np. `PlantPot-XXXX`).
2. Na ekranie wyświetla się kod QR z adresem AP.
3. Użytkownik:
   - w aplikacji wybiera „Dodaj nową doniczkę”,
   - skanuje QR i łączy się z AP `PlantPot-XXXX`,
   - aplikacja wysyła dane Wi-Fi użytkownika (SSID i hasło) do `http://192.168.4.1/setup` (ESP32 w trybie AP),
   - ESP32 restartuje się i łączy z docelowym Wi-Fi.

---

## 🧪 Czujniki i logika interpretacji

| Parametr | Czujnik | Co pokazuje buźka? |
|---------|--------|--------------------|
| Wilgotność gleby | Czujnik kapacyjny | Za sucho? Smutna buźka. Idealnie? Uśmiechnięta. |
| Temperatura i wilgotność | BME280 | Zbyt gorąco/zimno? Niezadowolona mina. |
| Poziom światła | Fotorezystor / TSL2561 | Za ciemno? Buźka śpiąca/ziewająca. |
| Poziom wody | Czujnik przewodności / pływakowy | Brak wody w zbiorniku? Ikona kropli z przekreśleniem. |

---

## 🔄 Tryby pracy

- **Normalny** – ESP32 działa w trybie oszczędnym, odczyty co kilka minut, dane wysyłane do Firebase.
- **Debug/Diagnostyczny** – wyświetla szczegółowe dane i działa intensywniej.
- **Setup (AP)** – tylko przy pierwszej konfiguracji.

---

## 📐 Obudowa

- Wydruk 3D lub gotowa plastikowa doniczka z przestrzenią na elektronikę.
- Otwory do pomiaru światła, dostęp powietrza.
- Wbudowany ekran LED lub OLED w widocznym miejscu.

---

## 📦 Opcjonalne przyszłe rozszerzenia

- Automatyczne podlewanie (mała pompka perystaltyczna).
- Wsparcie dla wielu doniczek na koncie użytkownika.
- Analiza zdjęć rośliny (AI – np. wykrycie uschnięcia).
- System powiadomień z radami ogrodniczymi.

---

Projekt inspirowany ideą uczłowieczenia technologii i stworzenia emocjonalnej więzi między człowiekiem a rośliną 🌿🙂
