<script>
   import { supabase } from '../../lib/supabaseClient.js'
   import { user } from '../../lib/sessionStore.js'

   let title, desc, number
   let loading = false
   const handleSubmit = async() => {
      try {
         loading = true
         if (title === undefined || desc === undefined || number === undefined) throw 'Please input field'
         const {error } = await supabase.from('comic_log')
            .insert([{title, desc, number, user_id: $user.id}])
         if (error) throw error
      } catch (e) {
         console.error(e)
      } finally {
         loading = false
      }

   }
</script>

<h1>Add</h1>
<form on:submit|preventDefault={handleSubmit}>
   <input type="text" name="title" bind:value={title} placeholder="title">
   <input type="text" name="desc" bind:value={desc} placeholder="desc">
   <input type="text" name="number" bind:value={number} placeholder="vol.">
   <input type="submit" value="add" disabled={loading}>
</form>

<style>
    form {
       display: flex;
       justify-content: space-between;
   }
    input {
        width: 25%;
    }
</style>
