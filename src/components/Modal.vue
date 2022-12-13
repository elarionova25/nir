<template>
  <transition name="modal-fade">
    <div class="modal-backdrop">
      <div class="modal">
        <header class="modal-header">
          <slot name="header" v-if="counter > 4 || counter < 4">
            Спасибо, что принимаете участие!
          </slot>
          <slot name="header" v-if="counter === 4">
            Спасибо, что принимаете хехехее!
          </slot>
          <button
            v-if="counter >= 4"
            type="button"
            class="btn-close"
            @click="close"
          >
            x
          </button>
        </header>
        <footer class="modal-footer">
          <button
            v-if="counter > 4 || counter < 4"
            type="button"
            class="btn-green"
            @click="more"
          >
            Продолжить
          </button>
          <button
            v-if="counter === 4"
            type="button"
            class="btn-green"
            @click="more"
          >
            Отправить
          </button>
        </footer>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: 'Modal',
  data() {
    return {
      counter: 0
    }
  },
  methods: {
    more() {
      if (this.counter === 4) {
        this.$emit('close');
      } else {
        this.counter++;
        this.$emit('continue')
      }
    },
    close() {
      this.$emit('close');
    }
  }
};
</script>

<style scoped>

</style>
