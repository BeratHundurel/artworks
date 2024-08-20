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

   const animateImage = (img: HTMLImageElement, x: number, y: number, isLast: boolean, end?: string, mainX?: number, mainY?: number) => {
      gsap.to(img, {
         scrollTrigger: {
            trigger: img,
            start: "+=75",
            end: end || "+=4250",
            scrub: 1,
         },
         x,
         y,
         onComplete: () => {
            if (isLast) {
               gsap.to(imageMain, {
                  rotate: 30,
                  duration: 2,
                  y: mainY || -50,
                  x: mainX || -300,
                  ease: "bounce.inOut",
               });

               [image, image2, image3, image4].forEach((img) => {
                  gsap.to(img, {
                     opacity: 0,
                     duration: 0,
                     ease: "back.in",
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
               anticipatePin: 1,
            },
         });
      }

      ScrollTrigger.matchMedia({
         "(min-width: 768px)": () => {
            console.log("desktop");
            animateImage(image, 450, -5, false);
            animateImage(image2, 250, 85, false);
            animateImage(image3, -225, -45, false);
            animateImage(image4, -250, 225, true);
         },
         "(max-width: 767px)": () => {
            animateImage(image, 150, -150, false);
            animateImage(image2, 100, 175, false);
            animateImage(image3, -125, -100, false);
            animateImage(image4, -80, 300, true, "+=2000", 20, -50);
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

<div class="relative max-w-[88rem] px-3 lg:px-0 mx-auto" id="page">
   <div
      class="flex items-center w-full lg:h-[95svh] h-[90svh] justify-start overflow-hidden whitespace-nowrap flex-nowrap list-none"
      bind:this={textContainer}
   >
      <p class="text-slate-100 lg:text-8xl text-5xl text inline-block font-bold tracking-tighter">
         Explore Art Around the world, Beautiful Artifacts, Memory to Remember Learn, Know and See History..
      </p>
      <div class="absolute lg:bottom-10 bottom-0 right-[55%] -z-10">
         <img src="/image1.png" alt="art-img" class="lg:w-[300px] w-60 rounded-sm" bind:this={image} />
      </div>
      <div class="absolute lg:bottom-36 bottom-52 right-[42.5%] -z-20">
         <img src="/image4.png" alt="art-img" class="lg:w-[300px] lg:h-[400px] w-52 h-64 rounded-md" bind:this={image2} />
      </div>
      <div class="absolute lg:bottom-10 bottom-14 right-[22.5%] -z-10">
         <img src="/image2.png" alt="art-img" class="lg:w-[350px] lg:h-[450px] w-56 h-72 rounded-md" bind:this={imageMain} />
      </div>
      <div class="absolute bottom-0 lg:right-[7.5%] right-[5%] -z-20">
         <img src="/image3.png" alt="art-img" class="lg:w-[250px] lg:h-[300px] w-44 h-52 rounded-md" bind:this={image3} />
      </div>
      <div class="absolute top-1 right-[7.5%] -z-20">
         <img src="/image5.png" alt="art-img" class="lg:w-[300px] lg:h-[300px] w-52 h-52 rounded-md" bind:this={image4} />
      </div>
      <progress class="fixed bottom-2 right-0 z-50 appearance-none h-1 w-full bg-transparent" max="100" value="0"></progress>
      <progress class="fixed top-6 left-0 z-50 appearance-none h-1 w-full bg-transparent rotate-180" max="100" value="0"></progress>
   </div>
</div>
