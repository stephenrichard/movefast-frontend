<template>
  <div class="container">
    <h1>{{ msg }}</h1>

    <div class="grid grid-parent d-grid-4">
      <div
        class="grid__item col-span-2 d-row-span-2"
        :style="{ backgroundColor: colors[0] }"
        tabindex="0"
        @click="shuffleColors"
        @keyup.enter="shuffleColors"
      >
        1
      </div>
      <div
        class="grid__item col-span-2 m-order-3"
        :style="{ backgroundColor: colors[1] }"
        tabindex="0"
        @click="shuffleColors"
        @keyup.enter="shuffleColors"
      >
        2
      </div>
      <div
        class="grid__item d-col-start-3"
        :style="{ backgroundColor: colors[2] }"
        tabindex="0"
        @click="shuffleColors"
        @keyup.enter="shuffleColors"
      >
        3
      </div>
      <div
        class="grid__item d-col-start-4"
        :style="{ backgroundColor: colors[3] }"
        tabindex="0"
        @click="shuffleColors"
        @keyup.enter="shuffleColors"
      >
        4
      </div>
    </div>
    <div class="grid d-grid-3 grid-parent">
      <div
        class="grid__item order-1"
        :style="{ backgroundColor: colors[4] }"
        tabindex="0"
        @click="shuffleColors"
        @keyup.enter="shuffleColors"
      >
        5
      </div>
      <div
        class="grid__item order-3 d-row-span-2"
        :style="{ backgroundColor: colors[5] }"
        tabindex="0"
        @click="shuffleColors"
        @keyup.enter="shuffleColors"
      >
        6
      </div>
      <div
        class="
          grid__item
          order-2
          m-order-first
          col-span-2
          d-col-span-1 d-row-span-3
        "
        :style="{ backgroundColor: colors[6] }"
        tabindex="0"
        @click="shuffleColors"
        @keyup.enter="shuffleColors"
      >
        7
      </div>
      <div
        class="grid__item order-2 d-row-span-2"
        :style="{ backgroundColor: colors[7] }"
        tabindex="0"
        @click="shuffleColors"
        @keyup.enter="shuffleColors"
      >
        8
      </div>
      <div
        class="grid__item order-4"
        :style="{ backgroundColor: colors[8] }"
        tabindex="0"
        @click="shuffleColors"
        @keyup.enter="shuffleColors"
      >
        9
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Grid",
  props: {
    msg: String,
  },
  data() {
    return {
      colorIndex: 0,
      colors: [
        "#001219",
        "#005f73",
        "#0a9396",
        "#94d2bd",
        "#e9d8a6",
        "#ee9b00",
        "#ca6702",
        "#bb3e03",
        "#ae2012",
      ],
    };
  },
  methods: {
    shuffleColors() {
      this.colors = this.shuffle(this.colors);
    },
    shuffle(array) {
      let newArr = [...array];
      let currentIndex = newArr.length,
        randomIndex;

      while (currentIndex !== 0) {
        randomIndex = Math.floor(Math.random() * currentIndex);
        currentIndex--;

        [newArr[currentIndex], newArr[randomIndex]] = [
          newArr[randomIndex],
          newArr[currentIndex],
        ];
      }

      return newArr;
    },
  },
};
</script>

<style lang="scss" scoped>
h3 {
  margin: 40px 0 0;
}
.grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  column-gap: 16px;
  row-gap: 16px;

  &:not(:first-child) {
    margin-top: 16px;
  }

  &__item {
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 80px;
    color: #fff;
    font-weight: 700;

    @media screen and (min-width: 600px) {
      min-height: 100px;
    }
  }
}
.col-span-2 {
  grid-column: span 2 / span 2;
}

@for $i from 1 through 4 {
  .order-#{$i} {
    order: #{$i};
  }
}

@media screen and (max-width: 600px) {
  .m-order-3 {
    order: 3;
  }
  .m-order-first {
    order: -1;
  }
}

@media screen and (min-width: 600px) {
  .container {
    max-width: 1440px;
    padding: 0 24px;
    margin: 0 auto;
  }

  .d-grid-3 {
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: repeat(3, 1fr);
  }
  .d-grid-4 {
    grid-template-columns: repeat(4, 1fr);
  }

  .d-col-span-1 {
    grid-column: span 1 / span 1;
  }
  .d-row-span-2 {
    grid-row: span 2 / span 2;
  }
  .d-row-span-3 {
    grid-row: span 3 / span 3;
  }
  .d-col-start-3 {
    grid-column-start: 3;
  }
  .d-col-start-4 {
    grid-column-start: 4;
  }
}
</style>
