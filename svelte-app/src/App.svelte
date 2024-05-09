<script>
  import { onMount } from "svelte";
  let offsetTop = 0;
  let opacity1 = 1;
  let opacity2 = 1;
  let y = 0;
  let header;
  let h;
  let poem = ["The trembling air, time", "sliding over our bodies like", "water. All the emptiness", "around us, as well as", "everything that remains."];
  let hedline = ["To", "Fall", "In Love", "With", "The", "World"];
  let deklin = ["A late summer meditation", "on time, loss, and solace in", "the natural world, made from", "the work of the photographer", "Mary Manning and the", "poet Brian Turner."];
  let flip1 = false;
  let flip2 = false;
  $: if (y) {
    offsetTop = ((header?.getBoundingClientRect().top / h) * 100).toFixed(2) + "%";
    flip2 = header?.getBoundingClientRect().bottom.toFixed(2) < h * 0.3 ? true : false;
    flip1 = header?.getBoundingClientRect().top.toFixed(2) < h ? true : false;

    opacity1 = 1 - y / h;
    opacity2 = 1 - ((y - h) / h) * 4;
  }
</script>

<svelte:window bind:scrollY={y} bind:innerHeight={h} />
<div class="background">
  <div class="left">
    <img src="/images/image-4.png" />
    <img class:flip={flip2} src="/images/image-1.png" />
  </div>
  <div class="right">
    <img src="/images/image-3.png" />
    <img class:flip={flip1} src="/images/image-2.png" />
  </div>
</div>
<div class="top">
  <div class="poem">
    <!-- <span>depth: {y}px {offsetTop} {h} {opacity1.toFixed(2)} {opacity2.toFixed(2)}</span> -->
    {#each poem as line, i}
      <p style="--fade-opacity: {opacity1}; --fadelater-opacity: {opacity2}" class="line-{i}" class:fadelater={i == 4}>{line}</p>
    {/each}
  </div>
  <div class="header" bind:this={header}>
    <h4>OPINION</h4>
    {#each hedline as hed}
      <h1>{hed}</h1>
    {/each}
    {#each deklin as dek}
      <h2>{dek}</h2>
    {/each}
  </div>
</div>
<div class="main"></div>

<style>
  .background {
    position: fixed;
    /* border: dashed black; */
    top: 0;
    height: 100vh;
    width: 100%;
    z-index: -1;
  }
  .left,
  .right {
    height: 100%;
    position: relative;
  }
  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    position: absolute;
    top: 0;
    left: 0;
    transition: opacity 500ms ease;
  }
  img.flip {
    opacity: 0;
    transition: opacity 500ms ease;
  }
  .background .right {
    display: none;
  }
  .poem {
    height: 100vh;
    width: 100%;
    position: fixed;
    /* border: solid red; */
    top: 0;
    display: flex;
    flex-direction: column;
    justify-content: center;
  }
  .poem p {
    font-family: "NYTCheltLight", serif;
    opacity: var(--fade-opacity);
    transition: opacity 100ms ease;
    width: calc(100% - 100px);
    margin: 0 auto;
    height: fit-content;
    color: white;
    font-size: 23px;
    line-height: 27.6px;
  }
  .poem p.fadelater {
    opacity: var(--fadelater-opacity);
  }
  .header {
    width: calc(100% - 100px);
    margin: 0 auto;
    margin-top: 200vh;
    margin-bottom: 100vh;
    /* padding-top: 100px; */
    /* border: solid green; */
  }
  h1 {
    font-weight: normal;
    mix-blend-mode: luminosity;
    color: rgba(234, 234, 234, 1);
    font-family: "NYTCondensed", serif;
    font-size: 4.8rem;
    text-transform: uppercase;
    letter-spacing: 10px;
    line-height: 1.3;
    margin: 0;
  }
  h2 {
    font-weight: normal;

    mix-blend-mode: luminosity;
    font-size: 23px;
    line-height: 27.6px;
    color: rgba(234, 234, 234, 1);
    font-family: "NYTCheltLight", serif;
    margin: 0;
  }
  h4 {
    font-family: "NYTCheltBold", serif;
    mix-blend-mode: luminosity;
    font-size: 18px;
    line-height: 27.6px;
    color: rgba(234, 234, 234, 1);
    margin: 0;
    letter-spacing: 1px;
  }
  .main {
    height: 1px;
    /* border: solid blue 1px; */
  }
  @media (min-width: 740px) {
    .background {
      display: flex;
    }
    .background .left {
      width: 50%;
    }
    .background .right {
      width: 50%;
      display: block;
    }
    .poem p,
    .header {
      width: calc(100% / 2 * 0.7);
      margin-left: calc(100% / 2 * 0.15);
    }
    .poem p {
      font-size: 30px;
      line-height: 34.6px;
    }
    h1 {
      font-size: 5.5rem;
      letter-spacing: 1.4rem;
      line-height: 1.3;
    }
    h2 {
      font-size: 30px;
      line-height: 34.6px;
    }
  }
</style>
