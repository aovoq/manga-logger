<script>
   import { Router, Link, Route, navigate } from 'svelte-routing'
   import { user } from './lib/sessionStore.js'
   import { supabase } from './lib/supabaseClient.js'
   import Register from './Components/Auth/Register.svelte'
   import Login from './Components/Auth/Login.svelte'
   import Dashboard from './Components/Dashboard.svelte'
   import Profile from './Components/Auth/Profile.svelte'
   import FirstView from './Components/Auth/FirstView.svelte'
   import Redirect from './Components/Redirect.svelte'

   user.set(supabase.auth.user())

   supabase.auth.onAuthStateChange((event, session) => {
      if (event === 'SIGNED_IN') user.set(session.user)
   })

   const signOut = () => {
      supabase.auth.signOut()
      user.set(false)
      navigate('/')
   }
</script>

<svelte:head>
   <link href="https://fonts.googleapis.com/icon?family=Material+Icons+Outlined" rel="stylesheet">
</svelte:head>

<Router>
   {#if $user}
      <nav>
         <ul>
            <li><a href="/" on:click|preventDefault={signOut}>Logout</a></li>
            <li>
               <Link to="dashboard">Dashboard</Link>
            </li>
            <li>
               <Link to="profile">Profile</Link>
            </li>
         </ul>
      </nav>
   {/if}

   <main>
      {#if $user}
         <Route path="dashboard" component={Dashboard}/>
         <Route path="profile" component="{Profile}"/>
      {:else}
         <Route path="login" component={Login}/>
         <Route path="register" component={Register}/>
         <Route path="/" component="{FirstView}"/>
      {/if}
      <Route path="*" component="{Redirect}"/>
   </main>
</Router>

<style>
    ul {
        display: flex;
        justify-content: space-between;
        padding: 0 30px;
    }

    :global(html) {
        font-size: 62.5%;
    }

    :global(body) {
        background: #F6F6F6;
        font-family: Roboto, sans-serif;
        font-weight: bold;
    }

    :global(*, *::before, *::after) {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }
</style>
