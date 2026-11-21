La simulación no debe ser un pipeline lineal.

   En realidad parece más adecuado algo así:

   ```text
                      ┌─────────────┐
                      │   Actions   │
                      └──────┬──────┘
                             │
                             ▼
                      ┌─────────────┐
                      │   Events    │
                      └──────┬──────┘
                             │
             ┌───────────────┼───────────────┐
             ▼               ▼               ▼
      Situations      Observations      Logs/Record
             │               │
             └───────┬───────┘
                     ▼
              Agent Reasoning
                     │
             ┌───────┴────────┐
             ▼                ▼
       New Actions     Interventions
             │                │
             └────────┬───────┘
                      ▼
                   Outcomes
   ```

   donde un mismo evento puede:
   - crear una situación,
   - producir varias observaciones,
   - no producir ninguna,
   - generar acciones distintas según quién lo observe.

---
