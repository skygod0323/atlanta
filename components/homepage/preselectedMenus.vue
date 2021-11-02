<template>
  <div class="choose-homepage">
    <h2>Select preferred menu type</h2>
    <div>
      <p class="bold-small">Each menu includes 5 meals</p>

      <div
        class="long-btn-wide"
        v-for="menu in this.$store.state.wizard.mealMenus"
        :key="menu.id"
        @click="selectMealMenu()"
      >
        <div class="text-wrapper">
          <b>{{ menu.meal_menu_name }}</b
          ><br />
          <span>{{ menu.description }}</span>
        </div>
        <img class="diet-img" src="~/assets/paleto_diet.png" alt="" />
      </div>

      <button
        @click="nextStep(1)"
        class="ms-button-wide ms-outlined-button meal-button ms-button–arrow ms-button-arrow-left"
      >
        Back
      </button>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    nextStep(step) {
      this.$store.commit('wizard/setStep', step)
    },
    selectMealMenu() {
      // call event with the view ID
      // push to /wizard
      this.$router.push({
        path: '/wizard?menu',
      })
    },
  },
}
</script>

<style scoped>
.ms-button-wide {
  margin-top: 24px;
  width: 484px;
}

.diet-img {
  position: absolute;
  top: 50%;
  right: 16px;
  transform: translateY(-50%);
  height: 20px;
}

.bold-small {
  font-family: Nunito;
  font-style: normal;
  font-weight: 800;
  font-size: 18px;
  line-height: 25px;
  letter-spacing: 0.2966px;
  color: #3c3c3c;
}

.long-btn-wide {
  width: 484px;
  padding-left: 16px;
  padding-right: 16px;
  padding-top: 12px;
  padding-bottom: 12px;
  background: #e0e9ef;
  border-radius: 8px;
  vertical-align: top;
  cursor: pointer;
  position: relative;
  transition: 250ms ease;
  margin-top: 12px;
}

.long-btn-wide:hover {
  background-color: #c1d4e0;
}

.long-btn-wide:last-child {
  margin-top: 16px;
}

.long-btn-wide:hover .right-arrow {
  right: 0px;
}

.right-arrow {
  position: absolute;
  top: 50%;
  right: -8px;
  transform: translate(-50%, -50%);
  transition: 250ms ease;
}

.long-btn-wide .text-wrapper {
  display: inline-block;
  width: 60%;
}

.long-btn-wide .text-wrapper span {
  font-size: 12px;
  display: block;
}

.text-wrapper {
  margin-left: 16px;
  vertical-align: middle;
}

.text-wrapper p {
  margin-bottom: 0px;
  margin-top: -4px;
}

.fruit-icon {
  padding: 18px;
  background: #ffffff;
  border-radius: 16px;
  width: max-content;
  height: 58px;
  display: inline-block;
  vertical-align: middle;
}

.fruit-icon svg {
  transform: translateY(-2px);
}

.choose-homepage {
  position: relative;
  /* top: 50%; */
  left: 10%;
  /* transform: translate(-50%, -50%); */
  width: 80%;
  max-width: 580px;
}

.choose-homepage h2 {
  font-family: Nunito;
  font-style: normal;
  font-weight: 800;
  font-size: 44px;
  line-height: 54px;
  color: #3c3c3c;
  margin-bottom: 0px;
}

@media only screen and (max-width: 1282px) {
  .choose-homepage h2 {
    font-size: 24px;
    line-height: 32px;
    margin-top: 0px;
    margin-bottom: 0px;
  }

  .ms-button-wide {
    width: 100%;
    display: none;
  }

  .long-btn-wide {
    width: 100%;
    padding: 12px;
  }

  .right-arrow {
    display: none;
  }

  .choose-homepage {
    position: relative;
    top: 0;
    left: 0;
    transform: none;
    width: calc(100% - 48px);
    display: block;
    margin-left: auto;
    margin-right: auto;
    margin-top: 35vh;
    z-index: 20;
  }

  .text-wrapper p:nth-child(2) {
    font-size: 12px;
    line-height: 16px;
  }

  .fruit-icon {
    vertical-align: middle;
    border-radius: 50%;
  }

  .text-wrapper {
    vertical-align: middle;
  }

  .diet-img {
    /* width: 40%; */
    height: 16px;
  }
}
</style>
