<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>
<script>
  import { onMount } from 'svelte';

  let temperature = 0;
  let knob;

  onMount(async () => {
    const Nexus = (await import('nexusui')).default;

    knob = new Nexus.Dial('#knob', {
      'size': [75,75],
      'interaction': 'radial',     // "radial", "vertical", or "horizontal"
      'mode': 'relative', // "absolute" or "relative"
      'min': 0,
      'max': 250,
      'step': 0,
      'value': 0
    });

    knob.on('change', function(v) {
      temperature = v;
    });
  });
</script>

<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>

<h1>Oven Temperature: {Math.round(temperature)}°C</h1>

<div id="knob"></div>