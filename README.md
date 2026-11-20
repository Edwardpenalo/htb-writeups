# Hack The Box — Red & Blue Team Write-ups

![Write-ups](https://img.shields.io/badge/write--ups-[N]-green)
![Red Team](https://img.shields.io/badge/red%20team-pentesting-red)
![Blue Team](https://img.shields.io/badge/blue%20team-DFIR%20%2F%20SOC-blue)
![MITRE ATT&CK](https://img.shields.io/badge/mapped%20to-MITRE%20ATT%26CK-orange)

**EN:** Write-ups of retired Hack The Box machines (red team: web/AppSec and system pentesting) and Sherlocks (blue team: DFIR/SOC). Each write-up includes the attack/incident chain, MITRE ATT&CK mapping, **detection ideas and remediation**. No flags or credentials are published.

**ES:** Write-ups de máquinas retiradas (red team) y Sherlocks (blue team) de Hack The Box. Cada uno incluye la cadena de ataque o incidente, mapeo a MITRE ATT&CK, **detección y remediación**.

> Solo contenido retirado. Sin flags, contraseñas ni hashes.

## Por qué este repo
Documento cada caso con enfoque **Purple Team**: no solo cómo se explota, sino cómo se detecta y se corrige.

## Red Team — `red-team/`
| Máquina | OS | Dificultad | Vulnerabilidad clave (OWASP/CWE) | Técnicas ATT&CK | Herramientas | Write-up |
|---|---|---|---|---|---|---|
| [Nombre] | Linux | Easy | [ej. IDOR / CWE-639] | [T1190, T1068] | nmap, Burp | [Ver](red-team/nombre/README.md) |

## Blue Team — `blue-team/`
| Sherlock | Tema | Dificultad | Hallazgos | Técnicas ATT&CK | Herramientas | Write-up |
|---|---|---|---|---|---|---|
| [Nombre] | [ej. compromiso de DC] | Medium | [persistencia, exfiltración] | [T1053, T1048] | Event Viewer, Wireshark | [Ver](blue-team/nombre/README.md) |

## Detecciones — `detections/`
Reglas Sigma y consultas KQL derivadas de los casos. *(opcional, cuando las tengas)*

## Estructura de cada write-up
1. Resumen ejecutivo (EN/ES, 3 líneas)
2. Reconocimiento / evidencias
3. Cadena de ataque o línea de tiempo
4. Detección y remediación
5. Lecciones aprendidas

## Hacia dónde voy
HTB CBBH · SC-500 · Proyecto [Sentinel](enlace): SAST + correlación de CVEs con IA.

## Contacto
[LinkedIn](https://www.linkedin.com/in/edward-penalo/)
