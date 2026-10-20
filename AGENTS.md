# AGENTS.md — Paxwise

Planner voor Airlines Manager Professional. Eén bestand, geen build.

## Waar werken
- Werk alleen in `index.html` (Productie, tyko91.github.io/Paxwise/).
- `test/index.html` is een bewuste tweede versie (Testomgeving). Alleen aanpassen als de gebruiker daarom vraagt.
- Niet doen: `AM_Routevuller.html`, xlsx-bestanden, IATA-uitbreidingen, rebuilds.
- Eén commit = één gevraagde wijziging.

## Data (`data/`)
- `fleet.json`: `{updated, source, count, hubs, aircraft[]}`.
  `aircraft[]`: `{id, name, type, hub, seatsY, seatsJ, seatsF, cargo}`.
- `routes.json`: `{updated, source, count, routes[]}`.
  `routes[]`: `{id, route, from, to, km, qY, qJ, qF, qC, lockRoute, lockAsk, retByType{type:"hh:mm"}, useTypes[], planPath, fleet[]}`.
  `fleet[]`: `{name, type, wk, start, y, j, f, c, status:"on"|"off", warn}`.
- `schedules.json`: `{updated, source, read_only, count, routes_for_paxwise[], aircraft[], notes}`.
  `aircraft[]`: `{id, name, type, hub, use_pct, schedule_date, flights_today[{from, to, departure, arrival, passengers, ...}]}`.
  Wordt nu niet door `index.html` geladen.
- `index.html` leest `fleet.json` en `routes.json` en bewaart lokaal in localStorage (keys `am_*`). Nieuwe seed nodig? Hoog de versie in de key op.

## Controle na elke wijziging
1. Pagina laadt zonder consolefouten.
2. Alle JSON in `data/` is geldig.
3. Hoofdschermen werken: vloot, routes, rooster.

De GitHub Action `.github/workflows/check.yml` controleert punt 2 en de JS-syntax.
