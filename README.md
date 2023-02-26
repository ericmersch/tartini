

<html>
<head>
  <meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
  <link rel="stylesheet" href="https://www.w3schools.com/w3css/4/w3.css">
</head>

<body>

<p>
We are familiar with the combination of colours: it is well known that adding green and red light result in the perception of yellow. But we are usually less concious of a similar phenomenon occuring with sound: when adding two pure sine waves of 800Hz and 1000Hz, one can hear a third sound at 200 Hz. This tone is not present in the acoustic signal, but it is thought to result from a non-linear phenomenon in the inner ear. These resultant tones fascinate me because they are like a ghost tones, or illusions. One call them Tartini tones, or resultant tones. 
<br/>
When adding two sine waves of fequencyes f1 and f2, the most common resultant tones frequencies are f1-f2, f1+f2, 2 f1-f2, 2 f2-f1.
<br/>
<br/>
Change the frequencies f1 and f2 of the component signals and press the buttons to here the tones and then press on the "f1-f2, f1+f2, 2 f1-f2, 2 f2-f1" to compare what you heard.
<br/>
<br/>
More information can be found here:
<br/>
</p>
<a href="https://en.wikipedia.org/wiki/Combination_tone">https://en.wikipedia.org/wiki/Combination_tone</a>
<br/>
<div>
  <img src="466px-Giuseppe_Tartini.jpg">
</div>

<br/>
  frequency f1 <input type="range" id="fIn1" min="50" max="1200" oninput="show()"/><span id="fOut1"></span><br/>

  frequency f2 <input type="range" id="fIn2" min="50" max="1200" oninput="show()"/><span id="fOut2"></span><span id="vOut"></span><br/>

  <br/>


<p>Components only</p>
  <button onclick="osc1()">only f1</button>
  <button onclick="osc2()">only f2</button>
  
  <p>The two components together</p>
  <button onclick="osc12()">f1 and f2</button>
  
    <p>The resulting tones only</p>
  <button onclick="tartini1()">f1-f2</button>
  <button onclick="tartini2()">f1+f2</button>
  <button onclick="tartini3()">2 f1-f2</button>
  <button onclick="tartini4()">2 f2-f1</button>
  

  <p id="t1"></p>
  <p id="t2"></p>
  <p id="t3"></p>
  <p id="t4"></p>

  <script>
        
  audioCtx = new(window.AudioContext || window.webkitAudioContext)();

  show();
        
  function show() {
  	f1 = (document.getElementById("fIn1").value);
  	document.getElementById("fOut1").innerHTML = f1 + ' Hz';

  	f2 = (document.getElementById("fIn2").value);
  	document.getElementById("fOut2").innerHTML = f2 + ' Hz';
            
        fR1 = f1 - f2;
        fR2 = f1-(-f2);
        fR3 = 2*f2 - f1;
        fR4 = 2*f1 - f2;
        document.getElementById("t1").innerHTML = 'f1-f2 = '+ fR1 + ' Hz';
        document.getElementById("t2").innerHTML = 'f1+f2 = '+ fR2 + ' Hz';
        document.getElementById("t3").innerHTML = '2f2-f1 = '+ fR3 + ' Hz';
        document.getElementById("t4").innerHTML = '2f1-f2 = '+fR4 + ' Hz';
            
}
       
        
        
  function player (freq) {

            
  var osc = audioCtx.createOscillator();
  var gainNode = audioCtx.createGain();

  osc.connect(gainNode);
  gainNode.connect(audioCtx.destination);

  gainNode.gain.value = 0.1;
  osc.frequency.value = freq;
  osc.type = "sine";

  osc.start();

  setTimeout(
    function() {
      osc.stop();
    },
    5000
  );
  };
        

        function osc1 () {
            player (f1);
        };
        function osc2 () {
            player (f2);
        };
        
        function osc12 () {
            player (f1);
            player (f2);
        };
        
        function tartini1 () {
            player (fR1);
        };
        function tartini2 () {
            player (fR2);
        };
        function tartini3 () {
            player (fR3);
        };
        function tartini4 () {
            player (fR4);
        };
    </script>
</body>
</html>
