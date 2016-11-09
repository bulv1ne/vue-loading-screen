<template>
  <div class="main">
    <slot></slot>
    <transition name="component-fade">
      <div v-if="loading" class="loading">
        <div class="message">{{loadingText}}</div>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  props: {
    loadingText: {
      type: String,
      default: 'Loading...',
    },
  },
  data() {
    return {
      loading: false,
    };
  },
  methods: {
    load(promise) {
      this.loading = true;
      const loadingFalse = () => {
        this.loading = false;
      };
      promise.then(
        loadingFalse,
        loadingFalse,
      );
      return promise;
    },
  },
};
</script>

<style scoped>
.component-fade-enter-active, .component-fade-leave-active {
  transition: opacity .3s ease;
}
.component-fade-enter, .component-fade-leave-active {
  opacity: 0;
}

.main {
  position: relative;
  min-height: 50px;
}

.loading {
  position: absolute;
  z-index: 1001;
  top: 0;
  left: 0;
  background-color: rgba(230, 233, 236, 0.8);
  cursor: wait;
  height: 100%;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.loading .message {
  background-color: #f4f4f4;
  border-radius: 4px;
  box-shadow: 0 1px 8px rgba(0,0,0,.15);
  border: solid 1px #bbb;
  padding: 10px 20px;
}
</style>
