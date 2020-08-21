<template>
  <div>
    <button @click="randomStart()" class="btn btn-danger">Start</button>
    <div class="row">
      <div class="col-12">
        <button @click="randomDamage(0,50)" class="btn btn-info">Attack</button>
        <button @click="randomDamageSP(50,100)" class="btn btn-info">Special Attack</button>
      </div>
    </div>

    <div class="row">
      <div class="col-6">
        <p>{{randomPlayer}}</p>
        <p>HP : {{hp1}}</p>
        <img :src="image1" />
      </div>

      <div class="col-6">
        <p>{{randomMonster}}</p>
        <p>HP : {{hp2}}</p>
        <img :src="image2" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      randomAttack: "",
      randomSpAttack: "",
      image1: "",
      image2: "",
      hp1: 0,
      hp2: 0,

      player: [
        {
          name: "Batman",
          hp: 300,
          image: "./assets/img/batman.png",
        },
        {
          name: "Joker",
          hp: 200,
          image: "./assets/img/joker.png",
        },
        {
          name: "Superman",
          hp: 400,
          image: "./assets/img/superman.png",
        },
      ],
      randomPlayer: "",
      monster: [
        {
          name: "Hukl",
          hp: 350,
          image: "./assets/img/hulk.png",
        },
        {
          name: "Ironman",
          hp: 240,
          image: "./assets/img/ironman.png",
        },
        {
          name: "Sipderman",
          hp: 230,
          image: "./assets/img/sipderman.png",
        },
      ],
      randomMonster: "",
    };
  },

  props: {
    Label: String,
  },

  methods: {
    randomStart: function () {
      var chosenNumber1 = Math.floor(Math.random() * this.player.length);
      this.randomPlayer = this.player[chosenNumber1].name;
      this.hp1 = this.player[chosenNumber1].hp;
      this.image1 = this.player[chosenNumber1].image;

      var chosenNumber2 = Math.floor(Math.random() * this.monster.length);
      this.randomMonster = this.monster[chosenNumber2].name;
      this.hp2 = this.monster[chosenNumber2].hp;
      this.image2 = this.monster[chosenNumber2].image;
    },

    randomDamage: function (min, max) {
      this.randomAttack = Math.max(Math.floor(Math.random() * max) + 1, min);
      console.log(this.randomAttack);
      console.log(this.hp2);
      if (this.hp1 != 0 && this.hp2 != 0) {
        this.hp2 -= this.randomAttack;
      }
      if (this.hp2 != 0 && this.hp1 != 0) {
        this.hp1 -= this.randomAttack;
      }
      if (this.hp1 <= 0) {
        this.hp1 = 0;
        console.log("LOSE");
      }
      if (this.hp2 <= 0) {
        this.hp2 = 0;
        console.log("WIN");
      }
    },

    randomDamageSP: function (min, max) {
      this.randomAttack = Math.max(Math.floor(Math.random() * max) + 1, min);
      console.log(this.randomAttack);
      this.hp2 -= this.randomAttack;
      if (this.hp2 <= 0) {
        this.hp2 = 0;
      }
    },
  },
};
</script>

<style>
</style>