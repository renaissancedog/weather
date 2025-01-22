<script>
  import '../app.css';
  let { children } = $props();
</script>

<div class="min-h-screen bg-sky-200 font-sans text-black">
  {@render children()}
  <footer class="mt-4 text-center">
    <p>
      <a
        class="text-sky-600 underline"
        href="https://github.com/renaissancedog/weather"
        target="_blank">Star or fork</a
      >
      this repo.
    </p>
    <p class="mb-4 mt-2">Made with ❤️ by William, 2025</p>
  </footer>
</div>
