<script>
   import { supabase } from '../../supabaseClient'

   let email
   let password
   let loading

   const handleRegisterForm = async () => {
      try {
         const { user, session, error } = await supabase.auth.signUp({
            email,
            password,
         })
         if (error) throw error
         alert('success')
      } catch (error) {
         alert(error.message)
      }
   }
</script>

<div id="container">
   <h1>Sign Up</h1>
   <form on:submit|preventDefault={handleRegisterForm}>
      <div>
         <label for="email">Email</label>
         <input type="email" name="email" id="email" />
      </div>
      <div>
         <label for="password">Password</label>
         <input type="password" name="password" id="password" />
      </div>
      <div>
         <input type="submit" value="Register" disabled={loading} />
      </div>
   </form>
</div>
