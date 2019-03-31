<template>
  <div>
    <p class="digit">{{ hours | two_digits }} : {{ minutes | two_digits }} : {{ seconds | two_digits }}</p>
  </div>
</template>

<script>
  export default {
    created() {
      this.pollData()
    },
    data() {
      return {
        now: Math.trunc((new Date()).getTime() / 1000)
      }
    },
    methods: {
      pollData() {
        window.setInterval(() => {
          this.now = Math.trunc((new Date()).getTime() / 1000);
        }, 1000);
      }
    },
    computed: {
      seconds() {
        return (this.now) % 60;
      },
      minutes() {
        return Math.trunc((this.now) / 60) % 60;
      },
      hours() {
        return Math.trunc((this.now) / 60 / 60) % 24;
      }
    },
    filters: {
      two_digits: function (value) {
        if (value.toString().length <= 1) {
          return "0" + value.toString();
        }
        return value.toString();
      }
    },
    beforeDestroy() {
      clearInterval(this.now)
    }
  }
</script>

<style scoped>
  .digit {
    color: #ecf0f1;
    font-size: 200px;
    font-family: 'Poppins', sans-serif;
    text-align: center;
  }
</style>
