<script>
/* eslint-disable */
import axios from 'axios';

export default {
  data() {
    return {
      ownedSets: [],
      ownedCards: [],
      setCodes: {
        core: [
          '01096',
          '01096',
          '01097',
          '01097',
          '01098',
          '01099',
          '01100',
          '01101',
          '01102',
          '01103',
        ],
        dwl: ['02037', '02037', '02038', '02038', '02039', '02039'],
        ptc: ['03040', '03040', '03041', '03042'],
        tfa: ['04038', '04040'],
        tcu: ['05041', '05041', '05042', '05042'],
        tde: ['06035', '06036', '06037', '06038'],
        tic: ['07038', '07038', '07039', '07039', '07040'],
        eote: ['08130', '08131', '08132', '08133'],
        rtdwl: ['51011', '51011'],
        rtptc: ['52011', '52012', '52013'],
        rttfa: ['53012', '53013'],
        rttcu: ['54014', '54015', '54015'],
        nate: ['60104'],
        harvey: ['60204'],
        wini: ['60304'],
        jackie: ['60404'],
        stella: ['60504'],
      },
      weaknessImageUrl: null,
    };
  },

  methods: {
    async getRandomBasicWeakness() {
      const baseUrl = 'https://arkhamdb.com/';

      const randomNumber = Math.floor(
        Math.random() * this.ownedCards.length
      );
      const randomCard = this.ownedCards[Math.floor(randomNumber)];

      const url = `${baseUrl}api/public/card/${randomCard}`;
      const result = await axios.get(url);

      const cardImage = `${baseUrl}${result.data.imagesrc}`;
      this.weaknessImageUrl = cardImage;
    },

    addSetCards() {
      this.ownedCards = [];

      this.ownedSets.forEach((set) => {
        this.ownedCards.push(...this.setCodes[set]);
      });
    },
  },
};
</script>

<template>
  <div class="container">
    <el-button
      type="primary"
      size="large"
      @click="getRandomBasicWeakness"
      :disabled="!ownedSets.length"
    >
      Generate Random Basic Weakness
    </el-button>
    <el-checkbox-group @change="addSetCards" v-model="ownedSets">
      <el-checkbox label="core">Core Set</el-checkbox>
      <el-checkbox label="dwl">Dunwich Legacy</el-checkbox>
      <el-checkbox label="ptc">Path to Carcosa</el-checkbox>
      <el-checkbox label="tfa">Forgotten Age</el-checkbox>
      <el-checkbox label="tcu">Circle Undone</el-checkbox>
      <el-checkbox label="tde">Dream-Eaters</el-checkbox>
      <el-checkbox label="tic">Innsmouth Conspiracy</el-checkbox>
      <el-checkbox label="eote">The Edge of the Earth</el-checkbox>
      <el-checkbox label="rtdwl">Return to DL</el-checkbox>
      <el-checkbox label="rtptc">Return to PtC</el-checkbox>
      <el-checkbox label="rttfa">Return to TFA</el-checkbox>
      <el-checkbox label="rttcu">Return to CU</el-checkbox>
      <el-checkbox label="nate">Nathaniel Cho</el-checkbox>
      <el-checkbox label="harvey">Harvey Walters</el-checkbox>
      <el-checkbox label="wini">Winifred Habbamock</el-checkbox>
      <el-checkbox label="jackie">Jacqueline Fine</el-checkbox>
      <el-checkbox label="stella">Stella Clark</el-checkbox>
    </el-checkbox-group>
    <img class="weakness-image" :src="weaknessImageUrl" />
  </div>
</template>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
  display: inline-block;
  flex-direction: column;
}
.weakness-image {
  display: block;
  margin: auto;
  margin-top: 20px;
  width: 500px;
}
</style>
