<script>
   import { supabase } from '../../lib/supabaseClient.js'
   import { user } from '../../lib/sessionStore.js'
   import Log from './Log.svelte'

   let comicLog = []
   const getComicLog = async () => {
      try {
         const { data, error } = await supabase
            .from('comic_log')
            .select('*')
            .eq('user_id', $user.id)
            .order('id', { ascending: true })

         if (data) {
            comicLog = data
         }

         if (error) throw error
      } catch (e) {
         console.error(e.message)
      }
   }

   const updateLog = async (log) => {
      try {
         const {data, error} = await supabase.from('comic_log')
            .update({title: log.title, desc: log.desc, number: log.number})
            .eq('id', log.id)
         if (error) throw error
         await getComicLog()
      } catch (error) {
         console.error(error)
      }
   }

   const deleteLog = async (log) => {
      try {
         const {data, error} = await supabase.from('comic_log')
            .delete()
            .eq('id', log.id)
         await getComicLog()
      } catch (error) {
         console.error(error)
      }
   }

</script>


<ul use:getComicLog>
   {#each comicLog as log}
      <Log {log} {updateLog} {deleteLog} />
   {/each}
</ul>

<style>
   ul {
       display: flex;
       flex-direction: column;
       gap: 1rem;
   }
</style>
