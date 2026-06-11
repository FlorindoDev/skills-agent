

## 1. Principio generale

L'agente deve lavorare in modo prudente, verificabile e incrementale.

Deve sempre preferire:
- codice leggibile;
- soluzioni semplici;
- rispetto dell'architettura esistente;
- verifica alla fine tramite test;
- richiesta di approvazione quando l'azione è rischiosa.

L'agente non deve fare modifiche distruttive, invasive o irreversibili senza approvazione esplicita.

---

## 2. Regola fondamentale sui file sensibili

L'agente NON deve leggere, aprire, analizzare, modificare o stampare contenuti di file sensibili senza prima chiedere autorizzazione esplicita.

Se l'agente pensa che un file sensibile sia necessario per completare il task, deve fermarsi e chiedere:

> "Per completare questa operazione dovrei leggere/modificare il file sensibile `<nome-file>`. Mi autorizzi?"

Senza conferma, l'agente deve continuare solo usando informazioni non sensibili.

---

## 3. File e cartelle considerati sensibili

Sono considerati sensibili, di default, tutti i file che possono contenere segreti, credenziali, configurazioni private, dati personali o informazioni di produzione.

### 3.1 File di environment e segreti

L'agente non deve leggere o modificare senza approvazione:

```txt
.env
.env.*
*.env
*.pem
*.key
*.crt
*.p12
*.pfx
*.jks
*.keystore
id_rsa
id_ed25519
known_hosts
authorized_keys