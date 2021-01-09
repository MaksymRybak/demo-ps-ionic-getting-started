Il link al corso https://app.pluralsight.com/library/courses/ionic-getting-started/table-of-contents

Getting familiar with Ionic
	installiamo nodejs e vscode (un editor in base alle nostre preferenze)
	in questo corso useremo android studio per lanciare l'app all'interno di un emulatore
		per questo motivo installiamo ionic in questo modo "npm i -g @ionic/cli native-run cordova-res"
		native-run, serve x lanciare i pacchetti (aka librerie) native all'interno di emulatore o un device
		cordova-res, serve x per generare le icone native .. 
		creiamo il progetto digitando
			ionic start lawChoice blank --type=react --capacitor
			NOTA: qui useremo react, secondo l'autore e' il framework piu' facile da vedere se non si abbia nessuna conoscenza iniziale di un fw web
			il parametro blank serve per specificare il template del progetto che vogliamo usare 
			specificando il parametro --capacitor aggiungiamo la parte di cordova per integrazione con funzionalita' native del device (es. camera)
			NOTA: capacitor sostituisce cordova ed e' mantenuto dal team ionic 
	NOTA: ricordiamo che anche se stiamo sviluppando per mobile, un progetto ionic e' cmq un progetto web 
		lanciamo la web app digitando "ionic serve"
	struttura del progetto 
		package.json - pacchetti installati
		public / manifest.json - elenco di icone, questo file ha importanza quando lanciamo la nostra app come una PWA
		public / index.html - ormai e' uno standard, unico file HTML che abbiamo, caricato di default quando viene lanciata l'app
		src - cartella contenente il codice della nostra app
		src / index.tsx - il file contenente il codice typescript, entry point della nostra app 
			contiene vari import:
				React - libreria di react 
				ReactDOM - libreria che consente di creare i nostri componenti all'interno di un elemento del nostro DOM 
				App - componente root della nostra app 
				serviceWorker - di default e' disabilitato, come si vede nel codice ts 
			la riga 
				ReactDOM.render(<App />, document.getElementById('root'));
				serve a renderizzare il componente <App /> all'interno di elemento con id="root" (elemento presente in index.html)
		src / App.tsx - il primo componente della nostra app 
			anche questo file contiene vari import 
			il nostro componente e' di tipo React.FC (FC sta per Functional Component)
			i componenti in react sono delle funzioni, e il nostro componente viene definito usando una funzione 
		src / pages
			Home.tsx - contiene la prima pagina dell'app <IonPage> 
			viene referenziato il componente ExploreContainer - componente con un markup semplice (giusto per darci un idea)
			questo componente definisce l'interfaccia ContainerProps - puo' essere usata per passare i parametri al nostro componente 
			NOTA: alla fine del codice di un componente vediamo un export default <nome componente>, serve per poter usarlo all'interno di altri componenti / pagine 
	routing
		ionic in background usa la libreria di routing di react 
		vedere App.tsx contenente le rotte di default 
			IonRouterOutlet - controlla il rendering di componenti in base alla rotta richiesta, responsabile anche dell'animazione
			<Route path="/home" component={Home} exact={true} />	--{Home} e' una espressione, viene impostato il riferimento al componente Home 
			<Route exact path="/" render={() => <Redirect to="/home" />} />	--se la rotta e' /, viene eseguito il redirect
		la rotta di partenza (quando viene avviata l'app) e' specificata nell'index.html, ed e' <base href="/" />
	componenti
		abbiamo la possibilita' di creare i nostri componenti da zero
		ionic cmq fornisce una librerie di componenti, e' consigliato prima valutare se non esista gia' qualcosa di pronto 
		il componente root della nostra app e' IonApp 
		IonPage e' il componente base per una pagina della nostra app
			una pagina e' un componente con una rotta associata
		IonGrid e' il componente di riferimento per gestire la griglia
			si basa su flex
		IonButton x pulsanti, puo' contenere il testo, icona, o entrambi
		IonItem per costruire la lista di elementi
		IonCard per rappresentare delle card 
		consultare la guida ufficiale per vedere la lista completa di componenti a disposizione
	funzionalita' native 
		usiamo libreria Capacitor (successore di Cordova)
		contiene diversi plugin che possiamo usare per accedere alle funzionalita' native di device 
		ci sono i plugin free (sviluppati e supportati dalla community) e a pagamento 
		esempio di plugin
			Camera (mobile e pwa, camera del nostro dispositivo mobile, la webcam del nostro desktop)
			Keyboard (solo x android e ios, per mostrare o nascondere la tastiera)
			Geolocation (x tutte le piattoforme, location info)
			File (x accedere al file system del dispositivo)
		oltre ai plugin che ci permettono di accedere alle funzionalita' native abbiamo anche i plugin social
			Facebook (x accedere a fb, per esempio usare il sistema di login di db)
			Instagram (x condividere le foto su instagram)
			Paypal (x processare pagamenti)
			Admob (facilita integrazione della pubblicita' nella nostra app)
		i plugin a pagamento che possano essere utili
			Ionic auth connect - login e registrazione utenti usando diversi auth provider 
			Ionic offline storage - salvataggio dei dati su SQLite locale a device 
			Ionic identity vault - sistema di identity authentication (es. usando autenticazione biometrica, touch-id, face-id)
	installazione di android 
		scarichiamo android studio dal sito ufficiale 
		(android studio e' disponibile x windows, mac e linux)
		assicuriamoci quando installiamo che il flag 'android virtual device' e' stato impostato 
		apriamo studio -> apriamo impostazioni (SDK manager) -> sezione Android SDK -> selezioniamo 'Android SDK command-line tools' 
			-> controlliamo che siamo installati 'Android emulator' e 'Android SDK platform tools'
		se stiamo sviluppando per diverse piattaforme android, il tab 'SDK Plaforms' della sezione 'Android SDK' ci consente installare dipendenze necessarie
		salviamo da qualche parte il path di Android SDK recuperabile da SDK Manager
		apriamo AVD Manager per vedere se abbiamo al meno un device virtuale configurato (nel momento di installazione di studio ne viene configurato uno)
		(abbiamo installato e configurato i pacchetti necessari di android studio, lo possiamo chiudere)
		apriamo la linea di comando e navighiamo al path di Android SDK (es. C:\Users\Maks\AppData\Local\Android\Sdk) -> 
			NOTA: solo se il PC ha il processore AMD dobbiamo lanciare silent_install.bat dalla cartella {androd sdk intall path}\extras\google\Android_Emulator_Hypervisor_Driver
			se siamo su windows dobbiamo aggiungere un paio di variabili di sistema	(x altri OS consultare la documentazione)
				-> apriamo la finestra contenente le variabili di sistema
				-> aggiundiamo una nuova variabile di sistema ANDROID_SDK_HOME = {il path di android sdk recuperabile da android studio}
				-> aggiungiamo i seguenti path alla variabile Path:
					%ANDROID_SDK_HOME%\cmdline-tools\latest\bin
					%ANDROID_SDK_HOME%\platform-tools
					%ANDROID_SDK_HOME%\emulator
					%ANDROID_SDK_HOME%\build-tools
			con questo abbiamo android tools utilizzabili dalla linea di comando 
		navighiamo dalla linea di comando alla cartella del nostro progetto
		eseguiamo la build digitando 'ionic build'
		aggiungiamo le dipendenze di android digitando 'ionic cap add android' (generazione pacchetti nativi di android)
		ogni volta che eseguiamo la build, per allineare la cartella contenente il progetto standalone di android eseguiamo il comando
			ionic cap copy 
		ogni volta che facciamo una modifica al progetto nativo (es. aggiunta/rimozione di un plugin) dobbiamo eseguire il comando 
			ionic cap sync 
		per aprire il progetto android eseguiamo il comando
			npx cap open andorid 
			NOTA: npx e' il runtime di npm che consente di lanciare i pacchetti senza di averli prima installati 
		viene aperto android studio che ci permette di lanciare l'app all'interno di emulatore
		NOTA: possiamo lanciare la nostra app anche su un device fisico 
Sviluppo app mobile usando Ionic
	