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
   let imageMain: HTMLDivElement;
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
            start: "+=75",
            end: "+=4250",
            scrub: 1,
            markers: true,
         },
         x: 450,
         y: -5,
         onComplete: () => {
            gsap.set(image, { opacity: 0 }); // This will hide the image by setting its opacity to 0
         },
      });

      gsap.to(image2, {
         scrollTrigger: {
            trigger: image2,
            start: "+=75",
            end: "+=4250",
            scrub: 1,
            markers: true,
         },
         x: 250,
         y: 85,
         onComplete: () => {
            gsap.set(image2, { opacity: 0 }); // This will hide the image by setting its opacity to 0
         },
      });

      gsap.to(image3, {
         scrollTrigger: {
            trigger: image3,
            start: "+=75",
            end: "+=4250",
            scrub: 1,
            markers: true,
         },
         x: -225,
         y: -45,
         onComplete: () => {
            gsap.set(image3, { opacity: 0 }); // This will hide the image by setting its opacity to 0
         },
      });

      gsap.to(image4, {
         scrollTrigger: {
            trigger: image4,
            start: "+=75",
            end: "+=4250",
            scrub: 1,
            markers: true,
         },
         x: -250,
         y: 225,
         onComplete: () => {
            gsap.to(imageMain, {
               rotate: 30,
               duration: 2.5,
               y: -50,
               x: -300,
               ease: "bounce.inOut",
            });
            gsap.set(image4, { opacity: 0 }); // This will hide the image by setting its opacity to 0
         },
      });

      gsap.to("progress", {
         value: 100,
         ease: "sine.inOut",
         scrollTrigger: {
            trigger: "#page",
            scrub: 0.5,
         },
      });
   });
</script>

<div class="relative max-w-[88rem] mx-auto" id="page">
   <div class="flex items-center w-full h-[95svh] justify-start overflow-hidden whitespace-nowrap flex-nowrap list-none" bind:this={textContainer}>
      <p class="text-slate-100 text-8xl text inline-block font-bold tracking-tighter">
         Explore Art Around the world, Beautiful Artifacts, Memory to Remember Learn, Know and See History..
      </p>
      <div class="absolute bottom-10 right-[55%] -z-10" bind:this={image}>
         <img src="/image1.png" alt="art-img" class="w-[300px] rounded-sm" />
      </div>
      <div class="absolute bottom-36 right-[42.5%] -z-20">
         <img src="/image4.png" alt="art-img" class="w-[300px] h-[400px] rounded-md" bind:this={image2} />
      </div>
      <div class="absolute bottom-10 right-[22.5%] -z-10">
         <img src="/image2.png" alt="art-img" class="w-[350px] h-[450px] rounded-md" bind:this={imageMain} />
      </div>
      <div class="absolute bottom-0 right-[7.5%] -z-20">
         <img src="/image3.png" alt="art-img" class="w-[250px] h-[300px] rounded-md" bind:this={image3} />
      </div>
      <div class="absolute top-1 right-[7.5%] -z-20">
         <img src="/image5.png" alt="art-img" class="w-[300px] h-[300px] rounded-md" bind:this={image4} />
      </div>
      <progress class="fixed bottom-2 right-0 z-50 appearance-none h-1 w-full bg-transparent" max="100" value="0"></progress>
      <progress class="fixed top-6 left-0 z-50 appearance-none h-1 w-full bg-transparent rotate-180" max="100" value="0"></progress>
   </div>
</div>
