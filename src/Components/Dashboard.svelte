<script>
   import { user } from './../sessionStore'
</script>

<h1>Welcome</h1>
{#if $user}
   <p>Your email address is {$user.email}</p>
{/if}
<p>Your protected content here.</p>
