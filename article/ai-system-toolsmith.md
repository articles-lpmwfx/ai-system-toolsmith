---
title: "AI as System Toolsmith"
subtitle: "From GUI to Intentional Automation"
author: "lpmwfx, Denmark, EU"
date: "20.02.2026"
lang: en
---

# AI som System-Toolsmith

## Fra GUI til Intentionel Automation

I årtier har grafiske brugerflader (GUI) været den primære måde mennesker interagerer med operativsystemer på. CLI har været for de tekniske, og scripting for de få. Med fremkomsten af moderne AI-agenter ændrer dette sig fundamentalt.

AI er ikke blot en chatbot eller en kodegenerator. Den kan fungere som en systemoperatør – men endnu vigtigere: som en toolsmith.

Denne artikel beskriver en praktisk og skalerbar model for at bruge AI som systemhjælper ved at automatisere alt gennem små, loggede, idempotente værktøjer.

---

## Grundidéen: Automatisér alt

I stedet for at lade AI direkte manipulere systemet, beder vi AI om at:

1. Skrive små scripts (Python eller JavaScript)
2. Placere dem i en struktureret service-mappe
3. Udføre dem med fuld logging
4. Dokumentere ændringer

Resultatet er en voksende lokal værktøjskasse.

AI handler ikke længere "magisk". Den producerer konkrete artefakter.

---

## Services-strukturen

Et simpelt, skalerbart mønster:

```
services/
  backup/
  bitwarden/
  sudo-faceid/
  audio/
```

Hver service fungerer som et isoleret domæne. Inden for hver service kan følgende struktur anvendes:

```
services/<domæne>/
  tools/
  conf/
  data/
  state/
  logs/
  README.md
```

Dette giver:

- Lokal kontekst
- Isoleret ændringsområde
- Let fejlfinding
- Reproducerbarhed

---

## Wrapper-arkitekturen

AI instrueres i at bygge tre standard-kommandoer for enhver service:

- `status` – Læser systemtilstand
- `apply` – Udfører ændringer
- `logs` – Indsamler relevante logs

Disse små wrappers fungerer som adaptere mellem:

- GUI-applikationer
- DBus
- systemd
- Konfigurationsfiler
- Services uden CLI

Wrapperen giver stdio, selv hvis appen aldrig havde det.

---

## Hvorfor stdout/stderr er centralt

AI fungerer bedst når:

- Output er deterministisk
- Fejl kan parses
- Status kan verificeres

Derfor bør alle tools:

- Logge alt
- Have `--dry-run`
- Være idempotente
- Skrive en rapport efter kørsel

Eksempel på rapportindhold:

- Hvad blev ændret
- Hvilke filer blev modificeret
- Hvilke kommandoer blev kørt
- Hvordan rulles ændringen tilbage

---

## Reversibilitet som sikkerhedsmodel

Traditionel sikkerhed fokuserer på at forhindre ændringer.

Denne model fokuserer på:

- Snapshot før ændring
- Logging under ændring
- Hurtig rollback

Når systemet er nemt at genskabe, bliver eksperimentering mulig uden frygt.

---

## AI som Toolsmith

Den vigtigste forskel i denne model er:

AI udfører ikke bare opgaver.

AI bygger værktøjer.

Over tid opstår et lokalt økosystem af små scripts, der:

- Kan køre uden AI
- Kan genbruges
- Kan versioneres
- Kan dokumenteres

AI bliver dermed en accelerator for systemforståelse – ikke en erstatning.

---

## Skalerbarhed

Denne tilgang skalerer fordi:

- Hver service er isoleret
- Værktøjer er små og selvstændige
- Ingen central monolitisk agent styrer alt
- Systemets sandhed bor i filer

Det minder om DevOps-principper anvendt på personlige workstations.

---

## Fra GUI til Intention

GUI handler om klik.
CLI handler om kommandoer.

AI-baseret systemarbejde handler om intentioner.

"Installer og konfigurer lokal Postgres med optimal dev-setup og dokumentér ændringerne."

AI oversætter intentionen til:

- Script
- Logs
- Rapport
- Verifikation

---

## Konklusion

AI bliver først en reel systemhjælper, når alt kan gøres som små, loggede, idempotente kommandoer – også for applikationer der aldrig var designet til CLI.

Ved at automatisere alt og gøre ændringer reversible, kan AI transcendere GUI og fungere som et intentionelt kontrol-lag over operativsystemet.

Det kræver ikke et nyt operativsystem.

Det kræver blot struktur, disciplin og en mappe kaldet services.
