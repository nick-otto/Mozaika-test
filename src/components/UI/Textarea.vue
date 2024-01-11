<template>
  <div class="text-area-header">
    {{ header }}
  </div>

  <div class="text-area">

    <textarea
        class="text-area__field"
        placeholder=" "
        :name="name"
        :maxlength="maxlength"
        :value="modelValue"
        :style="modelValue?.length >= maxlength? 'background: var(--textarea-backgroung-error)' : ''"
        @change="checkLength($event.target.value)"
    />

    <Loader
        v-if="loaderStart"
        variant="circle"
        class="text-area__loader"
    />

    <label class="text-area__label">
      {{ name }}
    </label>

    <template v-if="maxlength && showCounter">
      <div class="text-area__bottom" :style="modelValue?.length >= maxlength? 'bottom: -80px' : ''">

        <div v-if="modelValue?.length >= maxlength" class="text-area__error__text">
          Ошибка
        </div>

        <div class="text-area__bottom__counter">
          {{ modelValue?.length || 0 }}/{{ maxlength }}
        </div>

        <button class="text-area__bottom__button" @click="cleanTextArea">
          Очистить
        </button>
      </div>
    </template>


  </div>
</template>

<script setup>
import {computed, ref} from 'vue'
import Loader from './Loader.vue'

const props = defineProps([
  'name',
  'maxlength',
  'showCounter',
  'header'
])

const name = computed(() => props.name)
const maxlength = computed(() => props.maxlength || 1000)
const showCounter = computed(() => !!props?.showCounter)

const modelValue = ref('')
const loaderStart = ref(false)
const cleanTextArea = () => {
  modelValue.value = ''
  loaderStart.value = true
  setTimeout(() => loaderStart.value = false, 500)
}

const checkLength = (value) => {
  modelValue.value = value
}

</script>

<style lang="scss" scoped>

.text-area-header {
  font-weight: 500;
  font-size: 18px;
  line-height: 24px;
  color: var(--textarea-header-text);
  margin-bottom: 4px;
}

.text-area {
  width: 326px;
  height: 146px;
  position: relative;
  font-family: Roboto, sans-serif;

  .text-area__field {
    border-radius: 8px;
    background: var(--textarea-backgroung);
    width: 100%;
    outline: none;
    transition: all 0.15s linear;
    min-height: 100px;
    height: inherit;
    padding: 4px 4px 4px 12px;
    font-weight: 400;
    font-family: inherit;
    font-size: 16px;
    line-height: 22px;
    resize: none;
    border: none;
  }

  .text-area__loader {
    position: absolute;
    top: 0;
    right: 0;
    padding: 7px;
  }

  .text-area__field:not(:placeholder-shown),
  .text-area__field:focus {
    padding: 20px 10px 5px;
  }

  .text-area__field:disabled ~ .text-area__label,
  .text-area__field:not(:placeholder-shown) ~ .text-area__label,
  .text-area__field:focus ~ .text-area__label {
    color: #A6B7D4;
    top: 5px;
    font-weight: 400;
    font-size: 12px;
    line-height: 22px;
  }

  .text-area__field:disabled ~ .text-area__label {
    color: #4F4F4F;
    top: 5px;
    font-weight: 400;
    font-size: 12px;
    line-height: 22px;
  }

  .text-area__label {
    font-weight: 400;
    font-size: 16px;
    line-height: 140%;
    display: block;
    position: absolute;
    left: 11px;
    top: 11px;
    transition: 0.2s;
    color: var(--textarea-label);
    z-index: 0;
  }

  .text-area__bottom {
    position: absolute;
    bottom: -50px;

    .text-area__bottom__counter {
      width: 50px;
      display: flex;
      align-items: center;
      justify-content: center;
      color: var(--textarea-counter);
    }

    .text-area__bottom__button {
      color: var(--textarea-button-text);
      cursor: pointer;
      padding: 0;
      border-color: transparent;
      background: none;
    }
  }

  .text-area__error__text {
    color: var(--textarea-error);
  }
}
</style>