# Auditoría de Bloqueos de Cuentas en Active Directory (`Auditoria-BloqueosAD.ps1`)

Herramienta ligera en PowerShell diseñada para administradores de sistemas y analistas de ciberseguridad para identificar, auditar y rastrear de forma proactiva bloqueos de cuentas en entornos corporativos de **Active Directory** (Event ID 4740).

---

## Características

* **Filtrado Eficiente:** Utiliza `Get-WinEvent` con hashtable sobre el registro de eventos `Security`, optimizando el consumo de CPU y memoria en Controladores de Dominio (DCs).
* **Ventana Móvil:** Evalúa por defecto los bloqueos ocurridos en las últimas 24 horas (`(Get-Date).AddDays(-1)`).
* **Correlación de Identidad y Origen:** Extrae y deserializa las propiedades del evento 4740:
  * `Properties[0]`: Nombre de la cuenta de usuario afectada (*TargetUserName*).
  * `Properties[1]`: Nombre de host/equipo origen solicitante (*TargetDomainName* / *WorkstationName*).
* **Agrupación y Priorización:** Agrupa ocurrencias por usuario, deduplica equipos origen y ordena descendentemente por cantidad de incidentes para detectar ataques de fuerza bruta, bloqueos cíclicos o credenciales cacheadas desactualizadas.

---

## Requisitos de Ejecución

* **Rol / Permisos:** Ejecución con privilegios de Administrador del Dominio o permisos delegados de lectura sobre el visor de eventos de seguridad (`Audit and Security Log` privilege).
* **Entorno:** Ejecución preferente en un Controlador de Dominio (PDC Emulator recomendado para capturar todos los bloqueos centralizados) o estación de trabajo con RSAT / conectividad RPC y WinRM hacia los DCs.
* **PowerShell:** PowerShell 5.1 o PowerShell 7+.

---

## Uso

Ejecuta el script directamente desde una consola elevada de PowerShell:

```powershell
.\Auditoria-BloqueosAD.ps1
```

### Salida de Ejemplo

```text
Usuario       CantidadBloqueos UltimoBloqueo        EquiposOrigen
-------       ---------------- -------------        -------------
jrodriguez                  14 14/10/2026 15:42:10  WS-FIN-014, SRV-APP-02
mgarcia                      3 14/10/2026 11:20:05  WS-OPER-101
alopez                       1 14/10/2026 09:12:44  VPN-GW-01
```

---

## Estructura del Repositorio

```text
├── .github/
│   └── workflows/
│       └── psscriptanalyzer.yml
├── .gitignore
├── Auditoria-BloqueosAD.ps1
├── CHANGELOG.md
├── LICENSE
├── README.md
└── SECURITY.md
```

---

## Licencia

Distribuido bajo la licencia [MIT](LICENSE).
