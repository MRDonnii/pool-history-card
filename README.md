# Pool History Card

To beslægtede kort i én fil:

- **`pool-history-card`** — graf over høj/lav vandtemperatur og sandfilter-køretid over de sidste N dage.
- **`pool-water-quality-card`** — pH/klor-vandkvalitetshistorik, én måling om dagen (seneste test for dagen bruges hvis der er flere).

```yaml
type: custom:pool-history-card
title: Pooltemperatur
subtitle: Høj/lav vandtemperatur og sandfilter
temp_entity: sensor.pool_vandtemperatur
pump_entity: sensor.poolpumpe_koeretid_i_dag
days: 7
```

```yaml
type: custom:pool-water-quality-card
title: Vandkvalitet
subtitle: En måling pr. dag · seneste test bruges
ph_entity: input_number.pool_ph_vaerdi
chlorine_entity: input_number.pool_klor_vaerdi
ph_history_entity: sensor.pool_ph_maaling
chlorine_history_entity: sensor.pool_klor_maaling
measured_entity: sensor.pool_sidste_vandmaling_visning
days: 7
```

## Config — pool-history-card

| Felt | Type | Standard |
|---|---|---|
| `title` / `subtitle` | tekst | "Pooltemperatur" / "Høj/lav vandtemperatur og sandfilter" |
| `temp_entity` | entity-id | `sensor.pool_vandtemperatur` |
| `pump_entity` | entity-id | `sensor.poolpumpe_koeretid_i_dag` |
| `days` | tal | 7 |

## Config — pool-water-quality-card

| Felt | Type | Standard |
|---|---|---|
| `ph_entity` / `chlorine_entity` | entity-id | `input_number.pool_ph_vaerdi` / `input_number.pool_klor_vaerdi` (nuværende værdi til manuel indtastning) |
| `ph_history_entity` / `chlorine_history_entity` | entity-id | `sensor.pool_ph_maaling` / `sensor.pool_klor_maaling` (historiske målinger) |
| `legacy_measured_entity` | entity-id | `input_datetime.pool_sidste_vandmaaling` |
| `measured_entity` | entity-id | `sensor.pool_sidste_vandmaling_visning` |
| `imported_measurements` | array | `[{date, ph, chlorine}, ...]` — brug til at seede historik du ikke har en sensor for endnu |
| `days` | tal | 7 |

Historikken hentes via recorder for de entiteter der findes; `imported_measurements` er tænkt som et engangs-suppleret datasæt (fx manuelt loggede målinger fra før du havde sensorer på plads).

## Installation

1. Kopiér `pool-history-card.js` til `/config/www/`.
2. Tilføj som Lovelace-resource: `/local/pool-history-card.js?v=1`, type `module`.
3. Tilføj det ene eller begge kort med dine egne entiteter.
