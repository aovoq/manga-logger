<script>
   import { supabase } from '../../supabaseClient'
   import { user } from '../../sessionStore'

   let title, desc, number
   let loading = false
   const handleSubmit = async() => {
      try {
         loading = true
         const {error } = await supabase.from('comic_log')
            .insert([{title, desc, number, user_id: $user.id}])
         if (error) throw error
      } catch (e) {
         console.error(e.message)
      } finally {
         loading = false
      }

   }
</script>

<h1>Add</h1>
<form on:submit|preventDefault={handleSubmit}>
   <input type="text" name="title" bind:value={title}>
   <input type="text" name="desc" bind:value={desc}>
   <input type="number" name="text" bind:value={number}>
   <input type="submit" value="add" disabled={loading}>
</form>
