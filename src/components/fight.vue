<template>
  <div>
    <button @click="randomStart()" style="--content: 'START'; ">
      <div class="left"></div>START
      <div class="right"></div>
    </button>
    <template v-if="this.i != false ">
      <div class="row">
        <div class="col">
          <button
            @click="randomDamageAttack()"
            class="btn btn-primary btn-lg mb-4"
            tabindex="-1"
            role="button"
            aria-disabled="true"
          >Attack</button>
          <!-- ต้อง Random ถึง 150 ถึงจะกดปุ่ม Special Attack ได้ -->
          <template v-if="this.chart >= 100">
            <button class="btn btn-danger btn-lg mb-4 ml-3" @click="randomDamageSP()">Special Attack</button>
          </template>
          <template v-else-if="this.chart <= 100">
            <button class="btn btn-secondary btn-lg disabled mb-4 ml-3">Special Attack</button>
          </template>
        </div>
      </div>
      <div class="container-fluid">
        <div class="row">
          <div class="col">
            <div class="alert alert-primary" role="alert">
              Hero : {{randomPlayer}} | HP : {{hp1}}
              <div class="progress" style="height: 20px;">
                <div
                  id="HealthPID"
                  class="progress-bar progress-bar-striped bg-info"
                  style="width:100%"
                ></div>
              </div>
              <div class="progress" style="height: 5px;">
                <div
                  id="ChartID"
                  class="progress-bar progress-bar-striped bg-danger"
                  style="width:0%"
                ></div>
              </div>
            </div>
            <div class="heroMon">
              <img v-bind:style="{width: hp1 + 280 + 'px'}" :src="image1" />
            </div>
          </div>
          <div class="col">
            <div class="alert alert-danger" role="alert">
              Hero : {{randomMonster}} | HP : {{hp2}}
              <div class="progress" style="height: 25px;">
                <div
                  id="HealthMID"
                  class="progress-bar progress-bar-striped bg-info"
                  style="width:100%"
                ></div>
              </div>
            </div>
            <div class="heroMon">
              <img v-bind:style="{width: hp2 + 230 + 'px'}" :src="image2" />
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
      i: false,
      chart: 0,
      HealthP: 100,
      HealthM: 100,

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
          hp: 100,
          image: "./assets/img/p1.png",
          imageAv: "./assets/img/p1av.png", // ร่างอวตาร
        },
        {
          name: "Eevee",
          hp: 100,
          image: "./assets/img/p2.png",
          imageAv: "./assets/img/p2av.png", // ร่างอวตาร
        },
        {
          name: "Porygon",
          hp: 100,
          image: "./assets/img/p3.png",
          imageAv: "./assets/img/p3av.png", // ร่างอวตาร
        },
        {
          name: "Yanma",
          hp: 100,
          image: "./assets/img/p4.png",
          imageAv: "./assets/img/p4av.png", // ร่างอวตาร
        },
      ],
      randomPlayer: "",
      monster: [
        {
          name: "Misdreavus",
          hp: 100,
          image: "./assets/img/m1.png",
        },
        {
          name: "Murkrow",
          hp: 100,
          image: "./assets/img/m2.png",
        },
        {
          name: "Mewtwo",
          hp: 100,
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
      // randomBody
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
      this.i = true;
      this.chart = 0;
      document
        .getElementById("ChartID") //ChartAttack
        .setAttribute("style", "width:" + this.chart + "%");
      this.HealthP = 100;
      document
        .getElementById("HealthPID") //ChartHealthPayer
        .setAttribute("style", "width:" + this.HealthP + "%");
      this.HealthM = 100;
      document
        .getElementById("HealthMID") //ChartHealthMonster
        .setAttribute("style", "width:" + this.HealthM + "%");
    },

    randomDamage: function (min, max) {
      // randomReturn
      return Math.max(Math.floor(Math.random() * max) + 1, min);
    },

    randomDamageAttack: function () {
      // randomrandomDamageAttack
      var x = this.randomDamage(3, 10);
      var y = this.randomDamage(5, 15);
      console.log("x= " + x);
      console.log("x= " + y);
      // Attack return
      if (this.hp1 != 0 && this.hp2 != 0) {
        this.hp2 -= x;
        this.hp1 -= y;
        this.total += x;
        this.HealthP = this.hp1;
        document
          .getElementById("HealthPID")
          .setAttribute("style", "width:" + this.HealthP + "%");

        this.HealthM = this.hp2;
        document
          .getElementById("HealthMID")
          .setAttribute("style", "width:" + this.HealthM + "%");

        this.chart = this.total += 15;
        console.log("chart = " + this.chart);
        document
          .getElementById("ChartID")
          .setAttribute("style", "width:" + this.chart + "%");
      }
      // Must <-- attack more than 150 Create a new body
      if (this.chart >= 100) {
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

    randomDamageSP: function () {
      // randomrandomrandomDamageSP
      var sp = this.randomDamage(10, 20);
      // Must <-- attack more than 150  DamageSuperAttack
      if (this.chart >= 100) {
        this.hp2 -= sp;
        this.total = 0;
        this.image1 = this.afteravatar;
        this.HealthM = this.hp2;
        document
          .getElementById("HealthMID")
          .setAttribute("style", "width:" + this.HealthM + "%");
        this.chart = 0;
        document
          .getElementById("ChartID") //ChartAttack
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
  padding: 6em;
}
.pdCHart {
  padding: 2em;
}
</style>