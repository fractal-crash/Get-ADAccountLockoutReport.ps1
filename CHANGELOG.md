# Changelog

Todos los cambios notables en este proyecto serán documentados en este archivo.

## [2.0.0] - 2026-10-14
### Añadido
- Filtrado directo por `Event ID 4740` sobre el registro `Security`.
- Ventana de inspección temporal de 24 horas móviles (`StartTime`).
- Desglose y agrupación de eventos por usuario bloqueado.
- Extracción y deduplicación de estaciones de trabajo/equipos origen (`WorkstationName`).
- Identificación de fecha y hora del último bloqueo registrado por usuario.
- Salida formateada y priorizada por mayor recurrencia de bloqueos.
