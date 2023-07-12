<template>
  <div class="container">
    <h1>calcul frais de transport</h1>
    <div>
      <label for="">distance</label>
      <input type="number" v-model="distance" />
      <span>KM</span>
    </div>
    <div>
      <label for="">poids</label>
      <input type="number" v-model="poid" />
      <span>KG</span>
    </div>
    <div>
      <label for="">Mode de transport</label>
      <input type="radio" name="p" value="express" v-model="mode" /><span
        >Express</span
      >
      <input type="radio" name="p" value="normal" v-model="mode" /><span
        >Normal</span
      >
    </div>
    <div>
      <button @click="calcprice">calculer</button>
    </div>
    <div>
      <span>totla</span>
      <input type="text" :value="total" disabled />
      <span>DH</span>
    </div>
    <div v-if="error" class="error">error</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      distance: 0,
      poid: 0,
      mode: "",
      total: 0,
      error: false,
    };
  },
  methods: {
    calcprice() {
      if (this.distance <= 0 || this.poid <= 0 || this.mode == "") {
        this.error = true;
      } else {
        if (this.mode == "normal") {
          if (this.poid < 10) {
            this.total = this.distance * 0.5;
          } else {
            this.total = this.distance * (this.poid / 10) * 0.3;
          }
        } else {
          if (this.poid < 10) {
            this.total = this.distance * 0.5 + this.distance * 0.5 * 0.02;
          } else {
            this.total =
              this.distance * (this.poid / 10) * 0.3 +
              this.distance * (this.poid / 10) * 0.3 * 0.02;
          }
        }
        this.total = this.total.toFixed(2);
        this.error = false;
      }
    },
  },
};
</script>

<style>
.container {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: center;
}

.container div {
  margin-bottom: 10px;
}

.container label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
}

.container input[type="number"],
.container input[type="text"] {
  width: 100px;
  padding: 5px;
  border: 1px solid #ccc;
}

.container span {
  margin-left: 5px;
}

.container button {
  padding: 10px 20px;
  background-color: #4caf50;
  color: white;
  border: none;
  cursor: pointer;
}

.container input[type="radio"] {
  margin-right: 5px;
}

.container div.error {
  color: red;
}
</style>
