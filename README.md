# Pepsi House — randomizer premii (Android)

Aplicație de activare BTL: ecran de start cu grafica Pepsi → la apăsarea pe START, reel-ul „rulează" și se oprește pe premiul câștigat, afișat în cutia centrală din grafica originală. Premiile se acordă aleatoriu doar din stocul disponibil, iar stocul scade automat la fiecare câștig.

Construită ca aplicație web (React) împachetată cu **Capacitor**. APK-ul se generează automat în cloud prin **GitHub Actions** — nu ai nevoie de Android Studio.

## Funcții

**Ecran 1 — Start**: grafica originală „Ce ai câștigat azi în Pepsi House?" cu butonul START activ.

**Ecran 2 — Rezultat**: reel animat (rulare cu decelerare, ~2.7s) care se oprește pe premiu, afișat în cutia centrală, exact peste poziția din grafica originală. Rândurile de deasupra/dedesubt apar estompate, ca în machetă. Buton „ÎNCĂ O DATĂ" pentru următorul participant.

**Admin** (acces secret: 4 tap-uri rapide în colțul dreapta-sus → parolă `admin123`):
- adăugare premiu (nume + stoc)
- modificare stoc cu −/+ sau direct din câmp
- ștergere premiu
- premiile cu stoc 0 sunt excluse automat de la extragere

**Salvare locală**: premiile și stocurile rămân salvate pe dispozitiv între deschideri.

**Logica de extragere**: la fiecare START se alege aleatoriu un premiu dintre cele cu stoc > 0; stocul ales scade cu 1.

## Grafica

- `www/assets/bg_start.jpg` — ecranul de start (grafica originală).
- `www/assets/bg_clean.jpg` — același fundal, cu butonul START eliminat curat, peste care aplicația desenează reel-ul. Logo-ul și titlul din grafică rămân intacte.
- Aplicația folosește un „stage" 16:9 care **nu distorsionează** niciodată grafica: pe ecrane cu alt raport apar benzi laterale în albastru Pepsi, iar reel-ul rămâne aliniat fix pe poză.

## Cum obții APK-ul

1. Creează un repository nou pe GitHub.
2. Urcă tot conținutul acestui folder (inclusiv `.github` și `www/assets`).
3. La push pe `main` (sau manual din **Actions → Build Android APK → Run workflow**) se construiește APK-ul.
4. Descarcă artefactul **`pepsi-house-debug-apk`** din rularea respectivă și instalează-l pe tabletă/telefon (activează „Surse necunoscute").

Orientarea e blocată automat pe **landscape** (grafica e 16:9).

## De personalizat înainte de eveniment

- Parola de admin (`admin123`) — în `www/index.html`, constanta `ADMIN_PWD`.
- Premiile inițiale — `INITIAL_PRIZES` în `www/index.html` (sau direct din Admin pe dispozitiv).
- Pentru Google Play e nevoie de un APK/AAB **release** semnat (pas separat); pentru sideload la activare, varianta debug e suficientă.
