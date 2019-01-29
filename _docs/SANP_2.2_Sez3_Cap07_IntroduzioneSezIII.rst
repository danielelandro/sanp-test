**SEZIONE III – SPECIFICHE TECNICHE**

Introduzione 
=============

La presente sezione descrive le interfacce di cooperazione applicativa
del software che implementa i servizi del NodoSPC.

Il NodoSPC definisce le regole di cooperazione tra i due attori (EC e
PSP) del processo di pagamento, i quali sono connessi al NodoSPC per
mezzo di piattaforme software così denominate:

-  **stazioneIntermediarioPA**: rappresenta la piattaforma software
   utilizzata da un Ente Creditore per scambiare i messaggi all’interno
   del sistema pagoPA relativamente ai processi di pagamento di uno o
   più servizi.

-  **Canale**: rappresenta la piattaforma software messa a disposizione
   da un PSP (e connessa al NodoSPC) che realizza un servizio di
   pagamento messo a disposizione dell’utilizzatore finale al fine di
   completare un pagamento verso un Ente Creditore.

Entrambi gli attori possono utilizzare una molteplicità di piattaforme
software per colloquiare con il NodoSPC, in funzione delle proprie
esigenze.

Per la piena comprensione dell’interscambio dei messaggi all’interno del
sistema, si deve tenere presente la possibilità che tra l’attore
principale ed il NodoSPC si interponga un intermediario
(intermediarioPA, intermediarioPSP) a cui l’attore principale ha
demandato il compito di gestire la propria piattaforma software di
interconnessione e rendere disponibili le interfacce verso il NodoSPC.
Nella figura seguente sono rappresentate le varie casistiche possibili.

|C:\Users\mogi\AppData\Local\Microsoft\Windows\INetCache\Content.Outlook\2QI8WBLX\deploymentDiagram.png|

**Figura XX – Diagramma delle connessioni logiche al NodoSPC**

Si definisce quindi:

-  **IntermediarioPA**: il soggetto che opera come intermediario per un
   Ente Creditore. Qualora l’Ente Creditore non si avvalga di un
   intermediario, rappresenta l’Ente Creditore stesso;

-  **IntermediarioPSP**: il soggetto che opera come intermediario per un
   PSP. Qualora il PSP non si avvalga di un intermediario, rappresenta
   il PSP stesso;

-  **StazioneIntermediarioPA**: il sistema software gestito da un
   IntermediarioPA, che si interfaccia direttamente col NodoSPC;

-  **Canale**: il sistema software gestito da un IntermediarioPSP, che
   si interfaccia direttamente al NodoSPC con le modalità previste.

Allo stesso soggetto è consentito di connettersi al NodoSPC in maniera
diversa (diretta o intermediata) in funzione dei servizi offerti.

Nelle descrizioni seguenti si ometterà di fare riferimento a detti
intermediari, in quanto essi non svolgono un ruolo logicamente
distinguibile dai soggetti intermediati.

Interfacce/Protocolli
---------------------

Il NodoSPC espone diverse interfacce per realizzare le funzioni di
cooperazione:

-  **Web-services**, realizzati con protocollo SOAP;

-  **SFTP**, per il trasferimento sicuro di file che non necessitano di
   essere elaborati contestualmente;

-  **WISP**, *web app* (protocollo HTTPS) che realizza un *wizard*
   interattivo per la scelta del PSP con cui effettuare il pagamento da
   parte dell’Utilizzatore finale.

..

   |C:\Users\mogi\AppData\Local\Microsoft\Windows\INetCache\Content.Outlook\2QI8WBLX\cd_interfacce.png|

**Figura XX – Diagramma delle interfacce di comunicazione**

Le interfacce *web services* e SFTP rappresentate nella figura
precedente sono ricapitolate in tabella:

+-----------------+-----------------+-----------------+-----------------+
| Denominazione   | Formato         | Protocollo      | Descrizione     |
+=================+=================+=================+=================+
| NodoPerEc       | WSDL            | SOAP            | Raccolta di     |
|                 |                 |                 | metodi e        |
|                 |                 |                 | parametri di    |
|                 |                 |                 | interfaccia     |
|                 |                 |                 | esposti dal     |
|                 |                 |                 | NodoSPC         |
|                 |                 |                 | fruibili dagli  |
|                 |                 |                 | EC              |
+-----------------+-----------------+-----------------+-----------------+
| EcPerNodo       | WSDL            | SOAP            | Raccolta di     |
|                 |                 |                 | metodi e        |
|                 |                 |                 | parametri di    |
|                 |                 |                 | interfaccia     |
|                 |                 |                 | esposti dagli   |
|                 |                 |                 | EC fruibili dal |
|                 |                 |                 | NodoSPC         |
+-----------------+-----------------+-----------------+-----------------+
| NodoPerPSP      | WSDL            | SOAP            | Raccolta di     |
|                 |                 |                 | metodi e        |
|                 |                 |                 | parametri di    |
|                 |                 |                 | interfaccia     |
|                 |                 |                 | esposti dal     |
|                 |                 |                 | NodoSPC         |
|                 |                 |                 | fruibili dai    |
|                 |                 |                 | PSP             |
+-----------------+-----------------+-----------------+-----------------+
| PspPerNodo      | WSDL            | SOAP            | Raccolta di     |
|                 |                 |                 | metodi e        |
|                 |                 |                 | parametri di    |
|                 |                 |                 | interfaccia     |
|                 |                 |                 | esposti dai PSP |
|                 |                 |                 | fruibili dal    |
|                 |                 |                 | NodoSPC         |
+-----------------+-----------------+-----------------+-----------------+
|                 |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| SFTP            | Testo           | SFTP            | Raccolta di     |
|                 |                 |                 | regole per la   |
|                 |                 |                 | ricezione di    |
|                 |                 |                 | file massivi    |
|                 |                 |                 | e/o elementi    |
|                 |                 |                 | dal NodoSPC.    |
+-----------------+-----------------+-----------------+-----------------+

**Tabella XX – Interfacce di comunicazione**

Le caratteristiche tecniche dei servizi utilizzati all’interno dei casi
d’uso sono disponibili all’interno del progetto gitHub in formato WSDL
(per le chiamate SOAP). I dati per la configurazione dei servizi SFTP
sono messi a disposizione ai soggetti aderenti, in forma testuale,
mediante canali riservati.

Per l’interfaccia WISP nei confronti dell’Utilizzatore finale sono resi
disponibili per gli EC degli SDK per lo sviluppo di applicazioni
*mobile*.

Architettura Funzionale
-----------------------

Per descrivere l’interazione tra EC, NodoSPC e PSP questa sezione è
stata articolata nei seguenti capitoli:

-  **Modello dei Dati**: documenta le strutture dei dati scambiati
   all’interno dei servizi tra i diversi attori ed il NodoSPC.

-  **Pagamento Attivato presso EC**: documenta i metodi messi a
   disposizione dei soggetti aderenti per realizzare il modello di
   pagamento attivato presso l’EC.

-  **Pagamento Attivato presso PSP**: documenta i metodi messi a
   disposizione dei soggetti aderenti per realizzare un pagamento di una
   posizione debitoria presso un PSP.

-  **Avvisatura Digitale**: documenta i metodi messi a disposizione dei
   soggetti aderenti per realizzare la generazione e la distribuzione di
   un avviso di pagamento digitale.

-  **Back-Office**: documenta le funzioni accessorie che possono essere
   invocate per gestire scenari secondari del ciclo di vita del
   pagamento (es. storno, revoca).

-  **Ausiliarie**: documenta le funzioni di controllo che contribuiscono
   a monitorare lo stato di esecuzione di un pagamento (es. richiesta
   stato RPT, richiesta stato RT), al fine di attuare eventuali azioni
   di recupero.

Le funzioni del sistema sono descritte attraverso i casi d’uso secondo
lo standard UML (Use Cases, da ora in avanti UC). In particolare per
ogni funzione, verrà fornita:

-  la descrizione degli attori coinvolti ed i loro obiettivi;

-  la descrizione del caso d’uso nominale, cioè il *workflow* che
   termina in assenza di errori

Nel dettaglio, ogni UC verrà descritto attraverso:

-  una condizione iniziale dello stato del pagamento che definisce il
   pre-requisito per l’attuazione del caso d’uso;

-  un trigger, cioè l’evento che scatena il caso d’uso;

-  una descrizione testuale del *workflow*;

-  una condizione finale che identifica lo stato del pagamento a
   conclusione dello UC;

-  uno (o più) *sequence diagram* che descrivono le interazioni nel
   tempo tra i diversi attori e le interfacce utilizzate.

Ogni messaggio contenuto all’interno dei *sequence diagram* sarà:

-  numerato in base all’ordine temporale di invio/ricezione del
   messaggio;

-  caratterizzato dalla notazione riportata in tabella;

-  corredato da una descrizione; nel caso di messaggio di risposta
   (*response*), indicherà l’esito della richiesta (*request*)
   effettuata.

La tabella seguente illustra le notazioni grafiche utilizzate nei
*sequence diagrams*.

+-----------------------+-----------------------+-----------------------+
|    Elemento           | Simbolo               | Vincoli / Note        |
+=======================+=======================+=======================+
| Attore                | |image3|              | Rappresenta uno degli |
|                       |                       | attori del Sistema    |
|                       |                       | pagoPA                |
+-----------------------+-----------------------+-----------------------+
| Richiesta SOAP        |                       | Freccia rossa linea   |
|                       |                       | continua, che         |
|                       |                       | rappresenta la        |
|                       |                       | richiesta entrante    |
|                       |                       | nell’interfaccia      |
|                       |                       | dell’attore che       |
|                       |                       | espone i servizi      |
+-----------------------+-----------------------+-----------------------+
| Risposta SOAP         |                       | Freccia blu linea     |
|                       |                       | tratteggiata, che     |
|                       |                       | rappresenta la        |
|                       |                       | risposta uscente      |
|                       |                       | dall’interfaccia      |
|                       |                       | dell’attore che       |
|                       |                       | espone i servizi;     |
|                       |                       | appare sempre in      |
|                       |                       | corrispondenza di una |
|                       |                       | richiesta SOAP        |
+-----------------------+-----------------------+-----------------------+
| GET HTTP              |                       | Freccia verde linea   |
|                       |                       | continua, che         |
|                       |                       | rappresenta le        |
|                       |                       | chiamate effettuate   |
|                       |                       | dall’utilizzatore     |
|                       |                       | finale per la         |
|                       |                       | fruizione delle       |
|                       |                       | applicazioni WEB      |
|                       |                       | fornite dagli attori  |
|                       |                       | del processo          |
+-----------------------+-----------------------+-----------------------+
| Azione SFTP           |                       | Freccia viola linea   |
|                       |                       | continua, che         |
|                       |                       | rappresenta un’azione |
|                       |                       | mediata dal           |
|                       |                       | protocollo SFPT       |
+-----------------------+-----------------------+-----------------------+
| SFTP *response*       |                       | Freccia viola linea   |
|                       |                       | tratteggiata, che     |
|                       |                       | rappresenta la        |
|                       |                       | risposta ad un        |
|                       |                       | comando SFTP          |
+-----------------------+-----------------------+-----------------------+
| Stato Pagamento       |                       | Losanga fondo giallo  |
|                       |                       | bordo rosso, che      |
|                       |                       | rappresenta lo stato  |
|                       |                       | del pagamento sul     |
|                       |                       | NodoSPC               |
+-----------------------+-----------------------+-----------------------+

**Tabella XX – Notazioni grafiche utilizzate nei sequence diagram**

Con l’obiettivo di favorire l’attuazione di strategie di ripristino,
automatiche o manuali, da mettere in atto direttamente da parte degli
attori connessi al sistema (EC, PSP) i possibili errori saranno
classificati in base alle categorie riportate nella figura sottostante.

|intro_errori_revoca_storno_riconciliazione|

**Figura XX – Raggruppamento delle possibili tipologie di errori**

Le tipologie di errori con relativa descrizione e macro-categoria di
appartenenza sono descritte nella tabella sottostante.

+-----------------------+-----------------------+-----------------------+
| Categoria             | Tipologia             | Descrizione           |
+=======================+=======================+=======================+
| Errori                | Superamento Soglie    | Il soggetto fruitore  |
| Infrastrutturali      |                       | ha superato i limiti  |
|                       |                       | di interazione        |
|                       |                       | applicativa           |
|                       |                       | (frequenza di         |
|                       |                       | richieste troppo      |
|                       |                       | elevata) con il       |
|                       |                       | soggetto erogatore di |
|                       |                       | cui al documento      |
|                       |                       | “Indicatori di        |
|                       |                       | qualità per i         |
|                       |                       | soggetti aderenti”    |
+-----------------------+-----------------------+-----------------------+
|                       | Connessione           | Impossibilità di      |
|                       |                       | interagire con la     |
|                       |                       | Controparte           |
|                       |                       | applicativa raggiunta |
|                       |                       | mediante il NodoSPC   |
+-----------------------+-----------------------+-----------------------+
|                       | *Timeout*/Congestioni | Superamento delle     |
|                       |                       | soglie temporali      |
|                       |                       | previste per la       |
|                       |                       | risposta del soggetto |
|                       |                       | erogatore di cui al   |
|                       |                       | documento “Indicatori |
|                       |                       | di qualità per i      |
|                       |                       | soggetti aderenti”    |
+-----------------------+-----------------------+-----------------------+
| Errori Configurazione | Configurazione        | Errore nei dati di    |
|                       | Chiamante             | configurazione da     |
|                       |                       | parte del soggetto    |
|                       |                       | fruitore del servizio |
|                       |                       | applicativo invocato  |
+-----------------------+-----------------------+-----------------------+
|                       | Configurazione        | Errore nei dati di    |
|                       | Controparte           | configurazione della  |
|                       |                       | controparte           |
|                       |                       | applicativa raggiunta |
|                       |                       | mediante il NodoSPC   |
+-----------------------+-----------------------+-----------------------+
| Errori Controparte    | *Timeout* Controparte | Superamento delle     |
|                       |                       | soglie temporali      |
|                       |                       | previste per la       |
|                       |                       | risposta della        |
|                       |                       | controparte           |
|                       |                       | applicativa di cui al |
|                       |                       | documento “Indicatori |
|                       |                       | di qualità per i      |
|                       |                       | soggetti aderenti”    |
+-----------------------+-----------------------+-----------------------+
|                       | Errore *response*     | Errore nella risposta |
|                       | Controparte           | da parte della        |
|                       |                       | controparte           |
|                       |                       | applicativa           |
+-----------------------+-----------------------+-----------------------+
| Errori Validazione    | Validazione           | Errore nella sintassi |
|                       | Sintattica            | dei messaggi          |
|                       |                       | scambiati             |
+-----------------------+-----------------------+-----------------------+
|                       | Duplicazione Messaggi | Duplicazione dei      |
|                       |                       | messaggi scambiati    |
|                       |                       | tra soggetto          |
|                       |                       | erogatore e fruitore  |
+-----------------------+-----------------------+-----------------------+
|                       | Validazione Semantica | Errore di validazione |
|                       |                       | semantica             |
|                       |                       | nell’esercizio del    |
|                       |                       | processi del sistema  |
+-----------------------+-----------------------+-----------------------+

**Tabella XX – Descrizione delle categorie di errore**

Per gli errori che causano l’emanazione di un *faultBean* da parte del
NodoSPC, in riferimento a ogni caso d’uso, saranno trattate le possibili
strategie di risoluzione ed evidenziati i percorsi critici per cui è
necessario l’instaurazione del Tavolo Operativo di cui alla sezione IV.

Stato del Pagamento
-------------------

Nei processi di *business* descritti nella sezione II, il processo di
pagamento può essere definito da un insieme discreto di transazioni fra
stati stabili del sistema, caratterizzati da un set di
informazioni/condizioni di entrata e un set di informazioni/condizioni
di uscita.

Gli stati tracciati nei *sequence diagram* dei casi d’uso e riportati
nel presente documento, sono unicamente quelli in cui il *workflow*
attraversa l’interfaccia applicativa del NodoSPC. Quando un soggetto non
può essere autonomo nella diagnosi di una anomalia, verranno fornite
indicazioni per l’attivazione del Tavolo Operativo con il NodoSPC e/o
con la controparte interessata.

Il seguente diagramma evidenzia la successione temporale degli stati del
processo di pagamento, la cui descrizione è riportata nella tabella
successiva.

|image5|

**Figura XX – Stati del pagamento
**

+-----------------------+-----------------------+-----------------------+
| Stato                 | Descrizione           | Tracciato su pagoPA   |
+=======================+=======================+=======================+
| S1 - “In attesa       | Stato iniziale in cui | Si                    |
| generazione PD”       | permane il sistema se |                       |
|                       | fallisce l’avvio di   |                       |
|                       | un processo di        |                       |
|                       | pagamento             |                       |
+-----------------------+-----------------------+-----------------------+
| S2 – “PD in attesa”   | L’EC ha generato una  | Si                    |
|                       | Posizione Debitoria,  |                       |
|                       | di propria iniziativa |                       |
|                       | o in conseguenza di   |                       |
|                       | un’azione spontanea   |                       |
|                       | dell’Utilizzatore     |                       |
|                       | Finale.               |                       |
|                       |                       |                       |
|                       | *Sono in questo stato |                       |
|                       | tutti i pagamenti per |                       |
|                       | cui esiste un IUV, un |                       |
|                       | numero Avviso di      |                       |
|                       | Pagamento, ma ancora  |                       |
|                       | nessuna RPT associata |                       |
|                       | è stata generata.*    |                       |
+-----------------------+-----------------------+-----------------------+
| S3 – “RPT Attivata”   | Nel dominio dell’EC è | Si                    |
|                       | stata generata una    |                       |
|                       | RPT a causa della     |                       |
|                       | scelta da parte       |                       |
|                       | dell’Utilizzatore     |                       |
|                       | Finale del PSP che    |                       |
|                       | gestirà il pagamento. |                       |
|                       |                       |                       |
|                       | *Sono in questo stato |                       |
|                       | tutti i pagamenti per |                       |
|                       | cui è stata generata  |                       |
|                       | una RPT. È stato      |                       |
|                       | generato un CCP che   |                       |
|                       | distingue il          |                       |
|                       | tentativo di          |                       |
|                       | pagamento. La RPT     |                       |
|                       | risulta validata e    |                       |
|                       | presa in carico dal   |                       |
|                       | NodoSPC.*             |                       |
+-----------------------+-----------------------+-----------------------+
| S4 – “Pagamento       | Il pagamento risulta  | Si (solo per i        |
| autorizzato”          | autorizzato           | pagamenti autorizzati |
|                       | dall’Utilizzatore     | su WISP)              |
|                       | Finale attraverso i   |                       |
|                       | meccanismi previsti   |                       |
|                       | dal sistema pagoPA    |                       |
|                       |                       |                       |
|                       | *Sono in questo stato |                       |
|                       | tutti i pagamenti per |                       |
|                       | cui la RPT risulta    |                       |
|                       | presa in carico da un |                       |
|                       | PSP. Il PSP non ha    |                       |
|                       | ancora generato la RT |                       |
|                       | corrispondente.*      |                       |
+-----------------------+-----------------------+-----------------------+
| S5 – “RPT Pagata”     | Il pagamento risulta  | Si                    |
|                       | andato a buon fine ed |                       |
|                       | il PSP scelto         |                       |
|                       | dall’Utilizzatore     |                       |
|                       | Finale incassa la     |                       |
|                       | somma e genera la RT. |                       |
|                       |                       |                       |
|                       | *Sono in questo stato |                       |
|                       | tutti i pagamenti     |                       |
|                       | andati a buon fine,   |                       |
|                       | per cui il PSP ha     |                       |
|                       | generato la RT.*      |                       |
+-----------------------+-----------------------+-----------------------+
| S6 – “RT Nodo”        | La RT generata dal    | Si                    |
|                       | PSP scelto            |                       |
|                       | dall’Utilizzatore     |                       |
|                       | Finale è consegnata   |                       |
|                       | al NodoSPC            |                       |
|                       |                       |                       |
|                       | *Sono in questo stato |                       |
|                       | tutti i pagamenti     |                       |
|                       | andati a buon fine,   |                       |
|                       | per cui il NodoSPC ha |                       |
|                       | preso in carico la    |                       |
|                       | RT.*                  |                       |
+-----------------------+-----------------------+-----------------------+
| S7 – “RT EC”          | La RT è consegnata    | Si                    |
|                       | all’Ente Creditore    |                       |
|                       | dal NodoSPC           |                       |
|                       |                       |                       |
|                       | *Sono in questo stato |                       |
|                       | tutti i pagamenti     |                       |
|                       | andati a buon fine,   |                       |
|                       | per cui l’EC ha preso |                       |
|                       | in carico la RT.*     |                       |
+-----------------------+-----------------------+-----------------------+
| S8 – “RT Accreditata” | Il PSP scelto         | No                    |
|                       | dall’Utilizzatore     |                       |
|                       | Finale ha accreditato |                       |
|                       | il pagamento sul      |                       |
|                       | conto indicato nella  |                       |
|                       | RPT dall’Ente         |                       |
|                       | Creditore.            |                       |
|                       |                       |                       |
|                       | *Sono in questo stato |                       |
|                       | tutti i pagamenti la  |                       |
|                       | cui RT può essere     |                       |
|                       | messa in relazione a  |                       |
|                       | SCT disposto dal      |                       |
|                       | PSP.*                 |                       |
+-----------------------+-----------------------+-----------------------+
| S9 – “RT Rendicontata | Il PSP genera e mette | Si                    |
| PSP”                  | a disposizione il     |                       |
|                       | flusso di             |                       |
|                       | rendicontazione per   |                       |
|                       | l’EC sul Nodo SPC.    |                       |
|                       |                       |                       |
|                       | *Sono in questo stato |                       |
|                       | tutti i pagamenti per |                       |
|                       | il quali il PSP ha    |                       |
|                       | disposto un PSP       |                       |
|                       | cumulativo e possono  |                       |
|                       | essere messi in       |                       |
|                       | relazione a un flusso |                       |
|                       | di rendicontazione.*  |                       |
+-----------------------+-----------------------+-----------------------+
| S10 – “Pronto per     | Il pagamento è pronto | Si                    |
| riconciliazione”      | per essere            |                       |
|                       | riconciliato sui      |                       |
|                       | sistemi di            |                       |
|                       | *back-office* dell’EC |                       |
|                       |                       |                       |
|                       | *Sono in questo stato |                       |
|                       | tutti i pagamenti i   |                       |
|                       | cui flussi di         |                       |
|                       | rendicontazione,      |                       |
|                       | acquisiti dall’EC,    |                       |
|                       | quadrano con i        |                       |
|                       | corrispondenti SPC*   |                       |
+-----------------------+-----------------------+-----------------------+
| S11 – “PD annullata”  | L’EC ha annullato una | No                    |
|                       | Posizione Debitoria,  |                       |
|                       | precedentemente       |                       |
|                       | generata.             |                       |
|                       |                       |                       |
|                       | *Sono in questo stato |                       |
|                       | tutti i pagamenti     |                       |
|                       | disposti al di fuori  |                       |
|                       | del sistema pagoPA*   |                       |
+-----------------------+-----------------------+-----------------------+

**Tabella XX –** **Descrizione degli stati del pagamento**

La seguente tabella ha lo scopo di associare a ciascuno dei *task* dei
modelli di business di cui alla sezione II le primitive SOAP coinvolte,
evidenziando le transizioni di stato causate dall’esecuzione degli
stessi *task*.

+---------+---------+---------+---------+---------+---------+---------+
| Task    | Primiti | Stato   | Stato   | Pre-con | Post-co | Note    |
|         | va      | di      | di      | dizioni | ndizion |         |
|         |         | Ingress | Uscita  |         | i       |         |
|         |         | o       |         |         |         |         |
+=========+=========+=========+=========+=========+=========+=========+
| T2.2.1  | -       | n.a.    | S1 -    | n.a.    | L’EC ha | Lo      |
|         |         |         | “In     |         | ricevut | stato   |
|         |         |         | attesa  |         | o       | S1 è il |
|         |         |         | generaz |         | la      | primo   |
|         |         |         | ione    |         | richies | stato   |
|         |         |         | PD”     |         | ta      | present |
|         |         |         |         |         | di      | e       |
|         |         |         |         |         | generaz | a       |
|         |         |         |         |         | ione    | sistema |
|         |         |         |         |         | della   | in caso |
|         |         |         |         |         | Posizio | di      |
|         |         |         |         |         | ne      | pagamen |
|         |         |         |         |         | Debitor | to      |
|         |         |         |         |         | ia      | spontan |
|         |         |         |         |         | da      | eo      |
|         |         |         |         |         | parte   |         |
|         |         |         |         |         | del PSP |         |
+---------+---------+---------+---------+---------+---------+---------+
| T1.1.1  | *nodoIn | n.a.    | S2 –    | n.a.    | L’EC ha | Lo      |
|         | viaAvvi |         | “PD in  |         | effettu | stato   |
|         | soDigit |         | attesa” |         | ato     | S2 è il |
|         | ale*    |         |         |         | la      | primo   |
|         |         |         |         |         | generaz | stato   |
|         |         |         |         |         | ione    | present |
|         |         |         |         |         | della   | e       |
|         |         |         |         |         | Posizio | a       |
|         |         |         |         |         | ne      | sistema |
|         |         |         |         |         | Debitor | in caso |
|         |         |         |         |         | ia,     | di      |
|         |         |         |         |         | che è   | pagamen |
|         |         |         |         |         | pronta  | to      |
|         |         |         |         |         | per     | con     |
|         |         |         |         |         | essere  | avviso  |
|         |         |         |         |         | lavorat |         |
|         |         |         |         |         | a       |         |
+---------+---------+---------+---------+---------+---------+---------+
| T2.1.1  | -       | n.a     | S2 –    | n.a.    | L’EC ha |         |
|         |         |         | “PD in  |         | effettu |         |
|         |         |         | attesa” |         | ato     |         |
|         |         |         |         |         | la      |         |
|         |         |         |         |         | generaz |         |
|         |         |         |         |         | ione    |         |
|         |         |         |         |         | della   |         |
|         |         |         |         |         | Posizio |         |
|         |         |         |         |         | ne      |         |
|         |         |         |         |         | Debitor |         |
|         |         |         |         |         | ia,     |         |
|         |         |         |         |         | che è   |         |
|         |         |         |         |         | pronta  |         |
|         |         |         |         |         | per     |         |
|         |         |         |         |         | essere  |         |
|         |         |         |         |         | lavorat |         |
|         |         |         |         |         | a       |         |
+---------+---------+---------+---------+---------+---------+---------+
| T2.2.2  | -       | S1 -    | S2 –    | L’EC ha | L’EC ha |         |
|         |         | “In     | “PD in  | ricevut | effettu |         |
|         |         | attesa  | attesa” | o       | ato     |         |
|         |         | generaz |         | la      | la      |         |
|         |         | ione    |         | richies | generaz |         |
|         |         | PD”     |         | ta      | ione    |         |
|         |         |         |         | di      | della   |         |
|         |         |         |         | generaz | Posizio |         |
|         |         |         |         | ione    | ne      |         |
|         |         |         |         | della   | Debitor |         |
|         |         |         |         | posizio | ia,     |         |
|         |         |         |         | ne      | che è   |         |
|         |         |         |         | debitor | pronta  |         |
|         |         |         |         | ia      | per     |         |
|         |         |         |         | da      | essere  |         |
|         |         |         |         | parte   | lavorat |         |
|         |         |         |         | del PSP | a       |         |
+---------+---------+---------+---------+---------+---------+---------+
| T1.1.1  | -       | S2 –    | S11 –   | L’EC    | La      |         |
|         |         | “PD in  | “PD     | riceve  | Posizio |         |
|         |         | attesa” | Annulla | il      | ne      |         |
|         |         |         | ta”     | pagamen | Debitor |         |
|         |         |         |         | to      | ia      |         |
|         |         |         |         | al di   | non è   |         |
|         |         |         |         | fuori   | più     |         |
|         |         |         |         | del     | lavorab |         |
|         |         |         |         | circuit | ile     |         |
|         |         |         |         | o       |         |         |
|         |         |         |         | pagoPA  |         |         |
|         |         |         |         | oppure  |         |         |
|         |         |         |         | vuole   |         |         |
|         |         |         |         | annulla |         |         |
|         |         |         |         | re      |         |         |
|         |         |         |         | la      |         |         |
|         |         |         |         | posizio |         |         |
|         |         |         |         | ne      |         |         |
|         |         |         |         | debitor |         |         |
|         |         |         |         | ia      |         |         |
|         |         |         |         | perché  |         |         |
|         |         |         |         | errata  |         |         |
+---------+---------+---------+---------+---------+---------+---------+
| T2.1.2  | *nodoIn | S2 –    | S3 –    | E’      | L’EC ha |         |
|         | viaRPT* | “PD in  | “RPT    | stata   | indiriz |         |
|         |         | attesa” | Attivat | generat | zato    |         |
|         |         |         | a”      | a       | su WISP |         |
|         |         |         |         | una     | e       |         |
|         |         |         |         | Posizio | pagoPA  |         |
|         |         |         |         | ne      | ha      |         |
|         |         |         |         | Debitor | preso   |         |
|         |         |         |         | ia.     | in      |         |
|         |         |         |         |         | carico  |         |
|         |         |         |         | L’Utili | il      |         |
|         |         |         |         | zzatore | carrell |         |
|         |         |         |         | finale  | o       |         |
|         |         |         |         | genera  | di RPT  |         |
|         |         |         |         | un      |         |         |
|         |         |         |         | carrell |         |         |
|         |         |         |         | o       |         |         |
|         |         |         |         | di RPT  |         |         |
|         |         |         |         | e avvia |         |         |
|         |         |         |         | la      |         |         |
|         |         |         |         | procedu |         |         |
|         |         |         |         | ra      |         |         |
|         |         |         |         | di      |         |         |
|         |         |         |         | pagamen |         |         |
|         |         |         |         | to      |         |         |
+---------+---------+---------+---------+---------+---------+---------+
| T2.2.7  | *nodoIn | S2 –    | S3 –    | È stata | L’EC ha |         |
|         | viaRPT* | “PD in  | “RPT    | generat | attivat |         |
|         |         | attesa” | Attivat | a       | o       |         |
|         |         |         | a”      | una     | l’RPT e |         |
|         |         |         |         | Posizio | l’ha    |         |
|         |         |         |         | ne      | inoltra |         |
|         |         |         |         | Debitor | ta      |         |
|         |         |         |         | ia.     | al PSP  |         |
|         |         |         |         |         |         |         |
|         |         |         |         | L’EC    |         |         |
|         |         |         |         | riceve  |         |         |
|         |         |         |         | una     |         |         |
|         |         |         |         | richies |         |         |
|         |         |         |         | ta      |         |         |
|         |         |         |         | di      |         |         |
|         |         |         |         | attivaz |         |         |
|         |         |         |         | ione    |         |         |
|         |         |         |         | RPT da  |         |         |
|         |         |         |         | parte   |         |         |
|         |         |         |         | del PSP |         |         |
|         |         |         |         | oppure  |         |         |
|         |         |         |         | l’Utili |         |         |
|         |         |         |         | zzatore |         |         |
|         |         |         |         | finale  |         |         |
|         |         |         |         | accede  |         |         |
|         |         |         |         | diretta |         |         |
|         |         |         |         | mente   |         |         |
|         |         |         |         | ai      |         |         |
|         |         |         |         | canali  |         |         |
|         |         |         |         | messi a |         |         |
|         |         |         |         | disposi |         |         |
|         |         |         |         | zione   |         |         |
|         |         |         |         | dall’EC |         |         |
|         |         |         |         | ed ha   |         |         |
|         |         |         |         | scelto  |         |         |
|         |         |         |         | la      |         |         |
|         |         |         |         | Posizio |         |         |
|         |         |         |         | ne      |         |         |
|         |         |         |         | Debitor |         |         |
|         |         |         |         | ia      |         |         |
|         |         |         |         | da      |         |         |
|         |         |         |         | pagare  |         |         |
+---------+---------+---------+---------+---------+---------+---------+
| T2.1.5  | -       | S3 –    | S4 –    | La RPT  | L’Utili |         |
|         |         | “RPT    | “Pagame | è stata | zzatore |         |
|         |         | Attivat | nto     | attivat | finale  |         |
|         |         | a”      | autoriz | a       | ha      |         |
|         |         |         | zato”   |         | approva |         |
|         |         |         |         |         | to      |         |
|         |         |         |         |         | il      |         |
|         |         |         |         |         | pagamen |         |
|         |         |         |         |         | to      |         |
+---------+---------+---------+---------+---------+---------+---------+
| T2.2.8  | -       | S3 –    | S4 –    | La RPT  | L’Utili |         |
|         |         | “RPT    | “Pagame | è stata | zzatore |         |
|         |         | Attivat | nto     | attivat | finale  |         |
|         |         | a”      | autoriz | a       | ha      |         |
|         |         |         | zato”   |         | approva |         |
|         |         |         |         |         | to      |         |
|         |         |         |         |         | il      |         |
|         |         |         |         |         | pagamen |         |
|         |         |         |         |         | to      |         |
+---------+---------+---------+---------+---------+---------+---------+
| T2.1.9  | *pspInv | S4 –    | S5 –    | L’Utili | Il PSP  |         |
|         | iaRPT*  | “Pagame | “RPT    | zzatore | ha      |         |
|         |         | nto     | Pagata” | finale  | incassa |         |
|         |         | autoriz |         | ha      | to      |         |
|         |         | zato”   |         | approva | il      |         |
|         |         |         |         | to      | pagamen |         |
|         |         |         |         | il      | to      |         |
|         |         |         |         | pagamen |         |         |
|         |         |         |         | to      |         |         |
+---------+---------+---------+---------+---------+---------+---------+
| T2.2.9  | -       | S4 –    | S5 –    | L’Utili | Il PSP  | In caso |
|         |         | “Pagame | “RPT    | zzatore | ha      | di      |
|         |         | nto     | Pagata” | finale  | incassa | pagamen |
|         |         | autoriz |         | ha      | to      | to      |
|         |         | zato”   |         | approva | il      | attrave |
|         |         |         |         | to      | pagamen | rso     |
|         |         |         |         | il      | to      | PSP è   |
|         |         |         |         | pagamen |         | possibi |
|         |         |         |         | to      |         | le      |
|         |         |         |         |         |         | che il  |
|         |         |         |         |         |         | pagamen |
|         |         |         |         |         |         | to      |
|         |         |         |         |         |         | da      |
|         |         |         |         |         |         | parte   |
|         |         |         |         |         |         | dell’Ut |
|         |         |         |         |         |         | ente    |
|         |         |         |         |         |         | finale  |
|         |         |         |         |         |         | avvenga |
|         |         |         |         |         |         | prima   |
|         |         |         |         |         |         | del     |
|         |         |         |         |         |         | ricevim |
|         |         |         |         |         |         | ento    |
|         |         |         |         |         |         | dell’RP |
|         |         |         |         |         |         | T       |
|         |         |         |         |         |         | da      |
|         |         |         |         |         |         | parte   |
|         |         |         |         |         |         | dello   |
|         |         |         |         |         |         | stesso  |
|         |         |         |         |         |         | PSP,    |
|         |         |         |         |         |         | per     |
|         |         |         |         |         |         | questo  |
|         |         |         |         |         |         | si      |
|         |         |         |         |         |         | raccoma |
|         |         |         |         |         |         | nda     |
|         |         |         |         |         |         | di      |
|         |         |         |         |         |         | effettu |
|         |         |         |         |         |         | are     |
|         |         |         |         |         |         | sempre  |
|         |         |         |         |         |         | la      |
|         |         |         |         |         |         | verific |
|         |         |         |         |         |         | a       |
|         |         |         |         |         |         | dell’RP |
|         |         |         |         |         |         | T       |
|         |         |         |         |         |         | (*Gatew |
|         |         |         |         |         |         | ay*     |
|         |         |         |         |         |         | G2.5)   |
+---------+---------+---------+---------+---------+---------+---------+
| T2.1.12 | *nodoIn | S5 –    | S6 –    | Il PSP  | La RT è |         |
|         | viaRT*  | “RPT    | “RT     | ha      | stata   |         |
|         |         | Pagata” | Nodo”   | ricevut | ricevut |         |
|         |         |         |         | o       | a       |         |
|         |         |         |         | la RPT  | da      |         |
|         |         |         |         | ed ha   | pagoPA  |         |
|         |         |         |         | incassa |         |         |
|         |         |         |         | to      |         |         |
|         |         |         |         | il      |         |         |
|         |         |         |         | pagamen |         |         |
|         |         |         |         | to      |         |         |
+---------+---------+---------+---------+---------+---------+---------+
| T2.2.11 | *nodoIn | S5 –    | S6 –    | Il PSP  | La RT è |         |
|         | viaRT*  | “RPT    | “RT     | ha      | stata   |         |
|         |         | Pagata” | Nodo”   | ricevut | ricevut |         |
|         |         |         |         | o       | a       |         |
|         |         |         |         | la RPT  | da      |         |
|         |         |         |         | ed ha   | pagoPA  |         |
|         |         |         |         | incassa |         |         |
|         |         |         |         | to      |         |         |
|         |         |         |         | il      |         |         |
|         |         |         |         | pagamen |         |         |
|         |         |         |         | to      |         |         |
+---------+---------+---------+---------+---------+---------+---------+
| T2.1.13 | *paaInv | S6 –    | S7 –    | La RT è | L’EC ha |         |
|         | iaRT*   | “RT     | “RT EC” | stata   | ricevut |         |
|         |         | Nodo”   |         | ricevut | o       |         |
|         |         |         |         | a       | l’RT    |         |
|         |         |         |         | da      |         |         |
|         |         |         |         | pagoPA  |         |         |
+---------+---------+---------+---------+---------+---------+---------+
| T2.2.12 | *paaInv | S6 –    | S7 –    | La RT è | L’EC ha |         |
|         | iaRT*   | “RT     | “RT EC” | stata   | ricevut |         |
|         |         | Nodo”   |         | ricevut | o       |         |
|         |         |         |         | a       | l’RT    |         |
|         |         |         |         | da      |         |         |
|         |         |         |         | pagoPA  |         |         |
+---------+---------+---------+---------+---------+---------+---------+
| T2.1.16 | -       | S7 –    | S8 –    | Il PSP  | Il PSP  |         |
|         |         | “RT EC” | “Accred | ha      | ha      |         |
|         |         |         | itata”  | incassa | accredi |         |
|         |         |         |         | to      | tato    |         |
|         |         |         |         | il      | il      |         |
|         |         |         |         | pagamen | pagamen |         |
|         |         |         |         | to      | to      |         |
|         |         |         |         |         | sul     |         |
|         |         |         |         |         | conto   |         |
|         |         |         |         |         | dell’EC |         |
+---------+---------+---------+---------+---------+---------+---------+
| T2.2.15 | -       | S7 –    | S8 –    | Il PSP  | Il PSP  |         |
|         |         | “RT EC” | “Accred | ha      | ha      |         |
|         |         |         | itata”  | incassa | accredi |         |
|         |         |         |         | to      | tato    |         |
|         |         |         |         | il      | il      |         |
|         |         |         |         | pagamen | pagamen |         |
|         |         |         |         | to      | to      |         |
|         |         |         |         |         | sul     |         |
|         |         |         |         |         | conto   |         |
|         |         |         |         |         | dell’EC |         |
+---------+---------+---------+---------+---------+---------+---------+
| T2.1.17 | *nodoIn | S8 –    | S9 –    | Il PSP  | Il PSP  |         |
|         | viaFlus | “Accred | “RT     | ha      | ha      |         |
|         | si*     | itata”  | Rendico | accredi | inviato |         |
|         |         |         | ntata   | tato    | il      |         |
|         |         |         | PSP”    | il      | rendico |         |
|         |         |         |         | pagamen | nto     |         |
|         |         |         |         | to      | degli   |         |
|         |         |         |         | sul     | accredi |         |
|         |         |         |         | conto   | ti      |         |
|         |         |         |         | dell’EC | effettu |         |
|         |         |         |         |         | ati     |         |
|         |         |         |         |         | a       |         |
|         |         |         |         |         | pagoPA  |         |
+---------+---------+---------+---------+---------+---------+---------+
| T2.2.16 | *nodoIn | S8 –    | S9 –    | Il PSP  | Il PSP  | In caso |
|         | viaFlus | “Accred | “RT     | ha      | ha      | di      |
|         | si*     | itata”  | Rendico | accredi | inviato | pagamen |
|         |         |         | ntata   | tato    | il      | to      |
|         |         |         | PSP”    | il      | rendico | di      |
|         |         |         |         | pagamen | nto     | singola |
|         |         |         |         | to      | degli   | RT, il  |
|         |         |         |         | sul     | accredi | PSP     |
|         |         |         |         | conto   | ti      | potrebb |
|         |         |         |         | dell’EC | effettu | e       |
|         |         |         |         |         | ati     | non     |
|         |         |         |         |         | a       | inviare |
|         |         |         |         |         | pagoPA  | il      |
|         |         |         |         |         |         | rendico |
|         |         |         |         |         |         | nto     |
+---------+---------+---------+---------+---------+---------+---------+
| T2.1.18 | *nodoCh | S9 –    | S10 –   | Il PSP  | pagoPA  |         |
|         | iediFlu | “RT     | “Pronto | ha      | ha      |         |
|         | ssoRend | Rendico | per     | inviato | fornito |         |
|         | icontaz | ntata   | riconci | il      | i       |         |
|         | ione*   | PSP”    | liazion | rendico | rendico |         |
|         |         |         | e”      | nto     | nti     |         |
|         |         |         |         | degli   | ricevut |         |
|         |         |         |         | accredi | i       |         |
|         |         |         |         | ti      | all’EC  |         |
|         |         |         |         | effettu |         |         |
|         |         |         |         | ati     |         |         |
|         |         |         |         | a       |         |         |
|         |         |         |         | pagoPA  |         |         |
+---------+---------+---------+---------+---------+---------+---------+
| T2.2.17 | *nodoCh | S9 –    | S10 –   | Il PSP  | pagoPA  |         |
|         | iediFlu | “RT     | “Pronto | ha      | ha      |         |
|         | ssoRend | Rendico | per     | inviato | fornito |         |
|         | icontaz | ntata   | riconci | il      | i       |         |
|         | ione*   | PSP”    | liazion | rendico | rendico |         |
|         |         |         | e”      | nto     | nti     |         |
|         |         |         |         | degli   | ricevut |         |
|         |         |         |         | accredi | i       |         |
|         |         |         |         | ti      | all’EC  |         |
|         |         |         |         | effettu |         |         |
|         |         |         |         | ati     |         |         |
|         |         |         |         | a       |         |         |
|         |         |         |         | pagoPA  |         |         |
+---------+---------+---------+---------+---------+---------+---------+

**Tabella XX – Quadro sinottico delle transazioni di stato**

.. |C:\Users\mogi\AppData\Local\Microsoft\Windows\INetCache\Content.Outlook\2QI8WBLX\deploymentDiagram.png| image:: media_IntroduzioneSezIII/media/image1.png
   :width: 5.36207in
   :height: 4.8097in
.. |C:\Users\mogi\AppData\Local\Microsoft\Windows\INetCache\Content.Outlook\2QI8WBLX\cd_interfacce.png| image:: media_IntroduzioneSezIII/media/image2.png
   :width: 6.69272in
   :height: 2.02431in
.. |image2| image:: media_IntroduzioneSezIII/media/image3.png
   :width: 0.85417in
   :height: 0.23958in
.. |image3| image:: media_IntroduzioneSezIII/media/image3.png
   :width: 0.85417in
   :height: 0.23958in
.. |intro_errori_revoca_storno_riconciliazione| image:: media_IntroduzioneSezIII/media/image4.png
   :width: 5.11181in
   :height: 3.68681in
.. |image5| image:: media_IntroduzioneSezIII/media/image5.png
   :width: 3.17917in
   :height: 8.11181in
