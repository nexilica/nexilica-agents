# Python GUI Specialist Agent - Guida all'uso

## File Creati

- `python-gui-specialist.md` - Configurazione completa dell'agent

## Come Utilizzare l'Agent

### Metodo 1: Invocazione Diretta

Puoi invocare l'agent direttamente nelle tue conversazioni con Claude Code usando:

```
/python-gui-specialist
```

Questo attiverà l'agent specializzato che seguirà tutte le regole definite.

### Metodo 2: Invocazione Automatica

Claude Code può invocare automaticamente questo agent quando:
- Parli di sviluppo Python
- Menzioni GUI o scripting
- Chiedi di creare o modificare codice Python

### Metodo 3: Generazione con Claude (Consigliato per personalizzazioni)

Se vuoi modificare o rigenerare l'agent:

1. Esegui `/agents` in Claude Code
2. Seleziona "generate with claude (recommended)"
3. Descrivi le modifiche che vuoi apportare
4. Claude genererà una nuova versione

## Funzionalità Principali

### 1. Gestione Automatica di sw_context.md

L'agent crea e mantiene automaticamente un file `sw_context.md` che documenta:
- Struttura del progetto (folder tree)
- Funzionalità implementate
- Dettagli di implementazione passo-passo
- Dipendenze e librerie utilizzate
- Change log delle modifiche

### 2. Proposta Librerie

Quando non specifichi una libreria, l'agent:
- Si ferma prima di scrivere codice
- Propone 2-4 opzioni con pro/contro
- Aspetta la tua conferma
- Procede solo dopo la tua scelta

### 3. Uso Esclusivo di Librerie Specificate

Quando specifichi una libreria:
- L'agent la usa senza proporre alternative
- Non suggerisce librerie diverse
- Si concentra sulla migliore implementazione con quella libreria

### 4. Contestualizzazione Codice Esistente

Al primo utilizzo in un progetto:
- Legge tutto il codice Python esistente
- Crea `sw_context.md` se non esiste
- Documenta tutto il contesto del progetto
- Si integra con il codice esistente

## Esempi di Utilizzo

### Esempio 1: Nuovo Progetto GUI

```
User: Voglio creare una GUI per gestire una lista di task

Agent: Ti propongo le seguenti librerie per la GUI:

1. **tkinter** (Built-in)
   - Vantaggi: Già incluso in Python, cross-platform
   - Svantaggi: Aspetto meno moderno

2. **PyQt6**
   - Vantaggi: Aspetto professionale, molti widget
   - Svantaggi: Licenza GPL, dimensioni maggiori

3. **CustomTkinter**
   - Vantaggi: Moderno, basato su tkinter
   - Svantaggi: Community più piccola

Quale preferisci?
```

### Esempio 2: Libreria Specificata

```
User: Crea uno script per analizzare file CSV usando pandas

Agent: [Inizia subito a scrivere il codice usando pandas]
       [Crea/aggiorna sw_context.md con i dettagli]
```

### Esempio 3: Progetto Esistente

```
User: [Prima invocazione in un progetto con codice Python esistente]

Agent: Ho trovato codice Python esistente. Sto leggendo i file...
       Ho creato sw_context.md con la documentazione del progetto attuale.
       Cosa vuoi che faccia?
```

## Regole dell'Agent

L'agent segue queste regole rigide:

1. ✅ Usa **SOLO Python 3.10+**
2. ✅ **SEMPRE** aggiorna `sw_context.md` dopo modifiche al codice
3. ✅ **SEMPRE** propone opzioni se non specifichi una libreria
4. ✅ **MAI** propone alternative se specifichi una libreria
5. ✅ **SEMPRE** legge il codice esistente prima di modificarlo
6. ✅ **SEMPRE** contestualizza codice esistente in `sw_context.md`

## Struttura di sw_context.md

L'agent mantiene questa struttura nel file di contesto:

```markdown
# Project Context Documentation

## Project Overview
[Descrizione del progetto]

## Folder Tree
[Struttura directory con descrizioni]

## Core Functionality
[Funzionalità principali]

## Implementation Details
### [Nome Componente]
- **Purpose**: Scopo del componente
- **Implementation**: Come è implementato
- **Dependencies**: Librerie necessarie
- **Key Functions/Classes**: Elementi importanti

## Change Log
### [Data] - [Componente]
- Modifiche effettuate
- Motivazione delle modifiche
```

## Best Practices

### Quando Invocare l'Agent

- All'inizio di ogni nuovo progetto Python
- Quando aggiungi nuove funzionalità
- Quando modifichi codice esistente
- Quando vuoi documentazione automatica

### Comunicare con l'Agent

**Chiaro e Specifico:**
```
✅ "Crea una GUI per visualizzare grafici usando matplotlib"
✅ "Aggiungi gestione errori al file main.py"
```

**Da Evitare:**
```
❌ "Migliora il codice" (troppo vago)
❌ "Crea qualcosa di interessante" (non specifico)
```

**Specificare Librerie:**
```
✅ "Usa PyQt6 per creare la finestra principale"
✅ "Implementa con tkinter"
```

**Lasciare Scegliere l'Agent:**
```
✅ "Crea uno script per leggere file Excel" (agent proporrà openpyxl, pandas, xlrd)
```

## Risoluzione Problemi

### L'agent non si attiva automaticamente

- Usa invocazione diretta: `/python-gui-specialist`
- Verifica che il file sia in `.claude/agents/`

### sw_context.md non viene creato

- Verifica che l'agent abbia permessi di scrittura
- Controlla che `permissionMode: acceptEdits` sia impostato

### L'agent propone librerie quando non dovrebbe

- Assicurati di specificare chiaramente la libreria nel tuo messaggio
- Esempio: "Usa [libreria] per..."

## Personalizzazione

Per modificare il comportamento dell'agent:

1. Apri `.claude/agents/python-gui-specialist.md`
2. Modifica la sezione YAML in alto per cambiare:
   - `tools`: Strumenti disponibili all'agent
   - `model`: Modello da usare (sonnet, opus, haiku)
   - `permissionMode`: Livello di permessi
3. Modifica il contenuto markdown per cambiare:
   - Workflow e regole
   - Struttura di sw_context.md
   - Linee guida Python

## Supporto

Per problemi o domande:
- Consulta la documentazione ufficiale: https://code.claude.com/docs/en/sub-agents.md
- Usa `/help` in Claude Code
- Chiedi direttamente a Claude Code di spiegare il comportamento dell'agent

---

**Versione Agent**: 1.0
**Python Supportato**: 3.10+
**Data Creazione**: 2025-11-21
