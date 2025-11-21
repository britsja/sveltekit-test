<h1>Test page on Svelte</h1>
<p>Let's see how much easier this is compared to Leptos and Rust</p>
<script>
  let count = 0;
</script>

<h2>Hello SvelteKit 👋</h2>

<button on:click={() => count++}>
  Count is {count} (click here to make the count increase)
</button>
<h3>No usestate nonsense, nice!</h3>