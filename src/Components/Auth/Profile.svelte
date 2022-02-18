<script context="module">
   import { supabase } from '../../lib/supabaseClient'
   import { user } from '../../lib/sessionStore'
</script>

<script>
   let loading = true
   let username = ''

   const getUsername =  () => {
      try {
         loading = true
         username = $user.user_metadata.username
      } finally {
         loading = false
      }
   }

   const updateUsername = async () => {
      try {
         loading = true
         let {user,error} = await supabase.auth.update({data: {username}})
         if (error) throw error
      } catch (error) {
         console.error(error)
      } finally {
         loading = false
      }
   }
</script>

<form use:getUsername on:submit|preventDefault={updateUsername}>
   <div>
      <label for="email">Email : </label>
      <input type="email" id="email" name="email" bind:value={$user.email} disabled>
   </div>
   <div>
      <label for="username">UserName : </label>
      <input type="text" id="username" name="username" bind:value={username} />
   </div>
   <div>
      <input type="submit" value={loading ? 'Loading...' : 'Update'} disabled={loading} />
   </div>
</form>
