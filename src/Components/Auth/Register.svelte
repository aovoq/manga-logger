<script>
   import { supabase } from '../../lib/supabaseClient.js'
   import { Link, navigate } from 'svelte-routing'

   let username = ''
   let email = ''
   let password = ''
   let loading = false

   const handleRegister = async () => {
      try {
         loading = true
         const { error } = await supabase.auth.signUp({ email, password, }, {data: {username}})
         if (error) throw error
         await navigate('/dashboard')
      } catch (error) {
         console.error(error.message)
      } finally {
         loading = false
      }
   }
</script>

<div class="container">
   <Link to="/" class="back_link">
   <span class="material-icons-outlined back">
      arrow_back_ios_new
   </span>
   </Link>

   <div class="catch_box">
      <h1>Sign Up</h1>
      <h2>Create your Account! </h2>
   </div>
   <form class="wrapper" on:submit|preventDefault={handleRegister}>
      <div class="input-box">
         <label for="username">UserName</label>
         <input type="text" name="username" id="username" bind:value={username} required/>
      </div>
      <div class="input-box">
         <label for="email">Email</label>
         <input type="email" name="email" id="email" bind:value={email} autocomplete="off" required/>
      </div>
      <div class="input-box">
         <label for="password">Password</label>
         <input type="password" name="password" id="password" bind:value={password} required/>
      </div>
      <button class="button" type="submit" disabled={loading}>Sign Up</button>
   </form>
</div>

<style>
    .container {
        overflow: hidden;
        width: 100%;
        height: 100vh;
        font-size: 1.6rem;
        padding: 3rem 4rem;
        display: flex;
        flex-direction: column;
        justify-content: flex-end;
        gap: 8rem;
    }

    :global(.back_link) {
        flex: 1;
    }
    .back {
        color: #222;
    }

    h1 {
        font-size: 4rem;
    }

    h2 {
        font-size: 2.5rem;
    }

    .wrapper {
        height: 450px;
        gap: 6rem;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
    }

    .input-box:last-of-type {
        flex: 1;
    }

    .input-box label {
        display: block;
        color: #666;
        letter-spacing: 0.1rem;
        margin-bottom: 0.5rem;
    }

    .input-box input {
        padding: 0.5rem 0;
        font-size: 2rem;
        display: block;
        width: 100%;
        background-color: transparent;
        border: none;
        border-bottom: 2px solid #aaa;
    }

    .input-box input:focus-visible {
        outline: none;
        border: none;
        border-bottom: 2px solid #2D9AFF;
    }

    .button {
        position: relative;
        width: 100%;
        font-size: 1.6rem;
        text-transform: uppercase;
        letter-spacing: 0.1rem;
        color: #fff;
        border: none;
        padding: 1rem 2rem;
        border-radius: 6px;
        transition: .2s;
        background: transparent;
    }

    .button::before, .button::after {
        content: '';
        width: 100%;
        height: 100%;
        position: absolute;
        left: 0;
        top: 0;
        border-radius: 6px;
        transition: .2s;
    }

    .button::before {
        background: linear-gradient(90deg, hsla(209, 100%, 59%, 1), hsla(209, 100%, 75%, 1));
        z-index: -1;
    }

    .button::after {
        background: linear-gradient(90deg, #0678E1 0%, #5EA6E9 100%);
        z-index: -2;
    }

    .button:hover:before {
        opacity: 0;
    }
</style>
