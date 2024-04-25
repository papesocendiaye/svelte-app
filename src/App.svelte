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
  <style>
	/* Styles pour centrer la page au milieu */
	html, body {
	  display: flex;
	  justify-content: center;
	  align-items: center;
	  width: 100%;
	  height: 100%;
	  margin: 0;
	  background-color: #f5f5f5;
	}
  
	/* Conteneur principal */
	.container {
	  text-align: center;
	}
  
	/* Liste des tâches */
	ul {
	  list-style: none;
	  padding: 0;
	  margin: 0;
	}
  
	/* Éléments de la liste des tâches */
	li {
	  padding: 10px;
	  margin-bottom: 5px;
	  background-color: #f8f9fa;
	  border-radius: 5px;
	  transition: background-color 0.3s ease;
	  display: flex;
	  align-items: center;
	}
  
	/* Couleur du texte des tâches complétées */
	.completed {
	  text-decoration: line-through;
	  color: #adb5bd;
	}
  
	/* Styles pour les boutons */
	button {
	  margin-left: 10px;
	  padding: 5px 10px;
	  background-color: #007bff;
	  color: #fff;
	  border: none;
	  border-radius: 3px;
	  cursor: pointer;
	  transition: background-color 0.3s ease;
	}
  
	/* Hover sur les boutons */
	button:hover {
	  background-color: #0056b3;
	}
  </style>