# Context Validator Agent - Guida all'uso

## File Creati

- `context-validator.md` - Configurazione completa dell'agent

## Come Utilizzare l'Agent

### Metodo 1: Invocazione Diretta

Puoi invocare l'agent direttamente nelle tue conversazioni con Claude Code usando:

```
/context-validator
```

Questo attiverà l'agent specializzato che seguirà tutte le regole definite.

### Metodo 2: Invocazione Automatica

Claude Code può invocare automaticamente questo agent quando:
- Hai generato un nuovo report o documento markdown
- Vuoi verificare l'accuratezza di documentazione esistente
- Menzioni la necessità di validare contenuti contro CLAUDE.md
- Chiedi di controllare la consistenza della documentazione

### Metodo 3: Generazione con Claude (Consigliato per personalizzazioni)

Se vuoi modificare o rigenerare l'agent:

1. Esegui `/agents` in Claude Code
2. Seleziona "generate with claude (recommended)"
3. Descrivi le modifiche che vuoi apportare
4. Claude genererà una nuova versione

## Funzionalità Principali

### 1. Validazione Accuratezza Tecnica

L'agent verifica che i documenti contengano informazioni tecniche corrette:
- Specifiche hardware (tipi di sensori, microcontroller, protocolli)
- Descrizioni prodotto accurate (temperatura vs distanza, analogico vs digitale)
- Riferimenti corretti a repository GitHub
- Mappatura corretta dei nomi dei contributor

### 2. Controllo Conformità Linee Guida

Verifica che i documenti seguano le regole stabilite in CLAUDE.md:
- **Product Description Guidelines**: Evita descrizioni generiche di business applications
- **ProKASRO Context**: Assicura che i prodotti siano descritti nel contesto della robotica per riabilitazione fognaria
- **Report Standards**: Controlla formato, naming conventions, effort estimates
- **Technical Accuracy**: Verifica accuratezza di specifiche tecniche e terminologia

### 3. Report di Validazione Strutturati

Genera report markdown completi con:
- **Executive Summary**: Panoramica delle discrepanze trovate
- **Critical Errors**: Errori che devono essere corretti immediatamente
- **Medium Priority Issues**: Problemi che dovrebbero essere risolti
- **Low Priority Observations**: Suggerimenti per miglioramenti minori
- **Compliance Summary**: Checklist di conformità per area
- **Recommendations**: Azioni prioritizzate per migliorare la qualità

### 4. Categorizzazione Priorità

L'agent classifica i problemi in tre livelli:

**CRITICAL** (devono essere corretti):
- Specifiche tecniche errate
- Applicazioni business generiche che violano le linee guida
- Repository o URL GitHub sbagliati
- Mappatura nomi contributor errata
- Errori fattuali su funzionalità prodotti

**MEDIUM** (dovrebbero essere corretti):
- Terminologia inconsistente
- Deviazioni dal formato stabilito
- Descrizioni incomplete di prodotti
- File naming non conforme

**LOW** (nice to fix):
- Inconsistenze stilistiche minori
- Opportunità per maggiore chiarezza
- Dettagli opzionali mancanti

## Esempi di Utilizzo

### Esempio 1: Validazione Report Appena Generato

```
User: Ho appena generato il report IROS_Report_2025-01-01_to_2025-10-31.md.
      Puoi controllare che sia tutto corretto?

Agent: Let me use the context-validator agent to review this report
       against CLAUDE.md and identify any discrepancies.

[Agent analizza il report e genera un validation report che evidenzia:]
- Descrizione errata del sensore (IROS come distance sensor invece di temperature)
- Applicazioni generiche non appropriate per prodotto ProKASRO
- Nomi contributor da mappare correttamente
- Formato report conforme
```

### Esempio 2: Validazione Proattiva Dopo Generazione

```
User: Crea il report per CameraBrain da 2025-09-01 a 2025-11-12.

Agent: [Genera il report usando github-extractor]
       Report generated successfully. Now let me validate it against
       CLAUDE.md to ensure accuracy.

[Usa context-validator automaticamente e segnala eventuali problemi trovati]
```

### Esempio 3: Revisione Batch di Documentazione

```
User: Controlla tutti i report nella cartella CAMUX per vedere se ci
      sono errori rispetto a CLAUDE.md

Agent: I'll use the context-validator agent to systematically review
       all CAMUX reports and identify discrepancies with the canonical context.

[Analizza multipli file e genera report consolidato con tutti i problemi]
```

### Esempio 4: Verifica Documentazione Esistente

```
User: Ho il dubbio che alcuni vecchi report abbiano informazioni sbagliate.
      Puoi controllare?

Agent: [Usa context-validator per analizzare i documenti specificati]
       [Identifica discrepanze come specifiche tecniche datate,
        descrizioni obsolete, repository references incorretti]
```

## Regole dell'Agent

L'agent segue queste regole rigide:

1. ✅ **SEMPRE** legge CLAUDE.md come riferimento canonico
2. ✅ **SEMPRE** classifica i problemi in Critical/Medium/Low priority
3. ✅ **SEMPRE** fornisce citazioni esatte da CLAUDE.md per supportare i findings
4. ✅ **SEMPRE** suggerisce la versione corretta del contenuto errato
5. ✅ **SEMPRE** spiega il PERCHÉ qualcosa è un errore, non solo CHE è sbagliato
6. ✅ **MAI** ignora discrepanze anche minori
7. ✅ **SEMPRE** verifica Product Description Guidelines (focus speciale su applicazioni generiche)
8. ✅ **SEMPRE** controlla accuratezza tecnica (sensor types, protocols, microcontrollers)

## Aree di Focus Speciali

L'agent presta particolare attenzione a:

### 1. Accuratezza Tecnologica Prodotti
- Tipo sensori: temperature vs distance vs pressure
- Tipo camere: analogiche vs digitali
- Protocolli comunicazione: CANOpen, SPI, I2C
- Microcontroller: varianti STM32

### 2. Contesto Applicativo ProKASRO
I prodotti devono essere descritti nel contesto di:
- Robotica per riabilitazione fognaria
- UV liner curing
- Ispezione tubature
- Trenchless repair

**NON** devono includere:
- Automotive safety
- Manufacturing QC
- Traffic monitoring
- Agricultural automation
- Altre applicazioni generiche

### 3. Accuratezza Repository
Verifica nomi corretti repo:
- `nexilica/IROS`
- `nexilica/IRSens-SW`
- `nexilica/CameraSwitch`
- Altri secondo CLAUDE.md

### 4. Mappatura Nomi
- MattiVenturelli/Matti → Mattia Venturelli
- dinamitemic → Michele Gazzarri

## Struttura Validation Report

L'agent genera report con questa struttura:

```markdown
# Context Validation Report
**Date**: [Data corrente]
**Documents Analyzed**: [Lista file revisionati]
**Reference Context**: CLAUDE.md

## Executive Summary
[Numero discrepanze, distribuzione severity, status generale]

## Critical Errors (Must Fix)
### Issue: [Titolo problema]
- **Location**: [File, sezione, riga]
- **Current**: "[Citazione esatta]"
- **Problem**: [Descrizione problema]
- **Should Be**: "[Versione corretta]"
- **Reference**: [Citazione da CLAUDE.md]

## Medium Priority Issues (Should Fix)
[Stessa struttura]

## Low Priority Observations (Nice to Fix)
[Stessa struttura, più conciso]

## Compliance Summary
- ✅/❌ **Product descriptions**: [Status]
- ✅/❌ **Technical accuracy**: [Status]
- ✅/❌ **Naming conventions**: [Status]
- ✅/❌ **ProKASRO context**: [Status]
- ✅/❌ **Report format**: [Status]

## Recommendations
[Lista prioritizzata di azioni]
```

## Best Practices

### Quando Invocare l'Agent

**Sempre dopo:**
- Generazione di nuovi report
- Modifiche a documentazione esistente
- Import/merge di documentazione da altre fonti
- Aggiornamenti a specifiche prodotto

**Periodicamente:**
- Review trimestrale di tutta la documentazione
- Prima di condividere documenti con stakeholder esterni
- Dopo aggiornamenti a CLAUDE.md

### Comunicare con l'Agent

**Chiaro e Specifico:**
```
✅ "Valida il report IROS_Report_2025-01-15.md contro CLAUDE.md"
✅ "Controlla tutti i file nella cartella reports/ per accuratezza"
✅ "Verifica che questo documento segua le Product Description Guidelines"
```

**Da Evitare:**
```
❌ "Controlla se va bene" (troppo vago)
❌ "È corretto?" (specifica cosa controllare)
```

**Per Problemi Specifici:**
```
✅ "Ho il dubbio che le specifiche tecniche di IROS siano sbagliate in questo report"
✅ "Verifica che non ci siano business applications generiche in questo documento"
```

## Risoluzione Problemi

### L'agent non trova CLAUDE.md

- Verifica che CLAUDE.md sia nella root del progetto
- Controlla che il file sia leggibile
- L'agent leggerà automaticamente il file se esiste

### L'agent non categorizza correttamente le priority

- Verifica che CLAUDE.md contenga linee guida chiare
- L'agent usa le regole esplicite in CLAUDE.md per classificare
- Revedi le classificazioni con Claude se necessario

### L'agent è troppo permissivo / troppo rigido

- Modifica le soglie di classificazione nel file agent
- Adatta le regole nella sezione "Critical Errors" del agent config
- Usa la generazione Claude per personalizzare il comportamento

### Report di validazione troppo lunghi

- L'agent è progettato per essere completo e dettagliato
- Considera i report lunghi come segno di molti problemi da risolvere
- Usa l'Executive Summary per una panoramica rapida

## Personalizzazione

Per modificare il comportamento dell'agent:

1. Apri `.claude/agents/context-validator.md`
2. Modifica la sezione YAML in alto per cambiare:
   - `model`: Modello da usare (sonnet consigliato per accuracy)
   - `color`: Colore dell'agent nell'interfaccia
3. Modifica il contenuto markdown per cambiare:
   - Criteri di classificazione Critical/Medium/Low
   - Aree di focus speciali
   - Struttura del validation report
   - Livello di dettaglio nelle spiegazioni

### Aggiungere Nuove Aree di Validazione

Per aggiungere controlli su nuovi aspetti:

1. Aggiorna CLAUDE.md con le nuove linee guida
2. Aggiungi nuova sezione in "Special Focus Areas" del agent config
3. Includi esempi di cosa controllare
4. Specifica la categoria di priority appropriata

## Integrazione con Altri Agent

Context-validator è progettato per lavorare con:

- **github-extractor**: Valida automaticamente i report generati
- **python-specialist**: Verifica che sw_context.md segua le convenzioni
- Altri agent che generano documentazione markdown

## Supporto

Per problemi o domande:
- Consulta la documentazione ufficiale: https://code.claude.com/docs/en/sub-agents.md
- Usa `/help` in Claude Code
- Chiedi direttamente a Claude Code di spiegare il comportamento dell'agent
- Verifica che CLAUDE.md sia aggiornato con tutte le linee guida necessarie

---

**Versione Agent**: 1.0
**Modello**: Sonnet 4.5
**Data Creazione**: 2025-11-21
**Ultima Revisione**: 2025-11-21