<template>
  <component :is="type" :aria-label="ariaLabel" :class="['icon', size, rotate]" v-html="svg" />
</template>

<script>
const req = require.context("@/assets/icons/", true, /^\.\/.*\.svg$/)

/**
 * Icons are used to visually communicate core parts of the product and
 * available actions. They can act as wayfinding tools to help users more
 * easily understand where they are in the product.
 */
export default {
  name: "Icon",
  status: "review",
  release: "1.0.0",
  props: {
    /**
     * The name of the icon to display.
     */
    name: {
      required: true,
      default: "settings",
    },
    /**
     * The fill color of the SVG icon.
     */
    fill: {
      type: String,
      default: "currentColor",
    },
    /**
     * Descriptive text to be read to screenreaders.
     */
    ariaLabel: {
      type: String,
      default: "icon",
    },
    /**
     * The html element name used for the icon.
     */
    type: {
      type: String,
      default: "span",
    },
    /**
     * The size of the icon. Defaults to medium.
     * `small, medium, large`
     */
    size: {
      type: String,
      default: "medium",
      validator: value => {
        return value.match(/(small|medium|large)/)
      },
    },
    /**
     * The rotate of the icon. Defaults to right.
     * `normal, left, up, down`
     */
    rotate: {
      type: String,
      default: "normal",
      validator: value => {
        return value.match(/(normal|left|up|down)/)
      },
    },
  },
  data() {
    return {
      svg: req("./" + this.name + ".svg").replace(/^<svg /, `<svg style="fill: ${this.fill}" `),
    }
  },
}
</script>

<style lang="scss">
// This is here just to provide defaults if the original tokens are removed.
// Can be removed once you’re ready to start defining your own sizes.
@import "../../docs/docs.tokens.scss";

// We don’t want to use scoped since these styles need to cascade down to SVGs.
// We also want to be able to style .icon inside buttons etc.
.icon {
  @include reset;
  &.large svg {
    width: $space-l;
    height: $space-l;
  }
  &.medium svg {
    width: $space-m;
    height: $space-m;
  }
  &.small svg {
    width: $space-s;
    height: $space-s;
  }
  &.left svg {
    transform: rotate(180deg);
  }
  &.up svg {
    transform: rotate(-90deg);
  }
  &.down svg {
    transform: rotate(90deg);
  }
}
</style>

<docs>
  ```jsx
  <div>
    <Icon name="ready" aria-label="Component is ready" fill="#7cb518" />
    <Icon name="review" fill="rgb(255,186,10)" />
    <Icon name="deprecated" fill="rgb(235,59,36)" />
    <Icon name="prototype" fill="rgb(37,138,239)" />
    <Icon name="add" fill="rgb(37,138,239)" />
    <Icon name="angle" rotate="up" fill="rgb(37,138,239)" />
    <Icon name="angle" fill="#c1c1c1" />
    <Icon name="angle" rotate="left" fill="rgb(37,138,239)" />
    <Icon name="angle" rotate="down" fill="rgb(37,138,239)" />
    <Icon name="client" fill="rgb(37,138,239)" />
    <Icon name="dashboard" fill="rgb(37,138,239)" />
    <Icon name="close" fill="rgb(37,138,239)" />
    <Icon name="edit" fill="rgb(37,138,239)" />
    <Icon name="field" fill="rgb(37,138,239)" />
    <Icon name="info" fill="rgb(37,138,239)" />
    <Icon name="log" fill="rgb(37,138,239)" />
    <Icon name="out" fill="rgb(37,138,239)" />
    <Icon name="random" fill="rgb(37,138,239)" />
    <Icon name="search" fill="rgb(37,138,239)" />
    <Icon name="spinner" fill="rgb(37,138,239)" />
    <Icon name="view" fill="rgb(37,138,239)" />
    <Icon name="warning" fill="rgb(37,138,239)" />
  </div>
  ```
</docs>
