<template>
  <div>
    <section
      class="call-to-action"
      :style="{ backgroundImage: `url(${imgBackground})` }"
    >
      <div class="container narrow">
        <h2>Sign Up For Updates, Events, &amp; Recipes!</h2>
        <form
          action="https://atlantamealprep.us12.list-manage.com/subscribe/post?u=1df4740272423b3e25724441a&amp;id=be04ee5db3"
          method="post"
          id="mc-embedded-subscribe-form"
          name="mc-embedded-subscribe-form"
          class="validate"
          target="_blank"
          novalidate=""
        >
          <input
            type="email"
            value=""
            name="EMAIL"
            class="required email"
            id="mce-EMAIL"
            placeholder="Email Address"
          /><!-- real people should not fill this in and expect good things - do not remove this or risk form bot signups-->
          <div style="position: absolute; left: -5000px" aria-hidden="true">
            <input
              type="text"
              name="b_1df4740272423b3e25724441a_be04ee5db3"
              tabindex="-1"
              value=""
            />
          </div>
          <input
            type="submit"
            value="Sign me up!"
            name="subscribe"
            id="mc-embedded-subscribe"
            class="button solid"
          />
        </form>
      </div>
    </section>
  </div>
</template>

<script>
import backgroundImage from './../assets/sign_up_background.jpg'

export default {
  data() {
    return {
      imgBackground: backgroundImage,
    }
  },
}
</script>

<style scoped>
.container {
  background-color: transparent;
}

h2 {
  color: white;
  font-weight: bold;
}

input {
  border-radius: 10px;
  background-color: white;
}

@media only screen and (max-width: 765px) {
  .button {
    width: 65%;
  }
}

@media (max-width: 500px) {
  .button {
    width: 100%;
    margin-left: 0px !important;
  }
}
</style>