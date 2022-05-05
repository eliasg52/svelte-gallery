<script lang="ts">
  import { page } from '$app/stores';
  export let route: string;
</script>

<a
  class:active={$page.url.pathname === route}
  class="nav-link active"
  aria-current="page"
  href={route}><slot /></a
>
