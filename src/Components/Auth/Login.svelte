<script>
   import { supabase } from '../../supabaseClient'

   let email
   let password
   let loading = false

   const handleLoginForm = async () => {
      try {
         loading = true
         const { user, session, error } = await supabase.auth.signIn({
            email,
            password,
         })
         if (error) throw error
      } catch (error) {
         console.error(error.message)
      } finally {
         loading = false
      }
   }
</script>

<div id="container">
   <h1>Log in</h1>
   <form on:submit|preventDefault={handleLoginForm}>
      <div>
         <label for="email">Email</label>
         <input type="email" name="email" id="email" bind:value={email} />
      </div>
      <div>
         <label for="password">password</label>
         <input type="password" name="password" id="password" bind:value={password} />
      </div>
      <div>
         <input type="submit" value="login" disabled={loading} />
      </div>
   </form>
</div>
