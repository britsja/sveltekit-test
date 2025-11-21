<script>
  import { fade } from "svelte/transition";
  let count = 0;
  let name = "World";
  let a = 2;
  let b = 5;
  $: sum = a + b; // magically recalculates whenever a or b changes
  let value = 0;
  $: console.log("Value changed:", value);
  let todos = [];
  let newTodo = "";
  let active = false;  
  let show = true;
  let name2 = "";
  let count2 = 0;
  $: greeting = name2 ? `Hello, ${name2}!` : "Type your name below";

  let userPromise = new Promise(resolve =>
    setTimeout(() => resolve({ name: "Svelte User" }), 2000)
  );

  function addTodo() {
    if (newTodo.trim()) {
      todos = [...todos, newTodo];
      newTodo = "";
    }
  }

  function removeTodo(i) {
    todos = todos.filter((_, index) => index !== i);
  }
</script>

<style>
  .box { padding: 10px; border: 2px solid gray; }
  .active { border-color: limegreen; background: #e9ffe9; }
</style>

<div class="flex flex-row">
  <div class="p-10">
    <h1>Test page on Svelte</h1>
    <p>Let's see how much easier this is compared to Leptos and Rust</p>

    <h2>Hello SvelteKit 👋</h2>

    <button on:click={() => count++}>
      Count is {count} (click here to make the count increase)
    </button>
    <h3>No usestate nonsense, nice!!!</h3>

    <div class="w-1/2 border-t border-gray-300 my-6"></div>

    <h3>Two-way binding</h3>

    <input bind:value={name} placeholder="Type your name" />

    <p>Hello {name}!</p>

    <div class="w-1/2 border-t border-gray-300 my-6"></div>

    <h3>Reactive values</h3>

    <input type="number" bind:value={a} />
    <input type="number" bind:value={b} />

    <p>{a} + {b} = {sum}</p>

    <div class="w-1/2 border-t border-gray-300 my-6"></div>

    <h3>Reactive blocks</h3>
    <input type="range" min="0" max="100" bind:value={value} />
    <p>Slider value: {value}</p>

    <div class="w-1/2 border-t border-gray-300 my-6"></div>

    <h3>Simple todo list (no boilerplate!)</h3>

    <input bind:value={newTodo} placeholder="New todo..." />
    <button on:click={addTodo}>Add</button>

    <ul>
      {#each todos as todo, i}
        <li>
          {todo}
          <button on:click={() => removeTodo(i)}>❌</button>
        </li>
      {/each}
    </ul>

    <div class="w-1/2 border-t border-gray-300 my-6"></div>

    <h3>Class toggling</h3>

    <div class="box" class:active={active}>
      This box is {active ? "ACTIVE" : "INACTIVE"}
    </div>

    <button on:click={() => active = !active}>
      Toggle active
    </button>       
  </div>
  <div class="p-10">
    <h3>Transitions</h3>

    <button on:click={() => show = !show}>
      Toggle box
    </button>

    {#if show}
      <div transition:fade style="padding: 20px; margin: 10px; background: #c4ef17;">
        I fade in and out! 👋
      </div>
    {/if}
    <div class="w-1/2 border-t border-gray-300 my-6"></div> 

    <h3>Await block</h3>

    {#await userPromise}
      <p>Loading user...</p>
    {:then user}
      <p>Hello {user.name}!</p>
    {:catch error}
      <p>Error: {error.message}</p>
    {/await}

    <div class="w-1/2 border-t border-gray-300 my-6"></div>

    <h3>Mini Svelte Showcase</h3>

    <input bind:value={name2} placeholder="Your name" />
    <p>{greeting}</p>

    <button on:click={() => count2++}>
      Count2 = {count2}
    </button>

    {#if count2 > 5}
      <p transition:fade>You clicked more than 5 times 🎉</p>
    {/if}

  </div>
</div>