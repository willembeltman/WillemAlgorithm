# 📊 Player Ranking Calculator

## Een relationeel ranking-algoritme voor games, competities en simulaties

Dit project bevat een algoritme dat spelers beoordeelt op basis van hun onderlinge resultaten. In plaats van enkel “win/loss”-statistieken te gebruiken, kijkt dit algoritme ook naar indirecte relaties tussen spelers.
Dat maakt het bijzonder geschikt voor situaties waar spelers elkaar niet allemaal even vaak direct tegenkomen.

Bijvoorbeeld:

- Als A wint van B, en B wint van C, dan krijgt A ook indirect krediet ten opzichte van C.
- Het algoritme berekent deze relaties volledig automatisch, normaliseert scores en bepaalt uiteindelijke ranks.

# ✨ Features

✔️ Directe scores op basis van onderlinge wedstrijden

✔️ Indirecte scores via “common opponents”

✔️ Automatische normalisatie tussen -1 en +1

✔️ Eerlijke ranking op basis van geaggregeerde relatieve sterkte

✔️ Geen externe packages – puur C#

✔️ Geschikt voor simulaties, toernooien, AI-bots of matchmaking

# 🔧 Hoe werkt het?

Voor iedere speler wordt een subscore berekend tegen alle andere spelers:

## 1️⃣ Direct score

Op basis van Win/Loss tegen een specifieke tegenstander:

	score = (wins / (wins + losses)) * 2 - 1

Geeft een waarde tussen -1 (altijd verloren) en +1 (altijd gewonnen).

## 2️⃣ Indirect score

Wanneer twee spelers niet vaak direct spelen:

- Het algoritme zoekt naar derde spelers die wel tegen beiden gespeeld hebben.
- Via deze “alternatieve routes” wordt een relatieve score berekend.

## 3️⃣ Normalisatie

Per speler worden alle subscores geschaald, zodat extremen eerlijk worden uitgesmeerd.

## 4️⃣ Eindscores & ranking

- De totale score van een speler is het gemiddelde van alle subscores waarin hij/zij voorkomt.
- Spelers worden gesorteerd van hoog naar laag.
- Gelijke scores krijgen dezelfde rank.

# 📦 Interfaces
## IPlayer

Bevat ID, Score, Rank en RankDate.

## IGame

Bevat WinnerId en LoserId.

## Calculator

De hoofdklasse die:

- alle direct/indirect scores berekent,
- normaliseert,
- ranks bepaalt.

# 🧠 Waarom dit algoritme?

In veel competities is niet iedereen op dezelfde manier verbonden.
Dit algoritme vangt dat op door:

- relatieve sterkte mee te nemen
- indirecte informatie slim te gebruiken
- ruis te verminderen door averages
- geen ELO-inflatie problemen te hebben
- geen sequentieel systeem te zijn (alle data in 1 calculatie)

Het is vooral handig voor:

- toernooien met onvolledige speelschema’s
- AI-bots die elkaar wisselend spelen
- leaderboard systemen waar eerlijkheid belangrijk is
- correlatie-analyse tussen entiteiten (niet alleen spelers)

# ▶️ Gebruik

	var calculator = new Calculator(players, games);
	calculator.Calculate();

	// Na afloop:
	var rank = player.Rank;
	var score = player.Score;