<script context="module">
   import { user } from '../../lib/sessionStore.js'
   import { Link } from 'svelte-routing'
</script>

<div class="container">
   <h1>MangaLogger</h1>
   <Link to="/profile" class="user_button">
      <div class="user_wrapper">
         <p>{$user.user_metadata.username}</p>
         <span class="material-icons-outlined user_icon">
            account_circle
         </span>
      </div>
   </Link>
</div>

<style>
    .container {
        display: flex;
        justify-content: space-between;
        padding: 1.5rem;
    }

    :global(.user_button) {
        padding: 0.1rem 0.8rem;
        text-decoration: none;
        background: #FAE14A;
        display: inline-block;
        border-radius: 999px;
        color: #444;
    }

    .user_wrapper {;
        height: 100%;
        display: flex;
        align-items: center;
    }

    .user_icon {
        font-size: 2rem;
    }
</style>
