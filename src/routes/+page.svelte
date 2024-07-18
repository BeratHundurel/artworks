<script lang="ts">
   import { onMount } from "svelte";
   import { gsap } from "gsap";
   import { ScrollTrigger } from "gsap/dist/ScrollTrigger";

   gsap.registerPlugin(ScrollTrigger);

   let textContainer: HTMLParagraphElement;
   let image: HTMLImageElement;
   let image2: HTMLImageElement;
   let image3: HTMLImageElement;
   let image4: HTMLImageElement;
   let imageMain: HTMLImageElement;

   const animateImage = (img: HTMLImageElement, x: number, y: number, isLast: boolean) => {
      gsap.to(img, {
         scrollTrigger: {
            trigger: img,
            start: "+=75",
            end: "+=4250",
            scrub: 1,
         },
         x,
         y,
         onComplete: () => {
            if (isLast) {
               gsap.to(imageMain, {
                  rotate: 30,
                  duration: 2,
                  y: -50,
                  x: -300,
                  ease: "bounce.inOut",
               });

               [image, image2, image3, image4].forEach((img) => {
                  gsap.to(img, {
                     opacity: 0,
                     duration: 0,
                  });
               });
            }
         },
         onReverseComplete: () => {
            if (isLast) {
               gsap.to(imageMain, {
                  rotate: 0,
                  duration: 2,
                  y: 0,
                  x: 0,
                  ease: "bounce.inOut",
               });

               [image, image2, image3, image4].forEach((img) => {
                  gsap.to(img, {
                     opacity: 1,
                     duration: 3,
                     ease: "back.in",
                  });
               });
            }
         },
      });
   };

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

      animateImage(image, 450, -5, false);
      animateImage(image2, 250, 85, false);
      animateImage(image3, -225, -45, false);
      animateImage(image4, -250, 225, true);

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
      <div class="absolute bottom-10 right-[55%] -z-10">
         <img src="/image1.png" alt="art-img" class="w-[300px] rounded-sm" bind:this={image} />
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
