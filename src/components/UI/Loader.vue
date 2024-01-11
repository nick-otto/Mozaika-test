<template>
  <div class="loader-wrapper" :data-variant="variant">

    <template v-if="variant === 'circle'">
      <svg version="1.1"
           xmlns="http://www.w3.org/2000/svg"
           xmlns:xlink="http://www.w3.org/1999/xlink"
           x="0px" y="0px"
           width="20px"
           height="20px"
           viewBox="0 0 50 50"
           style="enable-background:new 0 0 50 50;"
           xml:space="preserve"
      >
        <path fill="currentColor"
              d="M25.251,6.461c-10.318,0-18.683,8.365-18.683,18.683h4.068c0-8.071,6.543-14.615,14.615-14.615V6.461z"
        >
          <animateTransform
              attributeType="xml"
              attributeName="transform"
              type="rotate"
              from="0 25 25"
              to="360 25 25"
              dur="0.6s"
              repeatCount="indefinite"
          />
        </path>
    </svg>
    </template>

    <template v-else>
      <div class="loader">
        <span v-for="item in 10" :key="item" class="loader__item"></span>
      </div>
    </template>
  </div>
</template>

<script setup>
import {computed, ref} from 'vue'
const props = defineProps(['variant'])
const variant = computed(() => props.variant || 'simple')
</script>

<style lang="scss" scoped>
.loader-wrapper {
  color: #00B6D0;

  &[data-variant="simple"] {
    background-color: var(--color-text-heading-light);
  }
}

.loader {
  $loader-size: 4;
  $animation-duration: 2s;
  $animation-speed: 10;
  $animation-scale: 1.4;
  $loader-color: black;
  $loader-text-color: black;
  $loader-font-family: 'Arial';

  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  margin: auto;
  height: calc(4 * 10px);
  width: calc(4 * 20px);
  box-sizing: border-box;

  .loader__item {
    position: relative;
    float: left;
    height: calc(4 * 10px);
    width: calc(4 * 1px);
    margin: 0 calc(4/2)*1px;


    @for $i from 1 through 10 {
      &:nth-child(#{$i}) {
        animation: loader-item-#{$i} $animation-duration linear infinite;
      }
    }

  }

  &:after {
    content: 'Загрузка...';
    font-size: calc(4 * 4px);
    color: black;
    text-align: center;
    position: absolute;
    left: 0;
    right: 0;
    bottom: calc(4 * -8px);
    margin: auto;
  }

  @for $i from 0 through 9 {
    @keyframes loader-item-#{$i+1}{
      #{$i+1+$i*5 * 1%} {
        transform: scaleY(1);
      }
      #{$i+1+$i*5+$animation-speed * 1%} {
        transform: scaleY($animation-scale);
      }
      #{$i+1+$i*5+$animation-speed*2 * 1%} {
        transform: scaleY(1);
      }
      100% {
        transform: scaleY(1);
      }
    }
  }

}
</style>