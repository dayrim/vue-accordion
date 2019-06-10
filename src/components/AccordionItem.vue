<template>
  <div class="accordion-item">
    <div class="accordion-item-header" @click="toggleVisibility()">
      <slot name="header"></slot>
      <i class="arrow" :class="{ closed: isShown }"></i>
    </div>
    <transition @enter="enter" @leave="leave">
      <div v-if="slotPassed && isShown" class="accordion-item-content">
        <div class="padding">
          <slot></slot>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  name: "accordion-item",
  computed: {
    slotPassed() {
      return !!this.$slots.default;
    },
    allowOpen() {
      return !!this.$parent.allowOpen;
    }
  },
  data: function() {
    return {
      isShown: false
    };
  },
  watch: {
    isShown(value) {
      this.$parent.$emit("itemShownChanged", value);
    }
  },
  methods: {
    toggleVisibility() {
      if (!this.isShown && this.allowOpen) {
        this.isShown = true;
      } else if (this.isShown) {
        this.isShown = false;
      }
    },
    enter(element) {
      const { height } = getComputedStyle(element);

      element.style.height = 0;

      setTimeout(() => {
        element.style.height = height;
      });
    },

    leave(element) {
      const { height } = getComputedStyle(element);

      element.style.height = height;

      setTimeout(() => {
        element.style.height = 0;
      });
    }
  }
};
</script>

<style scoped lang="scss">
.accordion-item {
  position: relative;
  padding: 0;
  margin: 0;
  width: 100%;
  height: 100%;
  .accordion-item-header {
    position: relative;
    box-shadow: 0px 10px 50px -20px rgba(0, 0, 0, 0.5);
    cursor: pointer;
    padding: 10px;
    overflow: hidden;
    color: #ffffff;
    background-color: #402a5f;

    &:hover {
      background-color: rgba(#402a5f, 0.8);
    }
    .arrow {
      border: solid #fff;
      border-width: 0 4px 4px 0;
      display: block;
      padding: 7px;
      transform: translateY(-50%) rotate(-315deg);
      position: absolute;
      right: 20px;
      top: calc(50% - 5px);
      transition: transform 0.3s ease-out;
      &.closed {
        transform: rotate(-135deg);
      }
    }
  }
  .accordion-item-content {
    overflow: hidden;
    background-color: #ffffff;
    .padding {
      padding: 10px;
    }
    &.v-enter-active,
    &.v-leave-active {
      transition-duration: 0.3s;
      transition-property: height, opacity;
      transition-timing-function: ease-in-out;
    }
  }
}
</style>
