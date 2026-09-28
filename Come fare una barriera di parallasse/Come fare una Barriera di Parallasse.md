di Gabriel Prandini
## Introduzione
La Barriera di Parallasse (Parallax Barrier) è una delle prime tecniche di auto-stereoscopia 3D, prima concettualizzata nel 1896 da Auguste Berthier e poi concretizzata nel 1901 da Frederic Eugene Ives. 

Per capire come funziona bisogna prima comprendere come le persone percepiscono la "profondità": essa di base è infatti un insieme di più fattori, sia percettivi che visivi, e il più importante tra essi è la piccola differenza visiva che i nostri occhi percepiscono quando osservano il mondo, essendo leggermente staccati orizzontalmente, la **disparità binoculare**, ed è proprio questa peculiarità che quasi tutti i sistemi digitali 3D, da quanto ne so, sfruttano cercando di mandare ai due occhi delle immagini leggermente differenti.

![[ParallaxBarrier_1.png | 400x300]]

Ritornando alla barriera di parallasse, possiamo dire che utilizza un metodo molto semplicistico per mandare 2 immagini diverse a ogni occhio: sfruttando delle piccolissime linee opache (nere) *verticali*, ben allineate, è possibile nascondere a ognuno degli occhi alcune colonne di pixel nello schermo, specificatamente quelle pari per uno e le dispari per l'altro (nella versione più semplice). In questo modo, visualizzando a schermo dei contenuti specifici (usando il *vertical interlacing*), è possibile far vedere a un occhio un'immagine composta dalla somma delle colonne di pixel visibili solo a lui, e all'altro un'immagine composta da quelle "oscurate" al primo. Semplice, no?
No. Partiamo dal fatto che è una delle prime tecniche mai create, e di sicuro non era stata pensata per essere usata negli schermi LCD attuali, infatti le linee della barriera devono essere larghe quasi quanto la lunghezza dei pixel dello schermo, e nei display moderni questo valore può variare dai 0,30 mm agli 0,055 mm, quindi è necessario scegliere con cura lo schermo su cui lavorare, in base alla professionalità della tua strumentazione.
## Come produrre la barriera 
Ma quindi come si produce la barriera? Beh in realtà il procedimento di base è molto semplice, ma richiederà un lungo processo di trial and error, per via delle piccole differenze fisiche che ci sono in ogni schermo, e soprattutto del margine di errore della nostra strumentazione.
I materiali che ci serviranno sono:
- Un monitor (ovviamente).
- Una stampante inkjet.
- Dei fogli di stampa **trasparenti** per inkjet.
- Un taglierino.
- Del plexiglass o vetro (vedi se necessario dopo).
Come ho accennato prima, la barriera non è altro che un insieme di linee nere e trasparenti in serie posizionate, nei sistemi più semplici, davanti al display dello schermo di interesse, in modo tale da essere:
- Allineata orizzontalmente: in modo che i punto di fuoco (sono le zone dove l'effetto 3D è evidente) siano esattamente davanti allo schermo (non così importante perché puoi semplicemente spostare la testa per trovare il punto di fuoco dell'immagine).
- Ruotata: in modo tale che le linee siano **esattamente** verticali, in modo tale che una di esse riesca a coprire la stessa colonna di pixel dall'inizio alla fine, questo è uno dei fattori più importanti da tenere in considerazione, perché se no non si otterrà l'effetto desiderato.

![[ParallaxBarrier_2.png||350]]

### Design della barriera
Per iniziare bisogna progettare la barriera, e per questo ci serviranno:
- Un software di editing immagini, io userò **GIMP**.
- Una calcolatrice.
- Tanta precisione e pazienza.
Prima di cominciare dobbiamo procurarci due dati importantissimi che determineranno la maggior parte dei risultati che calcoleremo: il **Pixel Pitch** dello schermo, un valore che indica la distanza tra i centri di due pixel adiacenti (si può trovare nella scheda tecnica del monitor online) e la **risoluzione della stampante**, più precisamente il primo valore dei due (es: se la dicitura è 5760 x 1440 dpi allora la risoluzione è 5760 dpi), questo perché le stampanti hanno 2 risoluzioni, una orizzontale che scorre direttamente sul toner della stampante (che ha la capacità di essere molto più preciso) e una verticale che scorre sull'altro asse e non è di nostro interesse, perché come vedremo le linee della barriera scorreranno in verticale e quindi nell'asse orizzontale scorrerà la **larghezza** delle linee, che è l'elemento più importante.

![[stampante.png|350]]
###### ⚠APPUNTI PER IL LETTORE⚠ (e per me)
C'è un problema di fondo con la risoluzione X della stampante, perché ho notato che GIMP non riesce sempre a gestire la stampa ed esportazione di file in risoluzioni molto alte (come quelle con cui lavoreremo).
Una soluzione che si potrebbe provare è quella di dimezzare la risoluzione X (es: 2800 dpi), e vedere se funziona, se no si può utilizzare la risoluzione Y per entrambe, ma il risultato sarà più scadente. Usare la risoluzione X ha senso SOLO se si stampano le linee in verticale lungo l'asse Y, perché facendo così la loro larghezza cadrà sull'altro asse a risoluzione maggiore. 

Ok, ora iniziamo calcolando i dati essenziali, e poi con essi creeremo il design stampabile.
**LAVOREREMO SEMPRE IN MM NELLA SCALA METRICA!**

![[schema_barriera.png|550]]
### Zona calcoli
##### Pitch della barriera
Questo valore, su carta, dovrebbe essere esattamente il doppio del **Pixel Pitch** del monitor, perché in questo modo si andrebbe a coprire quasi esattamente con le linee nere una colonna si e una colonna no. 
Ma per via del fatto che noi vediamo le parti più esterne dello schermo ad angoli diversi rispetto al centro in teoria il **Pitch della barriera** dovrebbe essere lo 0,01% più piccolo rispetto a quello detto prima, ma questo dato è marginale se si vuole lavorare con stampanti casalinghe.
_Per i nostri esempi useremo un Pixel Pitch di 0,19389309 mm, che raddoppiato diventerà il nostro Pitch della barriera: 0,3877862 mm._
##### Pixel per barriera
Ora che sappiamo quanto misura in mm la somma di una linea nera e una trasparente (pitch della barriera), dobbiamo fare 2 cose:
- Convertire questo valore in pixel, così da poter creare il design da stampare.
- Capire quanto spazio dedicare alle 2 diverse linee.
Per chiarire meglio il primo punto, dobbiamo capire che una stampante ha una certa risoluzione di stampa, e con questo si intende che in un determinato spazio *inch* (unità di misura anglosassone) questa riesce a stampare un certo numero di goccioline di inchiostro (che chiamerò pixel), e basandoci su questo dato andremo a ricavare il numero più preciso possibile di pixel o goccioline che la stampante dovrà stampare per avvicinarci il più possibile alle misure desiderate della barriera.
Questo vi farà già comprendere che purtroppo non tutte le stampanti potranno creare la barriera perfetta per ogni schermo, e che in realtà bisogna essere abbastanza fortunati a trovare l'accoppiata stampante + monitor perfetta.
Detto questo, possiamo continuare usando una semplicissima formula per convertire il **Pitch della barriera** in pixel, che è:

$$
NPixel = \frac{Pitch barriera}{25,4} \cdot RisoluzioneXStampante
$$
Quindi prendendo in considerazione i nostri esempi precedenti, il **Pitch della barriera** convertito in pixel sarà:
$$
\frac{0,3877862 mm}{25,4} \cdot 5760dpi= 87,93pixel
$$
In sintesi la formula converte il **Pitch della barriera** da mm a inch, che poi moltiplichiamo per la risoluzione della stampante, il che risulterà nel numero di pixel che dovrebbe stampare per ottenere quella misura precisa.
Ora arriva la parte difficile perché non tutte le stampanti riusciranno a darci un numero di pixel intero, come in questo caso con 87,93, e quindi dovremmo arrotondare idealmente al numero più vicino possibile a quello ottenuto.
Mettiamo caso che vogliamo arrotondare a 88, in questo caso la barriera sarà leggermente più grande, ma essendo abbastanza vicini al numero calcolato dovrebbe andare bene.
##### Determinare la larghezza delle 2 linee
Ora che sappiamo quanto vale in pixel la somma delle 2 linee possiamo andare a decidere quanti pixel vogliamo dedicare a una e quanti all'altra.
Anche qua dovremmo andare a tentativi, ma la regola di base è che la linea nera dovrebbe essere leggermente più larga di quella trasparente, così da ridurre il _**crosstalk**_, un fenomeno dove le due "immagini" o i punti di fuoco non riescono a isolarsi perfettamente, facendo in modo che in uno di essi sia possibile vedere leggermente anche il secondo, arrivando anche a rovinare l'effetto 3D (più dettagli in fondo), ma bisogna anche fare attenzione a non rendere la linea nera troppo spessa o l'effetto si rovinerà lo stesso.
Di solito a me piace aggiungere circa da 1 ai 4 pixel alla linea nera, ma questo è davvero a discrezione di chi la sta creando, non ho mai trovato una formula per calcolarlo precisamente, ma di sicuro esiste.
### Creazione della barriera
##### Progettazione pattern della barriera
Ora che abbiamo questi dati possiamo iniziare a progettare effettivamente la barriera.
Per prima cosa dobbiamo aprire il nostro software di manipolazione immagini, io userò GIMP perché è gratis, bellissimo, e intuitivo.
Una volta fatto ciò dobbiamo creare un nuovo file con queste impostazioni:
- WIDTH: Il numero di pixel calcolato in precedenza nella sezione "Pixel per barriera".
- HEIGHT: 1 px.
Poi nelle avanzate
- X/Y Resolution: 72 ppi (è un numero stock perché ora siamo progettando solo il pattern, non la barriera effettiva).
- Color space: Grayscale.
- Fill with: White.
![[GIMP_pattern.png|400]]
Adesso che abbiamo creato il file dobbiamo andare a selezionare con lo strumento _seleziona_ una sezione che parte dalla zona più a sinistra possibile dell'immagine e che sia lunga ESATTAMENTE il quantitativo di pixel che abbiamo deciso di assegnare alla linea nera (in basso sarà possibile visualizzare le dimensioni dell'area selezionata, assicuratevi che stia misurando in pixel), e una volta fatto ci basterà semplicemente riempire di nero l'intera zona con lo strumento _secchio_.
Ora che abbiamo fatto questo possiamo andare a _esportare il nostro file con nome_ nella cartella dei pattern di GIMP, che nella versione **3.0.4** si trova in:

Windows:
```
C:\Users\username\AppData\Roaming\GIMP\3.0\patterns
```

Linux:
```
/home/username/.config/GIMP/3.0/patterns/
```

salvandolo con estensione **.pat**, quindi il nome dovrà essere qualcosa del tipo:
"**patternBarriera.pat**" (se GIMP chiedesse un ulteriore nome da dare al file, chiamatelo nello stesso modo di prima).
![[pattern_name.png|400]]
##### Progettazione barriera completa
Adesso quello che si resta da fare è creare un altro file progetto in GIMP, stavolta con queste impostazioni:
- Selezionare il modello per il foglio A4 (o quello che vuoi usare per stampare)
- X Resolution: la risoluzione X della stampante che si sta sperimentando
- Y Resolution: la risoluzione Y della stampante (per inserire il valore X e Y diversi bisogna selezionare il tasto evidenziato di verde nell'immagine)
- Color space: Grayscale
- Fill with: White
![[creazione_barriera.png|400]]
Una volta creato il file bisogna andare a selezionare il pattern che abbiamo creato nel punto precedente nella tabella in alto a destra (spero rimanga uguale anche nelle prossime versioni), se non riesci a riconoscere il tuo pattern semplicemente selezionali uno a uno finché non leggi sopra la tabella il secondo nome che avevi assegnato al pattern al momento dell'esportazione.
Ora ci basta andare a creare un nuovo livello (layer) selezionando il primo tasto a sinistra nella barra in basso a destra di GIMP, andando a specificare questa importantissima impostazione:
- Fill with: Pattern.
Ora basta premere OK e aspettare che il programma finisca di creare la barriera.
Abbiamo finito di progettare la nostra barriera, non ci resta che stampare il file, ma solo dopo aver eventualmente salvato il nostro file come progetto GIMP o esportarlo come PNG, PDF, etc (non si possono usare formati lossy come JPEG).
##### Stampa della barriera
Lo step finale è proprio stampare la barriera tanto agognata, e per farlo non si dovrà far altro che premere il tasto _Stampa_ nel menù _File_ di GIMP. Una volta fatto questo si dovrà prestare particolare attenzione nell'impostare la _**risoluzione di stampa massima**_, selezionando, nella maggior parte dei casi, l'uso di carta fotografica nelle impostazioni di stampa e in quelle extra della stampante, in caso disponibili, e anche di stampare _**senza bordi**_ (se non è possibile non posso assicurare il funzionamento della barriera, ma cerca almeno di impostare il riempimento della pagina al 100% senza ridimensionamenti vari) e di controllare che nella sezione "impostazioni dell'immagine" (Image Settings) la risoluzione X/Y sia la stessa di quella impostata alla creazione del file della barriera. Fate anche attenzione che il documento stia venendo stampato in VERTICALE (Portrait).
Fatto questo possiamo inserire il nostro foglio trasparente nella stampante (la parte ruvida è quella dove andrà stampata la barriera) e premere il tasto **Stampa**.
## Applicazione barriera
### Preparazione
##### Distanza punto di fuoco
**RICORDO CHE TUTTI I CALCOLI VANNO FATTI IN MM.**
Prima di applicare la barriera allo schermo dobbiamo decidere la **distanza del punto di fuoco** dallo schermo agli occhi dell'osservatore, cioè la distanza che deve essere tenuta dallo schermo per far sì che l'effetto 3D sia visibile. 
Questa distanza può variare in base al tipo di schermo, ecco alcuni esempi:
- Nintendo 3DS: 330mm (33cm).
- Schermo di un tablet: 400-500mm (40-50cm).
- Monitor di un computer fisso: 800mm-1000mm (80cm-100cm).
La regola generale è che più uno schermo è piccolo, più la distanza sarà minore.
Si possono anche tenere le proprie misurazioni ponendo una riga tra i propri occhi e lo schermo, il modo alla fine è irrilevante, basta che alla fine si arrivi alla calcoli desiderata.
##### Distanza LCD - barriera
Con questa distanza in mente ora possiamo calcolare uno dei dati più importanti per l'applicazione della barriera: la **distanza tra la barriera e i pixel dello schermo**, infatti non è detto che la barriera debba essere messa direttamente sopra lo schermo, ma è invece più probabile che sarà necessario applicare uno spessore extra tra i due, usando un materiale trasparente come il vetro o il plexiglass, che per i nostri calcoli dovremo andare a ricercarne un valore chiamato **Refractive index** con una semplice ricerca online, ecco alcuni esempi:
- Plexiglass: 1.49
- Vetro: 1.51
Per calcolare questa distanza possiamo avvalerci di una semplice formula, e per questa ci serviranno alcuni dati:
- Pixel Pitch dello schermo (**p**)
- Distanza dal punto di fuoco (**r**)
- Indice di rifrazione del pannello che creerà spessore (**n**)
- Distanza di separazione tra gli occhi (**e**): questo valore lo si può semplicemente misurare con un righello ponendolo tra due occhi, ma un valore generico è 60mm.
Una volta recuperati questi dati possiamo calcolare la distanza schermo barriera (**d**) così:
$$
d = \frac{p \cdot r \cdot n}{e}
$$
Quindi prendendo in considerazione i dati del nostro schermo, ipotizzando di usare il plexiglass e di volere una distanza dal punto di fuoco di 600 mm, il calcolo sarà così:
$$
\frac{0,19389309mm \cdot 600mm \cdot 1,49}{60mm} = 2,88mm
$$
Ora che sappiamo la distanza che dev'esserci tra i PIXEL e la BARRIERA possiamo ragionare su come agire: dobbiamo prima di tutto bisogna sapere che tra l'LCD e il pannello di plastica/vetro che di solito riveste uno schermo ci sono già dai 0,5 mm all'1 mm di spazio vuoto, dei valori su cui però non ho trovato fonti affidabili che li sostengano, quindi di solito vado sui 0,5 mm.
Sapendo questo allora lo spessore extra che dovremmo aggiungere dovrà essere di:
$$
spessoreExtra = spessoreTotale - spessoreInterno
$$
quindi nel nostro caso lo spessore extra del **plexiglass dovrà essere di 2,33 mm** (variare questo numero porterà a un avvicinamento/allontanamento del punto di fuoco ideale).
### Installazione e allineamento
Ora possiamo finalmente applicare la barriera, attaccandola prima al plexiglass e poi poggiando il tutto sopra lo schermo.
Bisogna prestare attenzione però ad applicare in modo precisissimo la barriera al pannello in plexiglass/vetro, perché una qualsiasi piega, bolla d'aria o malformazione andrà a rovinare l'effetto generale.
Quello che consiglio è di "spalmarla" sopra il pannello con un righello non appena è stata stampata, perché per i primi minuti sembra che i fogli trasparenti siano leggermente appiccicosi, e questo può aiutarci per attaccarla.
Una volta fatto questo non ci basterà che allineare perfettamente il tutto sopra lo schermo andando a muovere il pannello finché non sarà nella posizione perfetta (all'inizio del file avevo parlato dei 2 tipi di allineamento desiderati) e infine bloccare la barriera in posizione in qualche modo (io uso dello scotch, ma sono sicuro ci siano modi migliori).
## Testing e Troubleeshoting

### Migliorare l'allineamento
Per essere sicuri che l'allineamento della barriera sia perfetto possiamo fare un piccolo test:
con un software di disegno che permette di lavorare con facilità sui singoli pixel (io uso ASEPRITE) dobbiamo creare un file della **stessa dimensione dello schermo** in cui andremmo a disegnare una colonna di **larghezza di 1 pixel** rossa e affianco una colonna della stessa larghezza ma bianca, continuando così fino alla fine dell'immagine (a un certo punto conviene usare copia e incolla).
Una volta fatto questo si dovrà impostare la visualizzazione dell'immagine a schermo intero, stando ATTENTI che l'immagine sia scalata al 100%, possibilmente con un software che assicuri la precisione dei pixel nella visualizzazione, sempre come ASEPRITE (consiglio nelle impostazioni di quest'ultimo di abbassare la _screen scaling_ nelle preferenze a 100%). Adesso poggiando la barriera sullo schermo, in base a come è allineata, potresti vedere delle linee curve od oblique rispetto allo schermo: il tuo obiettivo è cercare di raddrizzarle il più possibile finché non saranno rette, ruotando la barriera a destra o sinistra.
Non appena il risultato è soddisfacente dovresti essere in grado di chiudere un occhio, metterti alla distanza di fuoco predisposta dallo schermo e vedere, spostandoti leggermente a destra e a sinistra con la faccia, i colori rosso e bianco comparire alternati.
### Immagini "mischiate": effetto crosstalk
Se vedete che non riuscite a isolare perfettamente le 2 immagini o punti di fuoco, cioè che in un immagine per un occhio vedete anche un po' dell'altra in sottofondo, allora state sperimentando il crosstalk.
Questo effetto può essere dovuto da diverse cause:
- Hai la testa troppo lontana, vicina o disallineata in generale rispetto allo schermo.
- Le linee nere sono troppo piccole (o troppo grandi in certi casi).
- I calcoli sono stati fatti male.
- La tua stampante non riesce a stampare la barriera in maniera abbastanza precisa: questo è uno dei casi più probabili.
- Oppure potrebbe anche essere perché si sta usando un monitor con interfaccia VGA (non sono ancora sicuro di questa cosa ma usare un cavo VGA scadente _potrebbe_ provocare un po' di crosstalk)

![[crosstalk.jpg|500]]
## Risorse utili
⚠PRIMA DI COMINCIARE È IMPORTANTE SAPERE CHE QUESTA BARRIERA PERMETTE LA VISIONE, SOLO E SOLTANTO, DI IMMAGINI **INTERLACCIATE IN VERTICALE**, **VERTICALLY INTERLACED**, **INTERLEAVED COLUMNS** o ancora **VERTICALLY INTERLEAVED** (sono tutti sinonimi), E INOLTRE LA RISOLUZIONE DELLO SCHERMO DOVRÀ SEMPRE ESSERE IMPOSTATA A QUELLA NATIVA DI QUEST'ULTIMO⚠

Ok, ora abbiamo la nostra barriera, ma senza il supporto software giusto sarà impossibile usarla, ecco perché ci vengono in aiuto diversi siti e strumenti gratis e super utili:
##### Siti web
- www.stereo.jpn.org: questo sito ha una raccolta GIGANTE di video e immagini 3D, da poter visualizzare con letteralmente qualsiasi supporto, in più ha anche una sezione con degli strumenti molto utili. Nel visualizzatore online bisogna selezionare gli effetti _3DLCD_ o _V_INT_ (consiglio di usare la modalità HTML per gli strumenti).
##### Tools
###### [Ffmpeg](https://ffmpeg.org/)
È un programma multi piattaforma per la conversione di qualsiasi file multimediale e può aiutarci a creare delle immagini/video con la nostra modalità di visualizzazione 3D specifica. Per farlo bisogna partire da un file già in 3D, ma questo non è un problema perché il supporto per il formato a 3D L/R è molto popolare (quello dove ci sono due immagini una affianco all'altra), ed è possibile convertire i file da L/R a Vertical Interlaced.
Per farlo è possibile usare il comando:
```
ffmpeg -i /path/al/file/input -vf stereo3d=sbs2l:icl /path/al/file/output
```
Al posto di _sbs2l_ e _icl_ è possibile impostare il formato di input e di output del file, per input è possibile mettere quello che si vuole in base al caso, invece per output si possono mettere solo quelli di nostro interesse. La lista di argomenti completi è:

**INPUT***
- **sbsl**: Side-by-side completo, vista sinistra a sinistra
- **sbsr**: Side-by-side completo, vista destra a sinistra
- **sbs2l**: Side-by-side a metà larghezza, vista sinistra a sinistra
- **sbs2r**: Side-by-side a metà larghezza, vista destra a sinistra
- **abl**: Above-below completo, vista sinistra sopra
- **abr**: Above-below completo, vista destra sopra
- **ab2l**: Above-below a metà altezza, vista sinistra sopra
- **ab2r**: Above-below a metà altezza, vista destra sopra
- **tbl**: Top-bottom completo, vista sinistra sopra
- **tbr**: Top-bottom completo, vista destra sopra
- **tb2l**: Top-bottom a metà altezza, vista sinistra sopra
- **tb2r**: Top-bottom a metà altezza, vista destra sopra
- **al**: Solo vista sinistra (mono)
- **ar**: Solo vista destra (mono)
- **irl**: Interleaved rows, vista sinistra prima
- **irr**: Interleaved rows, vista destra prima

**OUTPUT**
- **icl**: interlacciato in verticale, vista sinistra prima
- **icr**: interlacciato in verticale, vista destra prima

Per l'output si può scegliere se usare _icl_ o _icr_, consiglio di provarle entrambe e vedere cosa esce meglio.
###### [3DSteroid](play.google.com/store/apps/details?id=jp.suto.stereoroid&hl=en_US&gl=US&pli=1)
Applicazione per Android utilissima per visualizzare immagini 3D, anche reperite dal web, e soprattutto permette di scattare foto 3D visualizzabili dal nostro schermo.
## Fonti
- [Forum thread](https://web.archive.org/web/20220816053625/https://www.mtbs3d.com/phpbb/viewtopic.php?t=1467&start=191) on mtbs3d by user "cybereality".
- [Wikipedia](https://en.wikipedia.org/wiki/Parallax_barrier).
- [A study of optimal viewing distance in a parallax barrier 3D display](https://www.researchgate.net/publication/256441068_A_study_of_optimal_viewing_distance_in_a_parallax_barrier_3D_display) (questo mi ha aiutato a capire meglio come funzionasse la barriera, ma non ho riportato molte informazioni da questa ricerca).
- Esperimenti e osservazioni personali.