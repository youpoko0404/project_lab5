<template>
  <div>
    <button @click="randomStart()" style="--content: 'START'; ">
      <div class="left"></div>START
      <div class="right"></div>
    </button>
    <template v-if="this.i != 0 ">
      <div class="row">
        <div class="col">
          <button
            @click="randomDamage(1,20)"
            class="btn btn-primary btn-lg mb-4"
            tabindex="-1"
            role="button"
            aria-disabled="true"
          >Attack</button>
          <!-- ต้อง Random ถึง 150 ถึงจะกดปุ่ม Special Attack ได้ -->
          <template v-if="this.total >= 100">
            <button
              class="btn btn-danger btn-lg mb-4 ml-3"
              @click="randomDamageSP(40,70)"
            >Special Attack</button>
          </template>
          <template v-else-if="this.total <= 100">
            <button
              class="btn btn-secondary btn-lg disabled mb-4 ml-3"
              @click="randomDamageSP(40,70)"
            >Special Attack</button>
          </template>
        </div>
      </div>
      <div class="container-fluid">
        <div class="row">
          <div class="col">
            <div class="alert alert-primary" role="alert">Hero : {{randomPlayer}} | HP : {{hp1}}</div>
            <div class="heroMon">
              <div class="pdCHart">
                <div class="progress">
                  <div
                    id="ChartID"
                    class="progress-bar progress-bar-striped bg-danger"
                    style="width:0%"
                  ></div>
                </div>
              </div>
              <img :src="image1" class="img-fluid" />
            </div>
          </div>
          <div class="col">
            <div class="alert alert-danger" role="alert">Hero : {{randomMonster}} | HP : {{hp2}}</div>
            <div class="heroMon">
              <div class="pdCHart"></div>
              <img :src="image2" class="img-fluid" />
            </div>
          </div>
        </div>
      </div>
    </template>
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
      i: 0,
      chart: 0,

      WinLose: [
        {
          image: "./assets/img/ko.png",
        },
        {
          image: "./assets/img/try.png",
        },
      ],
      player: [
        {
          name: "Magneton",
          hp: 300,
          image: "./assets/img/p1.png",
          imageAv: "./assets/img/p1av.png", // ร่างอวตาร
        },
        {
          name: "Eevee",
          hp: 200,
          image: "./assets/img/p2.png",
          imageAv: "./assets/img/p2av.png", // ร่างอวตาร
        },
        {
          name: "Porygon",
          hp: 400,
          image: "./assets/img/p3.png",
          imageAv: "./assets/img/p3av.png", // ร่างอวตาร
        },
        {
          name: "Yanma",
          hp: 250,
          image: "./assets/img/p4.png",
          imageAv: "./assets/img/p4av.png", // ร่างอวตาร
        },
      ],
      randomPlayer: "",
      monster: [
        {
          name: "Misdreavus",
          hp: 350,
          image: "./assets/img/m1.png",
        },
        {
          name: "Murkrow",
          hp: 240,
          image: "./assets/img/m2.png",
        },
        {
          name: "Mewtwo",
          hp: 230,
          image: "./assets/img/m3.png",
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
      this.i = 1;
      this.chart = 0;
      document
        .getElementById("ChartID")
        .setAttribute("style", "width:" + this.chart + "%");
    },

    randomDamage: function (min, max) {
      this.randomAttack = Math.max(Math.floor(Math.random() * max) + 1, min);
      //console.log(this.randomAttack);
      console.log(this.total);
      // Attack return
      if (this.hp1 != 0 && this.hp2 != 0) {
        this.hp2 -= this.randomAttack;
        this.hp1 -= this.randomAttack;
        this.total += this.randomAttack;
        this.chart = this.chart + this.randomAttack;
        document
          .getElementById("ChartID")
          .setAttribute("style", "width:" + this.chart + "%");
      }
      // Must <-- attack more than 150 Create a new body
      if (this.total >= 100) {
        this.image1 = this.avatar; // image index[avatar <- [imageAv]]
      }
      // WIN,TIE,LOSE
      if (this.hp1 <= 1) {
        this.hp1 = 0;
        this.image1 = this.WinLose[0].image; // image index[0] WIN
      }
      if (this.hp2 <= 1) {
        this.hp2 = 0;
        this.image2 = this.WinLose[0].image; //image index[0] WIN
      }
      if (this.hp1 == 0 && this.hp2 == 0) {
        this.hp1 = 0;
        this.image1 = this.WinLose[1].image; //image index[0] KO
        this.image2 = this.WinLose[1].image; //image index[0] KO
      }
    },

    randomDamageSP: function (min, max) {
      this.randomAttack = Math.max(Math.floor(Math.random() * max) + 1, min);
      //console.log(this.randomAttack);
      // Must <-- attack more than 150  DamageSuperAttack
      if (this.total >= 100) {
        this.hp2 -= this.randomAttack;
        this.total = 0;
        this.image1 = this.afteravatar;
        this.chart = 0;
        document
          .getElementById("ChartID")
          .setAttribute("style", "width:" + this.chart + "%");
      }
      // ชนะ,เสมอ,แพ้
      if (this.hp1 <= 1) {
        this.hp1 = 0;
        this.image1 = this.WinLose[0].image;
      }
      if (this.hp2 <= 1) {
        this.hp2 = 0;
        this.image2 = this.WinLose[0].image;
      }
      if (this.hp1 == 0 && this.hp2 == 0) {
        this.hp1 = 0;
        this.image1 = this.WinLose[1].image;
        this.image2 = this.WinLose[1].image;
      }
    },
  },
};
</script>

<style>
.heroMon {
  padding: 4em;
}
.pdCHart {
  padding: 2em;
}
</style>