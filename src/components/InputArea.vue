<template>
  <div>
      <div v-if="validPassword">
          <p>Logged in!</p>
        </div>
      <div v-if="(tries < 3 && !validPassword)">
        <input 
            :class="{ disabled: tries > 2 }"
            :disabled="tries > 2"
            type="text" 
           
            v-on:change="updateTitle"
            @click="clear"
            placeholder="Enter the password!"
        />
      </div>
      <div v-if="(tries > 2 && !validPassword)">
          <h1>You failed. Try again?</h1>
          <button
            @click="reset"
          >
              Reset
        </button>
    </div>
  </div>
</template>

<script>
// Shuffles the characters
String.prototype.shuffle = function () {
    var a = this.split(""),
        n = a.length;

    for(var i = n - 1; i > 0; i--) {
        var j = Math.floor(Math.random() * (i + 1));
        var tmp = a[i];
        a[i] = a[j];
        a[j] = tmp;
    }
    return a.join("");
}

export default {
  name: 'InputArea',
  methods: {
      updateTitle(event) {
        event.target.value = event.target.value.shuffle()
        // Global emits! https://alligator.io/vuejs/global-event-bus/ 
        this.$emit('update-title', event.target.value); 
        this.tries += 1;
      },
      clear() {
        event.target.value = "";
      },
      reset() {
          this.tries = 0;
      }
  },
  props: {
    validPassword: Boolean,
  },
  data() {
      return {
        tries: 0,
      }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .disabled {
        color: red;
    }

</style>
