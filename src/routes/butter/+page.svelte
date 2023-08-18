<svelte:head>
	<title>Buttera !</title>
	<meta name="description" content="About this app" />
</svelte:head>

<script>
import Butter from 'buttercms';
const butter = Butter('4c70e6ea4d3f7b58e11a604674c85560940af298');

butter.page.retrieve('*', 'simple-page').then(response => console.log(response.data))


butter.content.retrieve(['song_harmony'])
.then(function(resp) {
        console.log(resp.data)
    })
    .catch(function(resp) {
        console.log(resp)
    });

</script>

<div class="container">
  <h1>HEllo Butter CMS</h1>
</div>

<footer>

</footer>