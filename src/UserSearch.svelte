<script>
  import User from "./User.svelte";

  let usernameQuery = "";
  let user;

  const handleSubmit = async (e) => {
    e.preventDefault();

    const response = await fetch(
      `https://api.github.com/users/${usernameQuery}`
    );
    const data = await response.json();

    user = data;
  };
</script>

<div class="user-search">
  <h2>Search for Users</h2>

  <form on:submit={handleSubmit}>
    <input type="text" bind:value={usernameQuery} />
    <button>Search</button>
  </form>

  {#if user}
    <User username={user.login} avatar={user.avatar_url} />
  {/if}
</div>

<style>
  .user-search {
    padding: 20px;
    border-radius: 10px;
    margin-bottom: 50px;
    background: #efefef;
  }

  h2 {
    margin: 0 0 15px;
  }
</style>
