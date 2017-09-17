<template>
  <div>
    <header class="header">
      <h1 class="title">Tyler Smith:</h1>
      <h1 class="title">Full Stack</h1>
      <h1 class="title">Developer</h1>
    </header>
  </div>
</template>

<script>
export default {
  name: 'index'
}
</script>

<style scoped>
  .header {
    display: flex;

    width: 100vw;
    height: 15rem;

    padding: 0 2rem;

    flex-direction: column;
    justify-content: center;

    background-color: var(--bg-dark-color);
  }

  .title {
    /* TODO: Add Source Sans Pro as a static resource */
    font: 2.5rem 'Source Code Pro';
    letter-spacing: -0.05rem;

    color: var(--text-light-color);
  }

  /* TODO: add PostCSS Nested plugin */
  .title:last-of-type::after {
    content: '';
    display: inline-block;

    width: 1px;
    height: 1em;

    margin: 0.15em 0 0 0.1em;

    vertical-align: top;

    background-color: #AAA;

    animation: 1s step-end caret-blink infinite;
  }

  @keyframes caret-blink {
    0% {
      opacity: 1.0;
    }

    50% {
      opacity: 0.0;
    }

    100% {
      opacity: 1.0;
    }
  }
</style>
