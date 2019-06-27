<template>
  <div class="home">
    <p v-if="!validPassword">Try to login. The password is "123"</p>
    <Message v-if="!validPassword" v-bind:validPassword="validPassword" v-bind:msg="password"/>
    <InputArea v-bind:validPassword="validPassword" v-on:update-title="updateTitle"/>
    <br/><br/>
    <FlipCountdown v-if="!validPassword" :deadline="time"></FlipCountdown>
    <img v-if="validPassword" src="https://media1.giphy.com/media/a6GhnspYLkSBy/giphy.gif?cid=790b76115d14a4e74d456b6b67b4344d&rid=giphy.gif"/>
  </div>
</template>

<script>
// @ is an alias to /src
import Message from '@/components/Message.vue'
import InputArea from '@/components/InputArea.vue'
import FlipCountdown from 'vue2-flip-countdown'

export default {
  name: 'home',
  components: {
    Message,
    FlipCountdown,
    InputArea
  },
  data() {
    return {
      password: "",
      validPassword: false,
      time: this.now()
    }
  },
  methods: {
    updateTitle(password) {
      if(password == "123") this.validPassword = true;
      else this.validPassword = false;

      this.password = password;
    },
    now() {
      var date = new Date();
      date.setUTCSeconds(date.getUTCSeconds() + 50000);
      var aaaa = date.getUTCFullYear();
      var gg = date.getUTCDate();
      var mm = (date.getUTCMonth() + 1);

      if (gg < 10)
          gg = "0" + gg;

      if (mm < 10)
          mm = "0" + mm;

      var cur_day = aaaa + "-" + mm + "-" + gg;

      var hours = date.getUTCHours()
      var minutes = date.getUTCMinutes()
      var seconds = date.getUTCSeconds();

      if (hours < 10)
          hours = "0" + hours;

      if (minutes < 10)
          minutes = "0" + minutes;

      if (seconds < 10)
          seconds = "0" + seconds;

      return cur_day + " " + hours + ":" + minutes + ":" + seconds;
    }
  }
}
</script>