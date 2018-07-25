---
layout: post
title:  "Markdown preview e LiveReload in SublimeText."
date:   2017-02-11
categories: enviroment
summary: Come settare un corretto ambiente di sviluppo.  
featured: no
---

Molte applicazioni web supportano il Markdown come linguaggio di scrittura. Ad esempio **GitHub Pages**, il sistema di sviluppo web **Jekyll** o il famoso CMS **Wordpress** (al momento della scrittura solo su piattaforma wordpress.com). 

![picture alt](img/thethaw_header.jpg "Title is optional")

## Perché usare questi tools. 
Lo scopo di usare Markdown Preview e LiveReload in SublimeText è quello di salvare/aggiornare un file scritto in Markdown e vederne l'anteprima via browser premendo la sola combinazione tasti `ctrl+b` e `ctrl+s` (sempre e solo in ambiente SublimeText)!

### Cosa succede nella pratica

Preso un file con estensione `.md`, vogliamo vederne il contenuto (o anteprima) in formato HTML. In pratica nel file `.md` scriverò usando codice Markdown. Quando il file `.md` verrà salvato sarà creato un file `.html` in modo da visualizzarlo sul browser. Una cosa molto bella è che quando si effettuano delle modifiche al file `.md`, verrà aggiornato in automatico il file `.html` e l'anteprima sul browser. 

## Requisiti software

Sono necessari i seguenti programmi che devono essere già presenti (quindi installati) sul PC/MAC: 

* l'editor di testo SublimeText 2 o 3.
* un browser web Chrome (usato nel nostro esempio), Firefox o Safari.

## Cosa verrà installato

Al termine della procedura spiegata di seguito, nel PC/MAC avremo:

- [ ] l'editor di testo SublimeText con Markdown Preview (installato) e il plugin LiveReload (installato e configurato).
- [ ] un browser web (nel nostro caso Chrome) con LiveReload (installato e configurato). 

## Markdown Preview

È necessario installarlo solo in SublimeText editor.

1. Aprire l'editor SublimeText 2/3
2. Premere i tasti cmd + shift + p. 
	
	- Se già presente si aprirà Package Control. 
	- Se non presente installare Package Control (https://packagecontrol.io/installation). 

3. Digitare "Package Control: Install Package" + Invio

4. Digitare "Markdown Preview" + Invio, parte l'installazione. Nota che alla base dell'editor è possibile visualizzare lo stato dell'esecuzione dei comandi inseriti.

5. Riavvia l'editor SublimeText (chiudi e riapri il programma).

## LiveReload plugin

LivePreload va installato sia in SublimeText e sia nel browser. 

### Installare LiveReload in SublimeText

In ST LiveReload serve per creare un canale di comunicazione tra editor e browser.

1. Aprire l'editor SublimeText 2/3
2. Premere i tasti cmd + shift + p. 
	
	- Se già presente si aprirà Package Control. 
	- Se non presente installare Package Control (https://packagecontrol.io/installation). 

3. Digitare "Package Control: Install Package" e premere Invio 

4. Digitare "LiveReload" e premere Invio, parte l'installazione. 

### Configurare LiveReload in SublimeText

1.  andare in `Preferences > Package Settings > LiveReload > Setting - Default` e incollare il seguente testo: 

	```
	{ 
	   "enabled_plugins": [ 
	       "SimpleReloadPlugin", 
	       "SimpleRefresh" 
	   ]
	}
	```

2. Riavvia l'editor SublimeText (chiudi e riapri il programma).

### Installare LiveReload nel browser

Nel browser LiveReload serve per aggiornare in automatico la pagina web. Il plugin una volta avviato, esegue un monitoraggio del file .html aperto nel browser e ne aggiorna il contenuto quando modificato. In pratica è come se venisse prenuto F5 sul browser.

* **Firefox:** http://download.livereload.com/2.1.0/LiveReload-2.1.0.xpi 
* **Chrome:** https://chrome.google.com/webstore/detail/livereload/jnihajbhpnppcggbcgedagnkighmdlei 
* **Safari:** http://download.livereload.com/2.1.0/LiveReload-2.1.0.safariextz 



### Configurare LiveReload in Chrome

Avendolo già installato in precedenza, sul browser troveremo l'icona del plugin LiveReload. 
	
*  digitare nell'URL del browser il testo seguente `chrome://extensions/` per accedere alle estensioni/plugin installati. Cercare LiveReload e spuntare `Consenti l'accesso agli URL dei file`.

## Cosa è stato installato

A questo punto nel PC/MAC abbiamo:

- [x] l'editor di testo SublimeText con Markdown Preview (installato) e il plugin LiveReload (installato e configurato).
- [x] un browser web (nel nostro caso Chrome) con LiveReload (installato e configurto).  

## Istruzioni d'uso

1. **Aprire un file `.md` in SublimeText.** Il file dovrà contenere del testo scritto in codice Markdown.

2. **Creazione automatica di un file `.html`.** Premere i tasti `ctrl` + `b` (Windows/Linux) o `cmd` + `b` (Mac). Verrà creato un file `.html` con lo stesso nome del file `.md`.

3. **Aprire il file `.html` nel browser.** Si vedrà il testo del file `.html`.

4. **Nel browser premere l'icona LiveReload.** 

	![picture alt](img/livereload_browser_icon.png "Title is optional")

	Quando premuta, si abilita la sincronizzazione tra browser e SublimeText: il browser se vede che il file `.html` è stato modificato, aggiorna in automatico la pagina visualizzata.

5. **Aggiornamento automatico.** In sublimeText modificare il testo del file `.md` e premere i tasti seguenti ogni volta che si modifica il file `.md`:
	* `ctrl` + `b` per generare/aggiornare il file `.html` 
	* `ctrl` + `s` per salvare il file `.md` ed eseguire il refresh della pagina `.html` aperta nel browser (nota: è necessario che la pagina web sia aperta). 

## Credits

* Sublime Text 2/3 Markdown Preview (https://github.com/revolunet/sublimetext-markdown-preview)

* Install LiveReload on Sublime Text 3 (http://stackoverflow.com/questions/25886011/how-do-i-install-livereload-on-sublime-text-3)

### User as Developer 
 Ivan Garrini - http://www.twitter.com/ivangarrini