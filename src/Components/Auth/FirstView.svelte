<script>
   import { Link } from 'svelte-routing'
</script>

<div class="container">
   <div class="wrapper">
      <h1 class="catch">Hello</h1>
      <div class="button">
         <Link to="login">Log in</Link>
      </div>
      <p>or</p>
      <div class="button">
         <Link to="register">Register</Link>
      </div>
   </div>
</div>

<style>
    .container {
        overflow: hidden;
        width: 100%;
        height: 100vh;
        display: flex;
        justify-content: center;
        align-items: center;
    }
   .wrapper {
       padding: 2rem;
       display: flex;
       flex-direction: column;
       align-items: center;
       gap: .5rem;
       width: 80%;
       border-radius: 6px;
       border: 1px solid #ccc;
       text-align: center;
   }
   .catch {
       font-size: 3rem;
       margin-bottom: 2rem;
   }
   p {
       font-weight: normal;
       font-size: 1.2rem;
   }
   .button {
       width: 100%;
   }
   .button > :global(a) {
       display: inline-block;
       width: 100%;
       font-size: 1.5rem;
       background-color: #ddd;
       padding: 0.2rem 2rem;
       border-radius: 6px;
       color: #444;
       text-decoration: none;
   }
    .button > :global(a):hover {
        background: #888;
   }
</style>
