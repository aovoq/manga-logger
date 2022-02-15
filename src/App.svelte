<script>
   import { Router, Link, Route } from 'svelte-routing'
   import { user } from './sessionStore'
   import { supabase } from './supabaseClient'
   import Register from './Components/Auth/Register.svelte'
   import Login from './Components/Auth/Login.svelte'
   import Dashboard from './Components/Dashboard.svelte'

   user.set(supabase.auth.user())

   supabase.auth.onAuthStateChange((_, session) => {
      user.set(session.user)
   })

   const signOut = async () => {
      try {
         let { error } = await supabase.auth.signOut()
         user.set(null)
         if (error) throw error
      } catch (error) {
         console.error(error)
      }
   }
</script>

<Router>
   <nav>
      <ul>
         <li><Link to="/">Home</Link></li>
         <li><Link to="dashboard">Dashboard</Link></li>
         <li><Link to="login">Login</Link></li>
         <li><Link to="register">Register</Link></li>
         <li><a href="/" on:click|preventDefault={signOut}>Logout</a></li>
      </ul>
   </nav>
   <main>
      <Route path="login" component={Login} />
      <Route path="register" component={Register} />
      <Route path="dashboard" component={Dashboard} />
      <Route path="/">
         <h1>Home</h1>
         <p>To view the protected content, register or login to your account</p>
      </Route>
   </main>
</Router>
