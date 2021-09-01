<script lang="ts">
  import blobs2 from 'blobs/v2/index.js';
  import { onMount } from 'svelte';

  // import { canvasPath } from 'blobs/v2/animate';
  // import { onMount } from 'svelte';

  export let seed = Math.random();
  export let extraPoints = 8;
  export let randomness = 4;
  export let size = 256;
  let className: string;
  export { className as class };

  const lowerRadius = 25;
  const upperRadius = 75;

  // let path: SVGPathElement;
  let divBlob: HTMLDivElement;

  // const d = blobs2.svgPath({ seed, extraPoints, randomness, size });

  // let canvas: HTMLCanvasElement;

  // onMount(() => {
  //   const ctx = canvas.getContext('2d');

  //   const animation = canvasPath();
  //   ctx.fillStyle = 'magenta';

  //   const renderAnimation = () => {
  //     ctx.clearRect(0, 0, canvas.width, canvas.height);
  //     ctx.fill(animation.renderFrame());
  //     requestAnimationFrame(renderAnimation);
  //   };
  //   requestAnimationFrame(renderAnimation);

  //   const loopAnimation = () => {
  //     animation.transition({
  //       duration: 2000,
  //       timingFunction: 'ease',
  //       callback: loopAnimation,
  //       blobOptions: {
  //         extraPoints: 4,
  //         randomness: 9,
  //         seed: Math.random(),
  //         size: canvas.height
  //       }
  //     });
  //   };

  //   // Initial frame.
  //   animation.transition({
  //     duration: 0, // Render immediately.
  //     callback: loopAnimation,
  //     blobOptions: {
  //       extraPoints: 4,
  //       randomness: 9,
  //       seed: Math.random(),
  //       size: canvas.height
  //     }
  //   });
  // });

  const random = (min: number, max: number) => {
    return Math.floor(min + Math.random() * (max - min));
  };

  const remain = (n: number) => {
    return 100 - n;
  };

  const blob = () => {
    const r1 = random(lowerRadius, upperRadius);
    const r2 = random(lowerRadius, upperRadius);
    const r3 = random(lowerRadius, upperRadius);
    const r4 = random(lowerRadius, upperRadius);

    const r11 = remain(r1);
    const r22 = remain(r2);
    const r33 = remain(r3);
    const r44 = remain(r4);

    const radius = `${r1}% ${r11}% ${r22}% ${r2}% / ${r3}% ${r4}% ${r44}% ${r33}%`;

    divBlob.style.setProperty('--border-radius', radius);
  };

  onMount(() => {
    blob();
  });
</script>

<!-- <svg class={className} height={size} width={size}>
  <path bind:this={path} {d} />
</svg> -->

<div
  bind:this={divBlob}
  on:click={() => {
    console.log('clicked div');
    blob();
  }}
/>

<!-- <canvas bind:this={canvas} /> -->
<style>
  /* path {
    fill: var(--color-primary);
  } */

  /* canvas {
    height: 20rem;
    width: 20rem;
  } */

  div {
    z-index: 999;
    position: absolute;
    top: 5%;
    left: 5%;
    height: 20rem;
    width: 20rem;
    background: var(--color-primary);
    border-radius: var(--border-radius);

    transition-property: border-radius, transform;
    transition-duration: 1s;
  }
</style>
