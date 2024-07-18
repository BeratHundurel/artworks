<script lang="ts">
   let open = false;

   function onLinkClick() {
      open = false;
   }
</script>

<header class="top-0 z-50 mx-auto max-w-7xl h-[10vh] sticky">
   <nav>
      <div class="flex flex-col justify-between px-4 py-2 md:flex-row md:items-center md:rounded-xl backdrop:blur-lg transition-all">
         <div class="flex items-center justify-between">
            <a href="/" aria-label="Homepage" class="text-xl font-extrabold tracking-tighter text-slate-100">Artworks</a>
            <button aria-expanded={open} aria-label="Open Menu" class="block p-2 text-2xl text-slate-100 md:hidden" on:click={() => (open = true)}>
               <i class="fa-solid fa-bars"></i>
            </button>
         </div>
         <a href="buy-ticket" class="border-2 border-slate-100 text-slate-100 py-2 px-10 font-medium">Explore</a>
      </div>
   </nav>
</header>
