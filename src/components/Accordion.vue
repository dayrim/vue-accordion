<template>
  <div class="accordion">
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: "accordion",
  data: function() {
    return {
      allowOpen: true
    };
  },
  mounted: function() {
    this.$on("itemShownChanged", value => {
      this.allowOpen = !value;
    });
  }
};
</script>

<style scoped lang="scss">
.accordion {
  box-shadow: 0px 0px 5px -5px rgba(0, 0, 0, 0.75);
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 0;
  text-align: left;
  width: 100%;
  margin: auto;
  border-radius: 5px;
  overflow: hidden;
}
.accordion > .accordion-item:not(:last-child)::after {
  content: "";
  position: absolute;
  bottom: 0;
  left: 0;
  height: 1px;
  z-index: 1;
  width: 100%;
  border-bottom: 1px solid rgba(#ffffff, 0.4);
}
</style>
