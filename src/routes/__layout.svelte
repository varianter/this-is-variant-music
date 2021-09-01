<script>
  import Blob from '$lib/blob.svelte';
</script>

<svelte:head>
  <style>
    @import '/node_modules/@variant/profile/lib/colors/index.module.css';
    @import '/node_modules/@variant/profile/lib/typography/index.module.css';
    @import '/src/styles.css';
  </style>
</svelte:head>

<div class="background">
  <Blob class="blob-1" size={512} />
</div>

<slot />

<style>
  .background {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: -1;
    background-color: var(--color-secondary1);
    overflow: hidden;
  }

  .background :global(.blob-1) {
    position: absolute;
    transform: translate(-50%, -25%);
    fill: var(--color-primary);
  }
</style>
