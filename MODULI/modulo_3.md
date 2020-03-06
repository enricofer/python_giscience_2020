![](CopertinaModulo3.png)

--

# MODULI e librerie

Un fattore determinante nel successo di Python è la flessibilità, la modularità e la facile estendibilità permessa dall'organizzazione del codice eseguibile in moduli.  

I moduli possono essere:

* predefiniti, già compresi nella [dotazione di base del linguaggio](https://docs.python.org/3/library/index.html)
* esterni, contenuti nei path di sistema di Python (PATH, PYTHONPATH). Possono essere preimportati o [importati da internet](https://pypi.python.org/pypi?%3Aaction=browse) tramite pip/setuptools
* definiti localmente dall'utente in altri files python

---

## Importazione dei moduli

I moduli sono collezioni strutturate ed organizzate di codice python le cui definizioni possono essere importate all'interno di un programma

```python
# Importa un modulo con chiamata ad una funzione contenuta
import math
math.floor(10.6)

# Importa singoli elementi da un modulo
from os import path
path.join('C:', 'Utenti', 'paolo', 'documenti')
'C:/Utenti/paolo/documenti'
```

--

## Organizzazione dei moduli

Quando importiamo un modulo, Python deve trovare il file corrispondente, e per farlo controlla in ordine le directory elencate nella lista `sys.path`. Una volta trovato il file, Python lo importa, crea un *module object* (oggetto modulo), e lo salva nel dizionario `sys.modules`. Se il modulo viene importato nuovamente in un altro punto del programma, Python è in grado di recuperare il modulo da `sys.modules` senza doverlo importare nuovamente. Inoltre, i moduli `.py` vengono *compilati in bytecode*: un formato più efficiente che viene salvato in file con estensione `.pyc` che a loro volta vengono salvati in una cartella chiamata `__pycache__`. Quando viene eseguito un programma che ha bisogno di importare un modulo, se `modulo.pyc` esiste già ed è aggiornato, allora Python importerà quello invece di ricompilare il modulo in bytecode ogni volta.

--

## La libreria standard di Python

Python 3 nella sua versione base già mette a disposizione un set molto ampio di moduli standard sviluppati sotto l'ombrello della comunità di Python: https://docs.python.org/3/library/

Alcuni dei moduli comunemente usati sono i seguenti:

operazioni matematiche: `math`

servizi generici del sistema operativo: `os` `shutil`

interfaccia runtime con il sistema: `sys` `io `

tipi estesi di dato: `time` `datetime` `collections`

protocolli internet e serializzazione: `urllib `  `httplib `  `json`

archiviazione di dati: `csv` `zipfile`

interfaccia utente: `argparse` `tkinter`

--

## `math`

https://docs.python.org/3/library/math.html

```
import math

math.floor(10.6) # troncamento al numero intero inferiore 
math.ceil(10.6) # troncamento al numero intero superiore 

math.pi # PI greco
math.cos(2*math.pi)
math.degrees(math.pi)

math.isclose(math.sin(0),0) #confronta numeri decimali con approssimazione
```

--

## `os` e `os.path`

https://docs.python.org/3/library/os.path.html#os.path.split

```
import os

path = os.path.join("c:/","OSGeo4W64","OSGeo4W.bat")
path = os.path.dirname(__file__)
dirpath = os.path.dirname(path)
os.path.split(path) separa il nome della directory dal file
os.path.splitext(path) separa il file (path completo) dall'estensione

os.remove(path) #cancella il file puntato da path
os.listdir(dirpath) #lista il contenuto di una directory 
os.makedirs(path) #crea il path completo
```

--

## Uso dei moduli esterni

E' possibile usare moduli esterni configurando opportunamente la variabile d'ambiente PYTHONPATH in modo che essa punti ad una cartella contente il codice del modulo

Oppure si può depositare manualmente la cartella contente il modulo python ed i moduli da esso dipendenti dentro la cartella "site-packages".

La comunità Python ha organizzato un repository dei moduli correntemente utilizzabili da python: https://pypi.python.org/pypi Il repository è utilizzabile tramite il comando [pip](https://pip.pypa.io/en/stable/installing/) installabile scaricando ed eseguendo il file [get-pip.py](http://pip.readthedocs.io/en/stable/installing/#do-i-need-to-install-pip)

```shell
python get-pip.py #se non già installato con python
pip install [nome pacchetto]
```

Il comando provvede ad installare il pacchetto desiderato insieme alle sue dipendenze nella versione stabilita dai *"requirements"* del modulo, aiutando il programmatore a superare i conflitti tra versioni diverse dei pacchetti installati.

--

## pip install

```shell
C:\Users\enrico>pip install requests
Collecting requests
...
Collecting idna<3,>=2.5 (from requests)
...
Collecting certifi>=2017.4.17 (from requests)
...
Collecting urllib3!=1.25.0,!=1.25.1,<1.26,>=1.21.1 (from requests)
...
Collecting chardet<4,>=3.0.2 (from requests)
...
Installing collected packages: idna, certifi, urllib3, chardet, requests
Successfully installed certifi-2019.11.28 chardet-3.0.4 idna-2.9 requests-2.23.0 urllib3-1.25.8
```

--

## altri comandi di pip

```
pip uninstall requests  #disinstallazione pacchetto

pip search requests     #ricerca pacchetto per nome

pip show requests       #mostra dettaglio di un pacchetto

pip list                #lista dei pacchetti installati

pip freeze              #genera in file requirements
```

--

## Virtualenv

I Virtualenv (ambienti virtuali) sono un modo semplice per  creare progetti Python isolati, in cui installare diverse librerie che  non andranno in conflitto con altre librerie in altri ambienti. 

Per installare virtualenv sulla proprima macchina, basta digitare su un terminale il comando

```shell
pip install virtualenv
```

A questo punto, si può creare l’ambiente virtuale, utilizzando il comando

```shell
cd <directory di progetto>
virtualenv <nome ambiente virtuale> #l'ambiente verrà creato nella directory corrente
```

--

Attivazione e deattivazione di un virtualenv

```
<path alla directory dell'ambiente virtuale>\scripts\activate.bat #per l'attivazione
deactivate #per la disattivazione
```

--

## Virtualenv wrapper

Uno strumento pratico per gestire gli ambienti virtuali è virtualenvwrapper: https://virtualenvwrapper.readthedocs.io/en/latest/ che permette di individuare un repository comune e permette di gestire la creazione.

vitualenvwrapper funziona nativamente con la shell di Linux e MacOS ma esiste una versione specifica per windows: https://pypi.org/project/virtualenvwrapper-win/

## Pipenv

https://pipenv.kennethreitz.org/en/latest/

E' un comando che unifica pip virtualenv e pipfile rendendo possibile la creazione al volo di ambienti di lavoro virtuali e gestendo al contempo le dipendenze ed il loro aggiornamento

--

## Anaconda

Anaconda è un sistema di gestione dei pacchetti esterni **alternativo a pip** e si configura come un vero e proprio ambiente operativo che comprende una propria versione di python ed un proprio gestore di ambienti virtuali.

Anaconda è particolarmente adatto per l'installazione di moduli che in pip prevedono la compilazione del codice dal lato utente e quindi per la gestione di moduli esterni in windows dove i requisiti per la compilazione spesso non sono soddisfatti e nei contesti scientifici dove è necessaria la performance e/o la possibilità di utilizzare librerie precompilati, magari in un altro linguaggio.

Anaconda può essere installato da quasta pagina: https://docs.conda.io/projects/conda/en/latest/user-guide/install/windows.html

```shell
conda install <package>
```



---

# MODULI ESTERNI

## requests: 

## pandas: 

## geopandas:

## jupiter notebooks: 

---

# Esercitazione: analizziamo i dati aggiornati del coronavirus:

1) installazione di anaconda: https://docs.conda.io/en/latest/miniconda.html

2) installazione delle librerie necessarie:

```shell
conda install requests pandas geopandas descartes
conda install -c conda-forge jupyterlab
```

3) esecuzione jupiter notebook ed aggiornamento dei dati



---

# COLLABORARE ALLO SVILUPPO DEL SOFTWARE OPEN SOURCE

--

## La piattaforma github

[Github](https://github.com/) (*Ghi-tab* per i non italiani) è una piattaforma web che permette agli sviluppatori di conservare e pubblicare i codici sorgenti dei propri programmi, senza perdere traccia delle versioni del codice stesso. Nel contempo permette a gruppi di sviluppatori di lavorare simultaneamente sullo stesso progetto evitando conflitti.
E' basato su Git, il potente strumento di versionamento creato da Linus Torvarlds, il creatore di Linux, per gestire lo sviluppo collaborativo del sistema operativo open source.

- Git è uno strumento a linea di comando, la cui comprensione esula dagli obiettivi del corso. Per approfondimenti si può fare riferimento ad uno dei tanti tutorial presenti in internet: https://www.slideshare.net/stefanovalle/guida-git

- E' ottimizzato per tenere traccia delle modifiche di file testo a livello di riga (non va bene quindi per file binari o per file di testo con poche righe)

--

## Git

per facilitare l'interazione dell'utente, github mette a disposizione Github desktop (disponibile per MacOS e Windows), che permette di gestire con facilità i vari flussi di lavoro senza necessariamente conoscere Git. E' comunque importante comprendere i principi di funzionamento di Git:

![](doc/git-transport.png)

--

## Lessico di git/github

- *repository*: archivio di files e directory gestito da git. può essere locale o remoto

- *commit*: insieme coordinato di modifiche che l'utente registra sul repository

- *branch*: uno stato del repository che viene memorizzato dall'utente separatamente da altri branch. Esistono dei branch di sistema (master, origin etc...) e dei branch utente

- *diff*: operazione che mette in evidenza le modifiche di riga tra branch

- *merge*: operazione che permette di fondere tra loro due branch (per esempio un branch di sviluppo nel branch master) mettendo in evidenza eventuali conflitti

- *clone*: operazioone di clonazione in locale di un repository remoto

- *push*: operazione con la quale si si conferisce (submit) un branch locale ad un repository remoto tenendo condo dei conflitti tra versioni

- *pull*: operazione con la quale si scarica in locale un repository remoto

- *pull request*: operazione con la quale un utente propone la modifica di un repository

--

## github desktop

E' fondamentalmente un'interfaccia grafica di Git integrata con il servizio di Github
![](doc/githubDesktop1.png)

--

## Esercitazione di Github

- accreditarsi su Github, scaricare ed installare Github desktop

- inizializzare un repository

- clonare un repository

- modificare i files / verificare le differenze / realizzare un commit

- creare un branch

- fondere (merge) due branch

- pubblicare un repository

- inviare una pull request (PR)
