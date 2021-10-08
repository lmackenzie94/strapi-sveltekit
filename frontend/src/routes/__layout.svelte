<script lang="ts">
  import '../app.css';
  import userStore from '$lib/user';
  import type { User } from '$lib/types';
  import { onMount } from 'svelte';

  let loading = true;

  // Why use onMount instead of load
  // Since load is executed on the server, we won't have access to localStorage, which is on the browser. 
  // Hence, we have to wait for the app to load before accessing localStorage.
  onMount(async () => {
    // Check if 'token' exists in localStorage
    if (!localStorage.getItem('token')) {
      loading = false;
      return { props: { user: null } };
    }

    // Fetch the user from strapi
    const res = await fetch('http://localhost:1337/auth/me', {
        headers: { Authorization: `Bearer ${localStorage.getItem('token')}` }
    });
    const user: User = await res.json();
    loading = false;
    if (res.ok) {
        $userStore = user;
    }
  });
</script>

{#if !loading}
    <slot />
{/if}