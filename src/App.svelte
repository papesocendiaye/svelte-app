<script>
	let inputValue = "";
	let todos = [];
	function addTodo() {
	  if (inputValue === "") alert("allert");
	  todos = [
		...todos,
		{
		  contents: inputValue,
		  completed: false
		}
	  ];
	  inputValue = "";
	}
	function toggleTodo(i) {
	  todos = [
		...todos.slice(0, i),
		{
		  ...todos[i],
		  completed: !todos[i].completed
		},
		...todos.slice(i + 1)
	  ];
	}
  </script>
  
  <style>
	li.completed {
	  text-decoration: line-through;
	  color: #e4e4e4;
	}
  </style>
  
  <input type="text" bind:value={inputValue} />
  <button on:click={addTodo}>submit</button>
  
  <ul>
	{#each todos as todo, i}
	  <!-- svelte-ignore a11y-click-events-have-key-events -->
	  <li
		on:click={() => toggleTodo(i)}
		class={todo.completed ? 'completed' : ''}>
		{todo.contents}
	  </li>
	{/each}
  </ul>
  