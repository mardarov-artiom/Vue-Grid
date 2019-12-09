<template>
  <div :class="gridClasses">
    <slot />
  </div>
</template>

<script>
/* just to make sure container prop is provided */
const trueStatement = (...args) => {
  const falseArray = [];
  args.map(el => {
    if (el === undefined || el === null || el === false) {
      return falseArray.push(el);
    }
    return true;
  });

  return falseArray.length > 0 ? false : true;
};

/* defined available sizes for grid, to add another, also need to add it in scss */
const SIZE_TYPES = {
  xs: 'xs',
  sm: 'sm',
  md: 'md',
  lg: 'lg'
};

export default {
  name: 'Grid',
  props: {
    xs: String,
    sm: String,
    md: String,
    lg: String,
    spacing: String,
    container: String
  },
  computed: {
    gridClasses() {
      let sizesObject = {};
      Object.keys(SIZE_TYPES).map(size => {
        const field = `${SIZE_TYPES[size]}-${this[SIZE_TYPES[size]]}`;

        if (this[SIZE_TYPES[size]]) {
          sizesObject = {
            ...sizesObject,
            [field]: field
          };
        }
      });

      let spacing = {};

      if (trueStatement(this.container, this.spacing)) {
        spacing = {
          [`spacing-${this.spacing}`]: `spacing-${this.spacing}`
        };
      }

      return {
        container: trueStatement(this.container),
        ...spacing,
        ...sizesObject
      };
    }
  }
};
</script>

<style lang="scss">
$screenSizes: (
  xs: 360,
  sm: 768,
  md: 1024,
  lg: 1366
);

/* multiplying default grid values */
$spacing: 8;

@each $key, $size in $screenSizes {
  @for $i from 1 through 12 {
    @media (min-width: #{$size}px) {
      .#{$key}-#{$i} {
        flex-grow: 0;
        max-width: 100%/12 * $i;
        flex-basis: 100%/12 * $i;
      }
    }
  }
}

@for $i from 1 through 12 {
  .#{spacing}-#{$i} {
    width: calc(100% + #{$spacing * ($i * 2) + px});
    margin: -($spacing * $i) + px;
    > div {
      padding: #{$spacing * $i}px;
    }
  }
}

.container {
  display: flex;
  flex-wrap: wrap;
  flex-wrap: wrap;
  box-sizing: border-box;

  div {
    box-sizing: border-box;
  }
}
</style>
