<template>
  <transition name="modal-fade">
    <div class="modal-backdrop">
      <div class="modal">
        <header class="modal-header">
          <slot name="header" v-if="counter > 4 || counter < 4">
            Спасибо, что принимаете участие!
          </slot>
          <slot name="header" v-if="counter === 4">
            Спасибо, что принимаете участие!
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


        <footer class="modal-footer" v-if="counter > 4 || counter < 4">
          <b-button
            variant="primary"
            size="sm"
            @click="more"
          >
            Продолжить
          </b-button>
        </footer>

        <footer class="modal-footer" v-if="counter === 4">
          <b-button
            variant="primary"
            size="sm"
            @click="more"
          >
            Отправить
          </b-button>
        </footer>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: 'Modal',
  props: {
    counter: {
      type: Number,
      default: 0
    }
  },
  methods: {
    more() {
      if (this.counter === 5) {
        this.$emit('close');
      } else {
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
