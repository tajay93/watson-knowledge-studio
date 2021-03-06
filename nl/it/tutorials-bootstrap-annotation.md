---

copyright:
  years: 2015, 2018
lastupdated: "2018-03-20"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

Questa documentazione è per {{site.data.keyword.knowledgestudiofull}} su {{site.data.keyword.cloud}}. Per visualizzare la documentazione della versione precedente di {{site.data.keyword.knowledgestudioshort}} nel {{site.data.keyword.IBM_notm}} Marketplace, [fai clic su questo link ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.bluemix.net/docs/services/knowledge-studio/tutorials-bootstrap-annotation.html){: new_window}.
{: tip}

# Inizio dell'annotazione
{: #wks_tutboot_intro}

Questa esercitazione ti aiuta a comprendere come pre-annotare i documenti, che semplifica il lavoro di annotazione degli annotatori umani.
{: shortdesc}

## Obiettivi di apprendimento

Dopo aver completato questa esercitazione, conoscerai come pre-annotare i documenti con un modello di machine learning.

Questa esercitazione dovrebbe richiedere 5 minuti circa per essere completata. Potrebbe essere necessario più tempo se si approfondiscono altri concetti correlati a quest'esercitazione.

## Prima di cominciare

- Assicurati di stare utilizzando un browser supportato. Per informazioni, consulta [Requisiti del browser](/docs/services/watson-knowledge-studio/system-requirements.html).
- Hai correttamente completato [Esercitazione: Creazione di uno spazio di lavoro](/docs/services/watson-knowledge-studio/tutorials-create-project.html) e [Esercitazione: Creazione di un modello di machine learning](/docs/services/watson-knowledge-studio/tutorials-create-ml-model.html).
- Devi avere almeno un ID utente nel ruolo di gestore del progetto o di amministratore. Per informazioni sui ruoli utente, vedi [Assemblaggio di team](/docs/services/watson-knowledge-studio/team.html).

## Risultati

Dopo aver completato questa esercitazione, avrai una serie di documenti parzialmente annotati. In seguito, puoi assegnare i documenti agli annotatori umani per finire il lavoro di annotazione.

## Lezione 1: Pre-annotazione di nuovi documenti con un modello di machine learning
{: #wks_tutboot_ml}

In questa lezione, apprenderai come utilizzare un modello di machine learning per pre-annotare i documenti in {{site.data.keyword.knowledgestudioshort}}.

### Informazioni su quest'attività

Dopo aver preparato un modello di machine learning, puoi utilizzarlo per pre-annotare i nuovi documenti che aggiungi al corpus. 

> **Attenzione:** non eseguire un pre-annotatore sui documenti che sono stati annotati dagli umani ma non ancora aggiunti al ground truth. Se lo fai, tutte le annotazioni correnti saranno rimosse dai documenti.

In questa esercitazione, puoi aggiungere una seconda serie di documenti utilizzando il file `documents-ml.csv`. Non riaggiungere il file `documents-new.csv`, poiché creerà documenti duplicati nel ground truth. La duplicazione causa i seguenti problemi:

- Se le annotazioni su ogni documento non corrispondono, abbasseranno la qualità del modello di machine learning.
- Se le annotazioni su ogni documento corrispondono, sovrappreparano il modello di machine learning per i file duplicati. 

### Procedura

1. Accedi a {{site.data.keyword.knowledgestudioshort}} come amministratore.
1. Carica ulteriori documenti nello spazio di lavoro. Puoi utilizzare il file <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/knowledge-studio/documents-ml.csv" download>`documents-ml.csv`<img src="../../icons/launch-glyph.svg" alt="Icona link esterno" title="Icona link esterno" class="style-scope doc-content"></a>.

    Per i dettagli su come caricare i documenti, consulta [Creazione di un modello di machine learning > Aggiunta di documenti per l'annotazione ](/docs/services/watson-knowledge-studio/tutorials-create-ml-model.html#tut_lessml1).

1. Crea una serie di annotazioni con il file `documents-ml.csv`.

    Per questa esercitazione, assegna la serie di annotazioni a te stesso, l'amministratore. Dopo aver eseguito il modello di machine learning per pre-annotare i nuovi documenti, puoi visualizzare la serie di annotazioni per vedere come il modello li ha pre-annotati. Generalmente, assegni le serie di annotazioni a uno o più annotatori umani. Per ulteriori informazioni sulla creazione delle serie di annotazioni, consulta [Creazione di un modello di machine learning > Creazione delle serie di annotazioni](/docs/services/watson-knowledge-studio/tutorials-create-ml-model.html#wks_tutless_ml2).

1. Dalla barra laterale **Model Management** > **Versions**, seleziona la scheda **Machine Learning** e fai clic su **Run this model**.
1. Seleziona la serie di documenti che hai aggiunto al corpus, `documents-ml.csv` e fai clic su **Run**.
1. Dopo il completamento della pre-annotazione, puoi creare un'attività di annotazione umana e annotare i nuovi documenti pre-annotati.

    Per i dettagli sulla creazione di un'attività e sull'annotazione dei documenti, vedi [Creazione di un modello di machine learning > Creazione di un'attività di annotazione ](/docs/services/watson-knowledge-studio/tutorials-create-ml-model.html#wks_tutless_ml4) e [Creazione di un modello di machine learning > Annotazione dei documenti](/docs/services/watson-knowledge-studio/tutorials-create-ml-model.html#wks_tutless_ml5).

    In questa situazione, l'annotazione umana richiede meno tempo perché hai utilizzato il modello di machine learning per pre-annotare i documenti.

### Risultati

Utilizzando il tuo modello di machine learning per pre-annotare le nuove serie di documenti, puoi velocizzare le attività di annotazione umana per quei documenti.
