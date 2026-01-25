
### La concursurile individuale… fiecare jucător să apară pe poziții cu un Nr de la 1 la 8
Aici e alt format de competiție: Individual duplicate.
Implicații:
- nu mai ai “Axis fix (doi jucători împreună)” pe tot concursul
- perechile se schimbă; fiecare jucător joacă cu alți parteneri
- ranking-ul final e pe Player, nu pe Axis
➡️ Asta cere un “mode switch” în model:
GameType = PAIRS | INDIVIDUAL
dacă e INDIVIDUAL: Player devine obligatoriu, iar Axis devine derivat “pentru board-ul ăsta, North+South formează NS”.

Chiar și pentru Pairs, dacă vrei “poziția fiecărui jucător”, atunci ai nevoie de:
- Player (măcar ca ID + nume/număr)
- Seating pe fiecare rezultat (N/E/S/W)
Axis poate rămâne (pentru concursuri pe perechi), dar seating-ul îți dă granularitatea.
 Here’s the simplest path to add IMP scoring:

  - Add an ImpCalculator in core (score difference → IMP table).
  - Extend ScoringMode with TEAMS_IMP.
  - Add team structures: Team(id, name, pairNS, pairEW) or Team(id, name, players[4]).
  - Results for teams: store both table scores per board (open/closed room) or two results per board and compute the diff.
  - Rankings: sum IMPs per team.

  If you want, I can start by adding the IMP calculator + scoring mode, then we can wire teams/UI after.



Concursuri pe Matchpoints (MP)
Cum se numesc

Duplicate Pairs

Pair Tournaments

Open Pairs / Mixed Pairs / Ladies Pairs

Club Pairs

Caracteristici

Concurs de perechi

Fiecare board este comparat cu toate celelalte mese

Clasamentul este:

în MP

sau aproape întotdeauna afișat în %

Oficial

✔️ Cel mai răspândit format la nivel de club și turnee de o zi

2️⃣ Concursuri pe IMP
Cum se numesc

Teams

Swiss Teams

Knock-Out (KO)

League / Round-robin Teams

Caracteristici

Concurs pe echipe (4–6 jucători)

Se compară două mese (open vs closed)

Diferența de scor → IMP

Oficial

✔️ Standardul absolut pentru competiții pe echipe
✔️ Folosit la:

Campionate naționale

Campionate europene

Campionate mondiale

3️⃣ Concursuri în %
Important (clarificare cheie)

❗ NU există concursuri „pe %” ca sistem de punctare de bază

👉 % este doar o formă de afișare, nu un sistem primar.

De unde vine %

din MP (cel mai frecvent)

uneori din VP / IMP (clasamente sintetice)

Exemple de afișare

„Ai obținut 62.3%”

„Top = 100%, average = 50%”

🧾 Sinteză clară
Sistem	Tip concurs	Denumire uzuală	Ce joacă
MP	Pairs	Duplicate Pairs	perechi
IMP	Teams	Swiss / KO / League	echipe
%	—	doar afișare	derivat
🧠 Regula de aur (oficială)

🔹 MP → perechi
🔹 IMP → echipe
🔹 % → prezentare, nu competiție