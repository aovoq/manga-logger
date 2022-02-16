<script>
   import { supabase} from '../../supabaseClient'
   import {user} from '../../sessionStore'

   let comicLog = []
   const getComicLog = async () => {
      try {
         const { data, error } = await supabase
            .from('comic_log')
            .select('*')
            .eq('user_id', $user.id)
            .order('id', { ascending: false })

         console.log(data)
         if (data) {
            comicLog = data
         }

         if (error) throw error
      } catch (e) {
         console.error(e.message)
      }
   }

   const hoge = () => {
      console.log(comicLog)
   }
</script>

<button on:click={hoge}>hoge</button>
<ul use:getComicLog>
   {#each comicLog as log}
      <li>{log.title}</li>
      {:else}
      <p>Not Found</p>
      {/each}
</ul>
