<template>
  <div class="wrapper">
    <main class="main">
      <section class="product">
        <div class="container">
          <div class="product__wrapper grid">
            <div class="product__item card">
              <div class="card__wrapper">
                <img class="card__img" src="../assets/img.png" alt="frame" />
                <div class="card__item card__item-1"></div>
                <div class="card__item card__item-2"></div>
                <div class="card__item card__item-3"></div>
                <div class="card__item card__item-4"></div>
                <div class="card__item card__item-5"></div>
                <div class="card__item card__item-6"></div>
                <div class="card__item card__item-7"></div>
              </div>
            </div>
            <div class="product__item card-element">
              <v-popup
                @closePopup="closeInfoPopup"
                :isInfoPopup="isInfoPopupVisible"
              >
                <div>
                  <div class="popup__wrapper">
                    <div class="popup__color">
                      <div
                        class="popup__color-item color-1"
                        :class="`${isColorBlock}`"
                      ></div>
                      <div
                        class="popup__color-item blur-1"
                        :class="`${isColorBlockBlur}`"
                      ></div>
                    </div>
                    <div class="popup__item-wrap">
                      <div class="popup__item popup__item-1"></div>
                      <div class="popup__item popup__item-2"></div>
                      <div class="popup__item popup__item-3"></div>
                      <div class="popup__item popup__item-4"></div>
                      <div class="popup__item popup__item-5"></div>
                      <div class="popup__item popup__item-6"></div>
                    </div>

                    <button class="btn popup__button" @click="deleteItem">
                      Удалить предмет
                    </button>
                    <div
                      v-if="isInfoNumber"
                      class="popup__quantity"
                      :class="{ invalid: errors.name }"
                    >
                      <input
                        type="number"
                        id="number"
                        name="number"
                        maxlength="30"
                        class="form__input"
                        placeholder="Введите количество"
                        v-model.trim="name"
                      />
                      <small v-if="errors.name">{{ errors.name }}</small>
                      <div class="button__wrap">
                        <button
                          class="btn popup__cancellation"
                          @click="closeItem"
                        >
                          Отмена
                        </button>
                        <button
                          class="btn popup__button popup__button_red"
                          @click="submitHandler"
                        >
                          Подтвердить
                        </button>
                      </div>
                    </div>
                  </div>
                </div>
              </v-popup>
              <div class="field">
                <div
                  v-for="t in tickers"
                  :key="t.id"
                  @click="sel"
                  class="excel droptarget"
                  v-on:drop="drop"
                  v-on:dragover="allowDrop"
                >
                  <div
                    class="color-drag"
                    v-on:dragstart="dragStart"
                    draggable="true"
                    :id="`${t.id}`"
                  >
                    <div class="color-wrap">
                      <div
                        v-if="t.quantity"
                        class="color"
                        :class="`${t.color}`"
                      ></div>
                      <div
                        v-if="t.quantity > 1"
                        class="color"
                        :class="`${t.blur}`"
                        @click="showPopupInfo(t.id)"
                      ></div>
                    </div>
                    <div
                      v-if="t.quantity"
                      class="desired-count"
                      @click="showPopupNumber(t.id)"
                    >
                      {{ t.quantity }}
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="product__item element">
            <div class="element__wrapper">
              <button type="button" class="element__close"></button>
              <div class="element__block"></div>
            </div>
          </div>
        </div>
      </section>
    </main>
  </div>
</template>

<script>
import vPopup from './Popup.vue';

export default {
  name: 'MainPage',

  components: {
    vPopup,
  },
  data() {
    return {
      name: '',
      ticker: 'default',
      isInfoPopupVisible: false,
      isInfoNumber: false,
      tickers: [
        { id: '1', quantity: '4', color: 'color-1', blur: 'blur-1' },
        { id: '2', quantity: '2', color: 'color-2', blur: 'blur-2' },
        { id: '3', quantity: '5', color: 'color-3', blur: 'blur-3' },
        { id: '4', quantity: '' },
        { id: '5', quantity: '' },
        { id: '6', quantity: '' },
        { id: '7', quantity: '' },
        { id: '8', quantity: '' },
        { id: '9', quantity: '' },
        { id: '10', quantity: '' },
        { id: '11', quantity: '' },
        { id: '12', quantity: '' },
        { id: '13', quantity: '' },
        { id: '14', quantity: '' },
        { id: '15', quantity: '' },
        { id: '16', quantity: '' },
        { id: '17', quantity: '' },
        { id: '18', quantity: '' },
        { id: '19', quantity: '' },
        { id: '20', quantity: '' },
        { id: '21', quantity: '' },
        { id: '22', quantity: '' },
        { id: '23', quantity: '' },
        { id: '24', quantity: '' },
        { id: '25', quantity: '' },
      ],
      isColor: 0,
      isNumber: 0,
      isColorBlock: '',
      isColorBlockBlur: '',
      errors: {
        name: null,
      },
      count: '',
      testObject: '',
    };
  },
  methods: {
    showPopupInfo(colorId) {
      this.isInfoPopupVisible = true;
      this.isColor = parseInt(colorId) - 1;
      this.isColorBlock = this.tickers[parseInt(colorId) - 1].color;
      this.isColorBlockBlur = this.tickers[parseInt(colorId) - 1].blur;
    },
    showPopupNumber(colorId) {
      this.isColor = parseInt(colorId) - 1;
      this.isNumber = this.tickers[this.isColor].quantity;
      this.isInfoPopupVisible = true;
      this.isInfoNumber = true;
    },
    closeInfoPopup() {
      this.isInfoPopupVisible = false;
      this.isInfoNumber = false;
      this.name = '';
      this.errors.name = null;
    },
    deleteItem() {
      const item = { ...this.tickers };
      item[this.isColor].color = '';
      item[this.isColor].blur = '';
      item[this.isColor].quantity = '';
      this.tickers = item;
      localStorage.testObject = JSON.stringify(this.tickers);
    },
    closeItem() {
      this.name = '';
      this.errors.name = null;
    },
    formIsValid() {
      const res = this.name <= this.isNumber && this.name > 0;

      let isValid = true;
      if (!res) {
        this.errors.name = `Введите число <= ${this.isNumber}`;
        isValid = false;
      } else {
        this.errors.name = null;
      }
      return isValid;
    },
    submitHandler() {
      if (this.formIsValid()) {
        const item = { ...this.tickers };

        item[this.isColor].quantity = this.isNumber - parseInt(this.name);
        this.isNumber = item[this.isColor].quantity;
        this.tickers = item;
        this.name = '';
        localStorage.testObject = JSON.stringify(this.tickers);

        if (this.tickers[this.isColor].quantity == this.name) {
          const item = { ...this.tickers };
          item[this.isColor].color = '';
          item[this.isColor].blur = '';
          item[this.isColor].quantity = '';
          this.tickers = item;
          localStorage.testObject = JSON.stringify(this.tickers);
          this.name = '';
        }
      }
    },

    dragStart(event) {
      event.dataTransfer.setData('Text', event.target.id);
    },
    allowDrop(event) {
      event.preventDefault();
    },
    drop(event) {
      event.preventDefault();
      let data = event.dataTransfer.getData('Text');
      event.target.appendChild(document.getElementById(data));
      let idLastElementChild = event.target.lastElementChild.id - 1;
      let idFirstElementChild = event.target.firstElementChild.id - 1;
      const item = { ...this.tickers };
      let elemTextContent =
        event.target.lastElementChild.childNodes[1].textContent;
      item[idLastElementChild].color = '';
      item[idLastElementChild].blur = '';
      item[idLastElementChild].quantity = '';
      item[idFirstElementChild].color = 'color-2';
      item[idFirstElementChild].blur = 'blur-2';
      item[idFirstElementChild].quantity = elemTextContent;
      this.tickers = item;
      localStorage.testObject = JSON.stringify(this.tickers);
    },
  },
  mounted() {
    if (localStorage.testObject) {
      this.tickers = JSON.parse(localStorage.testObject);
    }
  },
};
</script>

<style scoped>
.main {
  padding-top: 66px;
  padding-bottom: 144px;
}
.product__wrapper {
  display: flex;
  justify-content: space-between;
}

.grid {
  padding: 32px 32px 23px 32px;
  height: 100%;
  display: grid;
  grid-gap: 20px;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr;
  grid-template-areas: 'one two';
  background: #1d1d1d;
}

.card-element {
  position: relative;
}
.field {
  width: 528px;
  height: 500px;
  margin: 0 auto;
  display: flex;
  flex-wrap: wrap;
  background: #262626;
  border: 1px solid #4d4d4d;
  border-radius: 12px;
  overflow: hidden;
}
.excel {
  width: 105px;
  height: 100px;
  padding: 5px;
  border: 1px solid #333;
  position: relative;
  display: flex;
  justify-content: center;
  text-align: center;
  align-items: center;
}
.desired-count {
  position: absolute;
  bottom: 0px;
  right: 0px;
  padding: 2px 5px 3px 4px;
  font-family: 'Inter';
  font-weight: 500;
  font-size: 10px;
  line-height: 12px;
  color: #ffffff;
  opacity: 0.4;
  border: 1px solid #4d4d4d;
  border-top-left-radius: 8px;
}

.color-wrap {
  position: relative;
}
.color {
  width: 48px;
  height: 48px;
  backdrop-filter: blur(6px);
}
.popup__color-item {
  width: 115.56px;
  height: 115.56px;
  backdrop-filter: blur(6px);
}
.color-1 {
  background: #7faa65;
  /* background: rgba(184, 217, 152, 0.35); */
}
.blur-1 {
  position: absolute;
  top: -7px;
  left: 8px;
  background: rgba(184, 217, 152, 0.35);
}
.blur-2 {
  position: absolute;
  top: -7px;
  left: 8px;
  background: rgba(217, 187, 152, 0.35);
}
.blur-3 {
  position: absolute;
  top: -7px;
  left: 8px;
  background: rgba(116, 129, 237, 0.35);
}
.color-2 {
  background: #aa9765;
}
.color-3 {
  background: #656caa;
}
.popup__color {
  position: relative;
  padding-bottom: 41px;
}
.popup__item-wrap {
  padding-top: 10px;
  padding-bottom: 10px;
  border-top: 1px solid #4d4d4d;
  border-bottom: 1px solid #4d4d4d;
  align-items: center;
  display: flex;
  justify-content: center;
  flex-direction: column;
  margin-bottom: 20px;
}
.card__wrapper {
  background-color: #262626;
  padding: 21px 23px;
  text-align: center;
  align-items: center;
  display: flex;
  justify-content: center;
  flex-direction: column;
  border: 1px solid #4d4d4d;
  border-radius: 12px;
}
.popup__wrapper {
  padding: 36px 23px;
  text-align: center;
  align-items: center;
  display: flex;
  justify-content: center;
  flex-direction: column;
}

.card__img {
  width: 208px;
  height: 240px;
  width: 100%;
  object-fit: cover;
  border-radius: 12px;
}
.card__item {
  background: linear-gradient(90deg, #3c3c3c 0%, #444444 51.04%, #333333 100%);
}
.card__item-1 {
  margin-bottom: 24px;
  margin-top: 20px;
  width: 190px;
  height: 26px;
  border-radius: 8px;
}
.card__item-2 {
  margin-bottom: 16px;
  width: 155px;
  height: 10px;
  border-radius: 4px;
}
.card__item-3 {
  margin-bottom: 16px;
  width: 190px;
  height: 10px;
  border-radius: 4px;
}
.card__item-4 {
  margin-bottom: 16px;
  width: 170px;
  height: 10px;
  border-radius: 4px;
}
.card__item-5 {
  margin-bottom: 16px;
  width: 160px;
  height: 10px;
  border-radius: 4px;
}
.card__item-6 {
  margin-bottom: 24px;
  width: 140px;
  height: 10px;
  border-radius: 4px;
}
.card__item-7 {
  width: 80px;
  height: 10px;
  border-radius: 4px;
}
.popup__item {
  background: linear-gradient(90deg, #3c3c3c 0%, #444444 51.04%, #333333 100%);
}
.popup__item-1 {
  margin-bottom: 24px;
  margin-top: 6px;
  width: 211px;
  height: 30px;
  border-radius: 8px;
}
.popup__item-2 {
  margin-bottom: 16px;
  width: 155px;
  height: 10px;
  border-radius: 4px;
}
.popup__item-3 {
  margin-bottom: 16px;
  width: 190px;
  height: 10px;
  border-radius: 4px;
}
.popup__item-4 {
  margin-bottom: 16px;
  width: 180px;
  height: 10px;
  border-radius: 4px;
}
.popup__item-5 {
  margin-bottom: 16px;
  width: 180px;
  height: 10px;
  border-radius: 4px;
}
.popup__item-6 {
  margin-bottom: 24px;
  width: 80px;
  height: 10px;
  border-radius: 4px;
  margin-bottom: 10px;
}

.element {
  padding-left: 34px;
  padding-bottom: 20px;
  background: #1d1d1d;
}
.element__block {
  max-width: 699px;
  height: 36px;
  border-radius: 12px;
  background: linear-gradient(90deg, #3c3c3c 0%, #444444 51.04%, #333333 100%);
}
.element__wrapper {
  padding: 18px 50px 18px 18px;
  background: #262626;
  border: 1px solid #4d4d4d;
  border-radius: 12px;
  position: relative;
}
.element__close {
  position: absolute;
  display: block;
  width: 12px;
  height: 12px;
  top: 15px;
  right: 15px;
  border: none;
  background-color: transparent;
  background-image: url('../assets/close.svg');
  background-repeat: no-repeat;
  background-position: center;
  background-size: contain;
}
.button__wrap {
  padding-top: 10px;
  display: flex;
  justify-content: space-between;
  text-align: center;
}
.btn {
  font-family: 'SF Pro Display';
  font-weight: 400;
  font-size: 14px;
  line-height: 17px;
}
.popup__button {
  padding: 12px 51px;
  overflow: hidden;
  border: 1px solid #333;
  color: #ffffff;
  background: #fa7272;
  border-radius: 8px;
}
.popup__button_red {
  padding: 12px 21px;
}
.popup__cancellation {
  padding: 12px 12px;
  overflow: hidden;
  border: 1px solid #333;
  color: #2d2d2d;
  color: #2d2d2d;
  background: #ffffff;
  border-radius: 8px;
}
.popup__button:hover {
  background: #7e3e3e;
}

.popup__quantity {
  padding: 20px;
  position: absolute;
  bottom: 0px;
  right: 0px;
  background: rgba(38, 38, 38, 0.7);
  backdrop-filter: blur(8px);
  width: 252px;
  height: 133px;
  border-top: 1px solid #4d4d4d;
}

.form__input {
  position: relative;
  padding: 5px 14px;
  background: transparent;
  border: 1px solid #c4c4c4;
  border: none;
  border-bottom: 1px solid #c4c4c4;
  font-family: 'Inter';
  font-style: normal;
  font-weight: 500;
  font-size: 14px;
  line-height: 17px;
  color: #ffffff;
  opacity: 0.4;
  width: 210px;
  height: 40px;
  background: #262626;
  border: 1px solid #4d4d4d;
  border-radius: 4px;
}
.popup__quantity small {
  display: block;
  color: red;
}
.popup__quantity.invalid input {
  border-color: red;
}
.color-drag {
}
</style>
