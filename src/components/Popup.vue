<template>
  <div
    ref="popup_wrapper"
    class="v-popup vigorous"
    :class="{ active: isInfoPopup }"
  >
    <div class="v-popup__header">
      <button
        class="modal__btn-close modal__close"
        @click="closePopup"
      ></button>
    </div>
    <div class="v-popup__content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: 'v-popup',

  props: {
    isInfoPopup: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {};
  },
  methods: {
    closePopup() {
      this.$emit('closePopup');
    },
  },
  mounted() {
    let vm = this;
    document.addEventListener('click', function (item) {
      if (item.target === vm.$refs['popup_wrapper']) {
        vm.closePopup();
      }
    });
  },
};
</script>

<style scoped>
.v-popup {
  position: absolute;
  top: 0px;
  right: 0px;
  z-index: 100;
  text-align: center;
  align-items: center;

  justify-content: center;
  flex-direction: column;
  background: rgba(38, 38, 38, 0.5);
  border-left: 1px solid #4d4d4d;
  backdrop-filter: blur(8px);
  border-top-right-radius: 12px;
  border-bottom-right-radius: 12px;
  transition: 0.6s all;
}
.vigorous {
  right: -289px;
  transition: right 0.5s;
}

.active {
  display: flex;
  right: 0px;
}
.v-popup__header,
.v-popup__footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.modal__btn-close {
  position: absolute;
  top: 8px;
  right: 14px;
  display: block;
  width: 24px;
  height: 24px;
  padding: 0;
}
.modal__close {
  background-image: url(../assets/close.svg);
  border-radius: 100%;
  background-size: 12px;
  background-position: center;
  background-repeat: no-repeat;
  cursor: pointer;
}
.v-popup__header span {
  padding-bottom: 10px;
  font-weight: 500;
  font-size: 19px;
  line-height: 23px;
  letter-spacing: 0.04em;
  text-transform: uppercase;
  color: #fff;
}
@media (max-width: 460px) {
  .v-popup {
    width: 351px;
  }
}
</style>
