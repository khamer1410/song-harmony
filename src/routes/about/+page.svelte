<svelte:head>
	<title>About</title>
	<meta name="description" content="About this app" />
</svelte:head>

<script>
  import { UnleashClient } from 'unleash-proxy-client';
  const TOKEN = '*:development.db0d4d2c1e72487eac8a176f99878eed5de6e98f5236a999e4a14fc4'

const unleash = new UnleashClient({
    url: 'http://localhost:4242/api/frontend',
    clientKey: TOKEN,
    appName: 'my-webapp',
});

window.unleash = unleash


unleash.on('ready', () => {
    if (unleash.isEnabled('hola')) {
        console.log('hola feature is enabled');
    } else {
        console.log('hola feature is disabled');
    }
});
console.log('poszło');

// Start the background polling
unleash.start();

</script>

<div class="text-column">
	<h1>About this app</h1>

	<p>
		This is a <a href="https://kit.svelte.dev">SvelteKit</a> app. You can make your own by typing the
		following into your command line and following the prompts:
	</p>

	<pre>npm create svelte@latest</pre>

	<p>
		The page you're looking at is purely static HTML, with no client-side interactivity needed.
		Because of that, we don't need to load any JavaScript. Try viewing the page's source, or opening
		the devtools network panel and reloading.
	</p>

	<p>
		The <a href="/sverdle">Sverdle</a> page illustrates SvelteKit's data loading and form handling. Try
		using it with JavaScript disabled!
	</p>
</div>
