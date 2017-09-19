<template>
  <div>
    <header class="header">
      <h1 class="title" v-bind:class="titleRow1.cursorClass">{{titleRow1.value}}</h1>
      <h1 class="title" v-bind:class="titleRow2.cursorClass">{{titleRow2.value}}</h1>
      <h1 class="title" v-bind:class="titleRow3.cursorClass">{{titleRow3.value}}</h1>
    </header>
  </div>
</template>

<script>
const CURSOR_CLASS = 'title-with-cursor';
const BLINKING_CURSOR_CLASS = 'title-with-blinking-cursor';

export default {
  name: 'index',

  data: function() {
    return {
      titleRow1: { value: '', cursorClass: CURSOR_CLASS },
      titleRow2: { value: '', cursorClass: '' },
      titleRow3: { value: '', cursorClass: '' }
    }
  },

  created: function() {
    const titleRowsToAnimate = [
      {
        rowKey: 'titleRow1',
        currentValue: '',
        finalValue: 'Tyler Smith:'
      },
      {
        rowKey: 'titleRow2',
        currentValue: '',
        finalValue: 'Full Stack'
      },
      {
        rowKey: 'titleRow3',
        currentValue: '',
        finalValue: 'Developer'
      }
    ];

    this.animateTitleRows(titleRowsToAnimate);
  },

  methods: {
    /* TODO: Look into Tween.js instead of this hacky solution */
    animateTitleRows: function(titleRowsToAnimate) {
      // slightly vary the time between "key strokes" to appear more realistic
      const timeoutMs = Math.floor(Math.random() * 150) + 50;

      setTimeout(() => {
        const currentTitleRow = titleRowsToAnimate[0];
        const nextCharIndex = currentTitleRow.currentValue.length;
        currentTitleRow.currentValue += currentTitleRow.finalValue[nextCharIndex];
        this[currentTitleRow.rowKey].value = currentTitleRow.currentValue;

          if (currentTitleRow.currentValue !== currentTitleRow.finalValue) {
            this.animateTitleRows(titleRowsToAnimate);
          } else if (titleRowsToAnimate.length > 1) {
            this[currentTitleRow.rowKey].cursorClass = '';
            titleRowsToAnimate.shift();
            this[titleRowsToAnimate[0].rowKey].cursorClass = CURSOR_CLASS;
            this.animateTitleRows(titleRowsToAnimate);
          } else {
            this[currentTitleRow.rowKey].cursorClass = BLINKING_CURSOR_CLASS;
          }
      }, timeoutMs);
    }
  }
};
</script>

<style scoped>
  .header {
    --border-width: 1px;

    display: flex;

    width: calc(100vw - (var(--border-width) * 2));
    height: 15rem;

    margin: var(--border-width) auto 0 auto;

    flex-direction: column;
    justify-content: center;

    background-color: var(--bg-dark-color);
    border: solid 0.5rem #CCC;
    box-shadow: 0 0 0 var(--border-width) black;
  }

  .title {
    margin: 0 2rem;

    /* TODO: Add Source Sans Pro as a static resource */
    font: 2.5rem 'Source Code Pro';
    letter-spacing: -0.05rem;

    color: var(--text-light-color);
  }

  .title::before {
    /* Forces the span to take it's line height up even when there is no content in it. */
    content: "\200b";
  }

  .title-with-cursor::after {
    content: '';
    display: inline-block;

    width: 1px;
    height: 1em;

    margin: 0.15em 0 0 0.1em;

    vertical-align: top;

    background-color: #AAA;
  }

  .title-with-blinking-cursor::after {
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
