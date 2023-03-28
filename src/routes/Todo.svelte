<script>
     let todoItem = '';
     let todoList= [];

     function add() {
          if (todoItem == ''){
               return;
          }
          todoList = [...todoList, {
               text: todoItem,
               done: false
          }]
          todoItem = '';
     }
     
     function removeThis(index){
          todoList.splice(index, 1);
          todoList = todoList;
     }
     function clearDone(){
          todoList = todoList.filter(t => !t.done);
     }
     function clearAll() {
          todoList = [];
     }
</script>

<form on:submit|preventDefault={add}>
     <input bind:value={todoItem} type="text" autofocus/><button type="submit">Add</button>
</form>

<ul>
     {#each todoList as item, index}
          <li>
               <input type="checkbox" bind:checked={item.done}>
               <span class:done={item.done}>{item.text}</span>
               <span on:click={() => removeThis(index)} on:keypress={() => removeThis(index)} class="remove"></span>
          </li>
     {/each}
</ul>

<button on:click={clearDone}>Clear Done</button>
<button on:click={clearAll}>Clear All</button>

<style>
     ul{
          list-style: none;
     }
     .done {
          text-decoration: line-through;
          color: rgb(192, 192, 192);
     }
     .remove {
          height: 1rem;
          width: 1rem;
          display: inline-block;
          background: url(src/routes/img/trash-can-icon-256.png);
          background-size: 100% auto;
          cursor: pointer;
     }
     button {
          border: none;
          padding: 0.3em;
          background-color: rgb(205, 72, 63);
          color: rgb(204, 204, 204);
          font-weight: bold;
          border-radius: 4px;
          cursor: pointer;
          font-family: Verdana, Geneva, Tahoma, sans-serif;
     }
</style>

