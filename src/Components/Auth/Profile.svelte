<script context="module">
   import { supabase } from '../../lib/supabaseClient'
   import { user } from '../../lib/sessionStore'
</script>

<script>
   let loading = true
   let username = ''

   const getProfile = async () => {
      try {
         loading = true
         const user = supabase.auth.user()

         let { data, error, status } = await supabase
            .from('profiles')
            .select(`username, website, avatar_url`)
            .eq('id', user.id)
            .single()

         if (error && status !== 406) throw error

         if (data) {
            username = data.username
         }
      } catch (error) {
         console.error(error)
      } finally {
         loading = false
      }
   }

   const updateProfile = async () => {
      console.log('submit')
      try {
         loading = true
         const user = supabase.auth.user()

         const updates = {
            id: user.id,
            username,
            updated_at: new Date(),
         }

         let { error } = await supabase.from('profiles')
         .upsert(updates, {returning: 'minimal'})

         if (error) throw error
      } catch (error) {
         console.error(error)
      } finally {
         loading = false
      }
   }
</script>

<form use:getProfile on:submit|preventDefault={updateProfile}>
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
