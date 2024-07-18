<script>
   import Header from "$lib/components/Header.svelte";
</script>

<Header />

<main>
   <slot></slot>
</main>

<div class="absolute inset-0 pointer-events-none -z-40 h-full bg-[url('/Background.png')]"></div>
