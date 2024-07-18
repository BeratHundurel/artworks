<script lang="ts">
   import { onMount } from "svelte";
   import { gsap } from "gsap";
   import { ScrollTrigger } from "gsap/dist/ScrollTrigger";

   gsap.registerPlugin(ScrollTrigger);

   let textContainer: HTMLParagraphElement;
   let image: HTMLDivElement;
   let image2: HTMLDivElement;
   let image3: HTMLDivElement;
   let image4: HTMLDivElement;
   onMount(() => {
      const textElement = textContainer.querySelector("p");

      if (textElement) {
         gsap.to(textElement, {
            x: () => -(textElement.scrollWidth - textContainer.clientWidth),
            ease: "none",
            scrollTrigger: {
               trigger: textContainer,
               start: "top top",
               end: () => `+=${textElement.scrollWidth}`,
               scrub: 1,
               pin: true,
            },
         });
      }

      gsap.to(image, {
         scrollTrigger: {
            trigger: image,
            start: "+=100", 
            end: "+=4000",
            scrub: 1,
            markers: true, 
         },
         x: 450,
         y: -5,
      });

      gsap.to(image2, {
         scrollTrigger: {
            trigger: image2,
            start: "+=100",
            end: "+=4000",
            scrub: 1,
            markers: true,
         },
         x: 250,
         y: 90,
      });

      gsap.to(image3, {
         scrollTrigger: {
            trigger: image3,
            start: "+=100",
            end: "+=4000",
            scrub: 1,
            markers: true,
         },
         x: -225,
         y: -45,
      });

      gsap.to(image4, {
         scrollTrigger: {
            trigger: image4,
            start: "+=100", 
            end: "+=4000",
            scrub: 1,
            markers: true,
         },
         x: -225,
         y: 175,
      });
   });
</script>

<div class="relative max-w-[88rem] mx-auto">
   <div class="flex items-center w-full h-[90svh] justify-start overflow-hidden whitespace-nowrap flex-nowrap list-none" bind:this={textContainer}>
      <p class="text-slate-100 text-8xl text inline-block">
         Explore Art Around the world, Beautiful Artifacts, Memory to Remember Learn, Know and See History...
      </p>
      <div class="absolute bottom-10 right-[55%] -z-10" bind:this={image}>
         <img src="/image1.png" alt="art-img" class="w-[300px]" />
      </div>
      <div class="absolute bottom-32 right-[40%] -z-20">
         <img src="/image4.png" alt="art-img" class="w-[300px] h-[400px]" bind:this={image2} />
      </div>
      <div class="absolute bottom-10 right-[22.5%] -z-10">
         <img src="/image2.png" alt="art-img" class="w-[350px] h-[450px]" />
      </div>
      <div class="absolute bottom-0 right-[7.5%] -z-20">
         <img src="/image3.png" alt="art-img" class="w-[250px] h-[300px]" bind:this={image3} />
      </div>
      <div class="absolute top-1 right-[7.5%] -z-20">
         <img src="/image5.png" alt="art-img" class="w-[300px] h-[300px]" bind:this={image4} />
      </div>
   </div>
</div>
