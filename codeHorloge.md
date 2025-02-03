# 🕰️ Horloges en différents langages 🕰️

## 1. Horloge en <a href="https://www.javascript.com/" target="_blank"><img style="margin: 10px" src="images/js.png" alt="JavaScript" title="JavaScript" height="50" /></a> 
 
``` 
<span class="date"><script type="text/javascript"> 
		var date = new Date();
		var a = date.getFullYear();
    	var b = date.getMonth()+1;
		var c = date.getDate();
		if( b < 10 ){ b = '0' + b; };
		if( c < 10 ){ c = '0' + c; };
		var newdate = c + '/' + b + '/' + a
		document.write(newdate);</script></span>
		<div style="margin-top: 10px;"><span id="horloge" class="date">00:00:00</span></div>
			<script>
				function miseAJourHorloge() {
					let date = new Date();
					let heures = date.getHours().toString().padStart(2, '0');
					let minutes = date.getMinutes().toString().padStart(2, '0');
					let secondes = date.getSeconds().toString().padStart(2, '0');

					document.getElementById("horloge").textContent = `${heures}:${minutes}:${secondes}`;
				}

				// Met à jour l'horloge chaque seconde
				setInterval(miseAJourHorloge, 1000);

				// Mise à jour immédiate au chargement
				miseAJourHorloge();
			</script>
		</div>
```
## 2. Horloge en <a href="https://www.php.net/" target="_blank"><img style="margin: 10px" src="images/php.png" alt="PHP" title="PHP" height="50" /></a>

``` 		  
<div style="margin-top:30px;"><span class="date">
		<?php 
		$dt = time();
		echo date( "d/m/Y", $dt );
		?></span>
		<div style="margin-top: 10px;"><span id="heurePhp" class="date">
        <?php 
            //date_default_timezone_set("Europe/Paris"); // Définir le fuseau horaire
            echo date("H:i:s"); 
        ?>
		</span>
		<script>
			function miseAJourHorloge() {
				let date = new Date();
				let heures = date.getHours().toString().padStart(2, '0');
				let minutes = date.getMinutes().toString().padStart(2, '0');
				let secondes = date.getSeconds().toString().padStart(2, '0');

				document.getElementById("heurePhp").textContent = `${heures}:${minutes}:${secondes}`;
			}

			// Mise à jour toutes les secondes
			setInterval(miseAJourHorloge, 1000);

			// Mise à jour immédiate au chargement
			miseAJourHorloge();
		</script>
		</div>
``` 
## 3. Horloge en <a href="https://www.python.org/" target="_blank"><img style="margin: 10px" src="images/python.png" alt="Python" title="Python" height="50" /></a> et <a href="https://www.python.org/" target="_blank"><img style="margin: 10px" src="images/pyodide.png" alt="Pyodide" title="Pyodide" height="50" /></a>

``` 
<div><span id="datePython" class="date">Chargement...</span>
			<div style="margin-top: 10px;"><span id="heurePython" class="date">Chargement...</span></div> 
			<script>
				async function initPyodide() {
					window.pyodide = await loadPyodide();
					console.log("Pyodide chargé");
					runDatePython();  // Afficher la date dès que Pyodide est prêt
					startClock();     // Démarrer l'horloge
				}
			
				async function runDatePython() {
					if (!window.pyodide) return;
			
					let pythonCode = `
			from datetime import datetime
			d = datetime.today()
			m = f"{d.month:02d}"
			j = f"{d.day:02d}"
			result1 = f"{j}/{m}/{d.year}"
			result1
					`;
			
					let result1 = await window.pyodide.runPythonAsync(pythonCode);
					document.getElementById("datePython").textContent = result1;
				}
			
				async function runTimePython() {
					if (!window.pyodide) return;
			
					let pythonCode = `
			from datetime import datetime
			h = datetime.now()
			result = h.strftime("%H:%M:%S")
			result
					`;
			
					let result = await window.pyodide.runPythonAsync(pythonCode);
					document.getElementById("heurePython").textContent = result;
				}
			
				async function startClock() {
					runTimePython();  // Exécuter immédiatement une première fois
					setInterval(runTimePython, 1000);  // Mettre à jour toutes les secondes
				}
			
				window.onload = initPyodide;
			</script></div>
```