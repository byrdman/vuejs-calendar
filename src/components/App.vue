<template>
    <div>{{msg}}</div>
</template>
<script>
    export default {
      data() {
        return {
          msg: 'Hello world'
        };
      },
      created() {
        console.log(this.$moment);
      }
    }
</script>