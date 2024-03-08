<center><h1>Ovn temperatur: {Math.round(temperature)}°C</h1></center>
<script>
  import { onMount } from 'svelte';
  let temperature = 0;
  let knob;
  let ovenColor = 'white';

  onMount(async () => {
    const Nexus = (await import('nexusui')).default;
    knob = new Nexus.Dial('#knob', {
      'size': [75,75],
      'interaction': 'radial',
      'mode': 'relative', 
      'min': 0,
      'max': 250,
      'step': 0,
      'value': 0
    });

    knob.on('change', function(v) {
      temperature = v;
      ovenColor = temperature >= 200 ? 'red' : 'white'; 
    });
  });
</script>
<style>
  .center {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }
  .oven {
    width: 300px; 
    height: 300px; 
    border: 3px solid black;
    border-radius: 10px;
    position: relative;
    background-color: ovenColor;
  }
  .oven::before {
    content: "";
    position: absolute;
    top: 10px;
    left: 10px;
    width: 280px; 
    height: 280px; 
    border: 3px solid black;
    border-radius: 10px;
  }
  .knob {
    position: absolute;
    top: 10px; 
    left: 10px; 
  }
</style>
<div class="center">
  <div class="oven" style="background-color: {ovenColor}">
    <div id="knob" class="knob"></div>
  </div>
</div>
<div id="knob"></div>