<template>
  <div>
    <button @click="randomStart()" class="btn btn-danger">Start</button>
    <div class="row">
      <div class="col-12">
        <button @click="randomDamage(1,20)" class="btn btn-info">Attack</button>
        <button @click="randomDamageSP(40,70)" class="btn btn-info">Special Attack</button>
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
      total: 0,
      afteravatar: "",
      avatar: "",

      WinLose: [
        {
          image: "./assets/img/lose.png",
        },
        {
          image: "./assets/img/win.png",
        },
        {
          image: "./assets/img/try.png",
        },
      ],
      player: [
        {
          name: "Batman",
          hp: 300,
          image: "./assets/img/batman.png",
          imageAv: "./assets/img/spb.png", // ร่างอวตาร
        },
        {
          name: "Joker",
          hp: 200,
          image: "./assets/img/joker.png",
          imageAv: "./assets/img/spj.png", // ร่างอวตาร
        },
        {
          name: "Superman",
          hp: 400,
          image: "./assets/img/superman.png",
          imageAv: "./assets/img/spp.png", // ร่างอวตาร
        },
      ],
      randomPlayer: "",
      monster: [
        {
          name: "Hulk",
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
      this.avatar = this.player[chosenNumber1].imageAv;
      this.afteravatar = this.player[chosenNumber1].image;

      var chosenNumber2 = Math.floor(Math.random() * this.monster.length);
      this.randomMonster = this.monster[chosenNumber2].name;
      this.hp2 = this.monster[chosenNumber2].hp;
      this.image2 = this.monster[chosenNumber2].image;

      this.total = 0;
    },

    randomDamage: function (min, max) {
      this.randomAttack = Math.max(Math.floor(Math.random() * max) + 1, min);
      //console.log(this.randomAttack);
      console.log(this.total);
      // โจมตีไปกลับ
      if (this.hp1 != 0 && this.hp2 != 0) {
        this.hp2 -= this.randomAttack;
        this.total += this.randomAttack;
      }
      if (this.hp1 != 0 && this.hp2 != 0) {
        this.hp1 -= this.randomAttack;
      }
      // ถ้า โจมตีสะสมเท่ากับ 150 สร้างร่างอวตาร
      if (this.total >= 150) {
        this.image1 = this.avatar; // image ร่างอวตาร
      }
      // ชนะ,เสมอ,แพ้
      if (this.hp1 <= 1) {
        this.hp1 = 0;
        this.image1 = this.WinLose[0].image;
      }
      if (this.hp2 <= 1) {
        this.hp2 = 0;
        this.image2 = this.WinLose[1].image;
      }
      if (this.hp1 == 0 && this.hp2 == 0) {
        this.hp1 = 0;
        this.image1 = this.WinLose[2].image;
        this.image2 = this.WinLose[2].image;
      }
    },

    randomDamageSP: function (min, max) {
      this.randomAttack = Math.max(Math.floor(Math.random() * max) + 1, min);
      //console.log(this.randomAttack);
      //ถ้าจะ SuperAttack ต้องสะสมพลังมากกว่า 150 หน่วย
      if (this.total >= 150) {
        this.hp2 -= this.randomAttack;
        this.total = 0;
        this.image1 = this.afteravatar;
      }
      // ชนะ,เสมอ,แพ้
      if (this.hp1 <= 1) {
        this.hp1 = 0;
        this.image1 = this.WinLose[0].image;
      }
      if (this.hp2 <= 1) {
        this.hp2 = 0;
        this.image2 = this.WinLose[1].image;
      }
      if (this.hp1 == 0 && this.hp2 == 0) {
        this.hp1 = 0;
        this.image1 = this.WinLose[2].image;
        this.image2 = this.WinLose[2].image;
      }
    },
  },
};
</script>

<style>
</style>