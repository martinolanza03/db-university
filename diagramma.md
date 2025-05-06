# Modello Entità-Relazione per Database Universitario

## Descrizione delle Entità e Relazioni

### Entità Principali

#### **DIPARTIMENTI**
- **Identificatore**: `id_dipartimento` (PK)
- **Attributi**:
  - `nome`: Nome del dipartimento (es: "Informatica")
  - `descrizione`: Descrizione testuale
  - `sede`: Edificio principale
  - `telefono`: Recapito telefonico
  - `email`: Contatto istituzionale
- **Relazione**: Offre molti CORSI DI LAUREA (1-N)

#### **CORSI DI LAUREA**
- **Identificatore**: `id_corso_laurea` (PK)
- **Attributi**:
  - `nome`: Nome completo (es: "Ingegneria Informatica")
  - `descrizione`: Presentazione del corso
  - `durata_anni`: Durata in anni (2, 3, 5...)
- **Relazioni**:
  - Appartiene a un DIPARTIMENTO (N-1)
  - Comprende molti CORSI (1-N)

#### **CORSI**
- **Identificatore**: `id_corso` (PK)
- **Attributi**:
  - `nome`: Nome esame (es: "Basi di Dati")
  - `codice`: Codice identificativo (es: "INF-101")
  - `crediti`: CFU (Crediti Formativi Universitari)
  - `descrizione`: Programma didattico
  - `anno_erogazione`: Anno di frequenza (1°, 2°...)
- **Relazioni**:
  - Appartiene a un CORSO DI LAUREA (N-1)
  - Insegnato da molti INSEGNANTI (N-M tramite INSEGNAMENTO)
  - Ha molti APPELLI ESAME (1-N)

#### **INSEGNANTI**
- **Identificatore**: `id_insegnante` (PK)
- **Attributi**:
  - `nome`: Nome
  - `cognome`: Cognome
  - `email`: Contatto elettronico (UNIQUE)
  - `telefono`: Recapito personale
- **Relazioni**:
  - Assegnato a un DIPARTIMENTO (N-1)
  - Insegna molti CORSI (N-M tramite INSEGNAMENTO)

#### **STUDENTI**
- **Identificatore**: `id_studente` (PK)
- **Attributi**:
  - `matricola`: Codice univoco (UNIQUE)
  - `nome`: Nome
  - `cognome`: Cognome
  - `data_nascita`: Data di nascita
  - `email`: Contatto istituzionale
  - `telefono`: Recapito personale
- **Relazioni**:
  - Iscritto a un CORSO DI LAUREA (N-1)
  - Partecipa a molti APPELLI ESAME (N-M tramite ISCRIZIONI ESAMI)

#### **APPELLI ESAME**
- **Identificatore**: `id_appello` (PK)
- **Attributi**:
  - `data_esame`: Data e ora della prova
  - `luogo`: Aula/laboratorio
  - `tipo_appello`: Modalità (Scritto/Orale)
  - `descrizione`: Eventuali note
- **Relazioni**:
  - Associato a un CORSO (N-1)
  - Ha molti STUDENTI iscritti (N-M tramite ISCRIZIONI ESAMI)

## Cardinalità delle Relazioni

| Relazione                     | Tipo   | Descrizione |
|-------------------------------|--------|-------------|
| Dipartimento → Corsi di Laurea | 1 a N  | Ogni dipartimento offre più corsi di laurea, ma ogni corso di laurea appartiene a un solo dipartimento |
| Corso di Laurea → Corsi       | 1 a N  | Ogni corso di laurea comprende più esami, ma ogni esame appartiene a un solo corso di laurea |
| Insegnanti ↔ Corsi            | N a M  | Un insegnante può insegnare più corsi e un corso può avere più insegnanti (gestito da INSEGNAMENTO) |
| Corsi → Appelli Esame         | 1 a N  | Ogni corso ha più sessioni d'esame, ma ogni appello è associato a un solo corso |
| Studenti → Corso di Laurea    | N a 1  | Molti studenti sono iscritti a un corso di laurea, ma ogni studente è iscritto a un solo corso |
| Studenti ↔ Appelli Esame      | N a M  | Uno studente può iscriversi a più appelli e un appello può avere più studenti iscritti (gestito da ISCRIZIONI ESAMI) |
