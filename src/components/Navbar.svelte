<script lang="ts">
  import ActiveClass from '../components/ActiveClass.svelte';
</script>

<nav class="navbar navbar-expand-lg navbar-dark bg-dark">
  <div class="container-fluid">
    <a class="navbar-brand" href="/">Gallery SK</a>
    <button
      class="navbar-toggler"
      type="button"
      data-bs-toggle="collapse"
      data-bs-target="#navbarNav"
      aria-controls="navbarNav"
      aria-expanded="false"
      aria-label="Toggle navigation"
    >
      <span class="navbar-toggler-icon" />
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav">
        <li class="nav-item">
          <ActiveClass route="/">Home</ActiveClass>
        </li>
        <li class="nav-item">
          <ActiveClass route="/search">Search</ActiveClass>
        </li>
      </ul>
    </div>
  </div>
</nav>
