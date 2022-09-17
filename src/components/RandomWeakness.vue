<script>
/* eslint-disable */
import axios from 'axios';

export default {
  data() {
    return {
      ownedSets: [],
      ownedCards: [],
      setCodes: {
        core: {
          codes: [
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
          friendlyName: 'Core Set',
        },
        dwl: {
          codes: [
            '02037',
            '02037',
            '02038',
            '02038',
            '02039',
            '02039',
          ],
          friendlyName: 'Dunwich Legacy',
        },
        ptc: {
          codes: ['03040', '03040', '03041', '03042'],
          friendlyName: 'Path to Carcosa',
        },
        tfa: {
          codes: ['04038', '04040'],
          friendlyName: 'Forgotten Age',
        },
        tcu: {
          codes: ['05041', '05041', '05042', '05042'],
          friendlyName: 'Circle Undone',
        },
        tde: {
          codes: ['06035', '06036', '06037', '06038'],
          friendlyName: 'Dream-Eaters',
        },
        tic: {
          codes: ['07038', '07038', '07039', '07039', '07040'],
          friendlyName: 'Innsmouth Conspiracy',
        },
        eote: {
          codes: ['08130', '08131', '08132', '08133'],
          friendlyName: 'Edge of the Earth',
        },
        rtdwl: {
          codes: ['51011', '51011'],
          friendlyName: 'Return to DWL',
        },
        rtptc: {
          codes: ['52011', '52012', '52013'],
          friendlyName: 'Retrun to PtC',
        },
        rttfa: {
          codes: ['53012', '53013'],
          friendlyName: 'Return to TFA',
        },
        rttcu: {
          codes: ['54014', '54015', '54015'],
          friendlyName: 'Return to TCU',
        },
        nate: { codes: ['60104'], friendlyName: 'Nathaniel Cho' },
        harvey: { codes: ['60204'], friendlyName: 'Harvey Walters' },
        wini: {
          codes: ['60304'],
          friendlyName: 'Winifred Habbamock',
        },
        jackie: { codes: ['60404'], friendlyName: 'Jacqueline Fine' },
        stella: { codes: ['60504'], friendlyName: 'Stella Clarke' },
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
        this.ownedCards.push(...this.setCodes[set].codes);
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
      <el-checkbox
        v-for="(set, key) in setCodes"
        :label="key"
        :key="key"
      >
        {{ set.friendlyName }}
      </el-checkbox>
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
