<template>
  <div class="wrapper">
    <main class="main">
      <section class="product">
        <div class="container">
          <div class="product__wrapper grid">
            <div class="product__item card">
              <div class="card__wrapper">
                <img class="card__img" src="../assets/img.png" alt="frame" />
                <div class="card__item-1"></div>
                <div class="card__item-2"></div>
                <div class="card__item-3"></div>
                <div class="card__item-4"></div>
                <div class="card__item-5"></div>
                <div class="card__item-6"></div>
                <div class="card__item-7"></div>
              </div>
            </div>
            <div class="product__item">
              <div class="field">
                <div
                  v-for="t in tickers"
                  :key="t.id"
                  @click="sel"
                  class="excel"
                >
                  {{ t.price }}
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
export default {
  name: 'MainPage',
  props: {
    msg: String,
  },
  data() {
    return {
      ticker: 'default',
      tickers: [
        { id: '1', price: '1' },
        { id: '2', price: '2' },
        { id: '3', price: '3' },
        { id: '4', price: '3' },
        { id: '5', price: '3' },
        { id: '6', price: '3' },
        { id: '7', price: '3' },
        { id: '8', price: '3' },
        { id: '9', price: '3' },
        { id: '10', price: '3' },
        { id: '11', price: '3' },
        { id: '12', price: '3' },
        { id: '13', price: '3' },
        { id: '14', price: '3' },
        { id: '15', price: '3' },
        { id: '16', price: '3' },
        { id: '17', price: '3' },
        { id: '18', price: '3' },
        { id: '19', price: '3' },
        { id: '20', price: '3' },
        { id: '21', price: '3' },
        { id: '22', price: '3' },
        { id: '23', price: '3' },
        { id: '24', price: '3' },
        { id: '25', price: '3' },
      ],
    };
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

.card__img {
  width: 208px;
  height: 240px;
  width: 100%;
  object-fit: cover;
  border-radius: 12px;
}

.card__item-1 {
  margin-bottom: 24px;
  margin-top: 20px;
  width: 190px;
  height: 26px;
  background: linear-gradient(90deg, #3c3c3c 0%, #444444 51.04%, #333333 100%);
  border-radius: 8px;
}
.card__item-2 {
  margin-bottom: 16px;
  width: 155px;
  height: 10px;
  background: linear-gradient(90deg, #3c3c3c 0%, #444444 51.04%, #333333 100%);
  border-radius: 4px;
}
.card__item-3 {
  margin-bottom: 16px;
  width: 190px;
  height: 10px;
  background: linear-gradient(90deg, #3c3c3c 0%, #444444 51.04%, #333333 100%);
  border-radius: 4px;
}
.card__item-4 {
  margin-bottom: 16px;
  width: 170px;
  height: 10px;
  background: linear-gradient(90deg, #3c3c3c 0%, #444444 51.04%, #333333 100%);
  border-radius: 4px;
}
.card__item-5 {
  margin-bottom: 16px;
  width: 160px;
  height: 10px;
  background: linear-gradient(90deg, #3c3c3c 0%, #444444 51.04%, #333333 100%);
  border-radius: 4px;
}
.card__item-6 {
  margin-bottom: 24px;
  width: 140px;
  height: 10px;
  background: linear-gradient(90deg, #3c3c3c 0%, #444444 51.04%, #333333 100%);
  border-radius: 4px;
}
.card__item-7 {
  width: 80px;
  height: 10px;
  background: linear-gradient(90deg, #3c3c3c 0%, #444444 51.04%, #333333 100%);
  border-radius: 4px;
}

.element {
  padding-left: 34px;
  padding-bottom: 20px;
  background: #1d1d1d;
}
.element__block {
  max-width: 699px;
  height: 36px;
  background: linear-gradient(90deg, #3c3c3c 0%, #444444 51.04%, #333333 100%);
  border-radius: 12px;
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
</style>

