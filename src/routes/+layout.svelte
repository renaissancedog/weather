<script>
  import '../app.css';
  let { children } = $props();
</script>

<div class="min-h-screen bg-sky-200 font-sans text-black">
  {@render children()}
</div>
