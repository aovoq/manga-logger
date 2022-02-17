<script>
   import { onMount } from 'svelte'
   import { navigate } from 'svelte-routing'
   import {user} from '../lib/sessionStore.js'

   onMount(() => {
      if ($user) {
         navigate('/dashboard')
      } else {
         navigate('/')
      }
   })
</script>

<div>404</div>
