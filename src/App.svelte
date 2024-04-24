<script>
	let inputValue = "";
	let todos = [];
	let completedTodos = [];
  
	function addTodo() {
	  if (inputValue.trim() === "") {
		alert("Veuillez entrer du texte pour la tâche.");
		return;
	  }
	  todos = [
		...todos,
		{
		  id: todos.length + 1,
		  contents: inputValue.trim(),
		  completed: false
		}
	  ];
	  inputValue = "";
	}
  
	function toggleTodo(todo) {
	  todo.completed = !todo.completed;
	  if (todo.completed) {
		completedTodos.push(todo);
		todos = todos.filter(item => item.id !== todo.id);
	  } else {
		completedTodos = completedTodos.filter(item => item.id !== todo.id);
		todos.push(todo);
	  }
	  // Mettre à jour les listes après modification
	  todos = [...todos];
	  completedTodos = [...completedTodos];
	}
  
	function removeTodoFromCompleted(todo) {
	  completedTodos = completedTodos.filter(item => item.id !== todo.id);
	}
  
	function editTodo(todo) {
	  inputValue = todo.contents;
	  removeTodoFromCompleted(todo);
	  todos = todos.filter(item => item.id !== todo.id);
	}
  </script>
  
  <input type="text" bind:value={inputValue} />
  <button on:click={addTodo}>Ajouter</button>
  
  <h2>Tâches à faire</h2>
  <ul>
	{#each todos as todo}
	  <li>
		<span class:completed={todo.completed}>{todo.contents}</span>
		<button on:click={() => toggleTodo(todo)}>Valider</button>
		<button on:click={() => editTodo(todo)}>Modifier</button>
	  </li>
	{/each}
  </ul>
  
  <h2>Tâches validées</h2>
  <ul>
	{#each completedTodos as todo}
	  <li>
		<span class:completed={todo.completed}>{todo.contents}</span>
		<button on:click={() => removeTodoFromCompleted(todo)}>Supprimer</button>
	  </li>
	{/each}
  </ul>
  