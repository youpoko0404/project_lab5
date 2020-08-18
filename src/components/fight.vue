<template>
  <div>
    <button @click="randomA()" class="btn btn-warning">START {{ i }}</button>
    <button @click="randomDamage(10,100)" class="btn btn-warning">Random {{ randomNo }}</button>
  </div>
</template>
<script>
export default {
  data: function () {
    return {
      counter: 0,
      fsize: 50,
      randomNo: 0,
      i: null,
      player: [
        { name: "I", hp: 100, image: "" },
        { name: "D", hp: 100, image: "" },
        { name: "A", hp: 100, image: "" },
      ],
      Monster: [
        { name: "T", hp: 100, image: "" },
        { name: "C", hp: 100, image: "" },
        { name: "P", hp: 100, image: "" },
      ],
    };
  },
  props: {
    lable: String,
  },
  methods: {
    randomFI: function (min, max) {
      return Math.max(Math.floor(Math.random() * max) + 1, min);
    },
    randomA: function () {
      console.log("caLL FUNCTION RAN");
      var x=this.randomFI(0,2);
      console.log('x= '+x);
      this.i = this.player[x];
    },
     randomDamage: function (min, max) {
      this.randomNo =  Math.max(Math.floor(Math.random() * max) + 1, min);
    },
  },
};
</script>
<style>
</style>