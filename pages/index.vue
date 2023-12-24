<template>
  <v-container class="bk-pink">
    <v-row class="p-40">
      <v-col class="p-12 b-dash-pink br-20 tx-center fs-80">
        <p v-if="!loading" v-text="selectNum" />
        <client-only v-if="loading">
          <vue-loading type="spiningDubbles" color="#fed3e6" :size="{ width: '120px', height: '120px' }" />
        </client-only>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <v-btn height="60px" block color="#d56d8b" @click="roulette" :disabled="loading">Start</v-btn>
      </v-col>
    </v-row>
    <v-row class="pb-40" id="list">
      <v-col :key="call" v-for="call in callList">
        <call-num :num="call" :called="calledList.includes(call)" />
      </v-col>
    </v-row>
    <v-row class="pb-40">
      <v-col>
        <v-btn height="60px" block color="#ed1a3d" @click="reset" :disabled="loading">Reset</v-btn>
      </v-col>
    </v-row>
  </v-container>
</template>
<script>
import callNum from '@/components/callNum'

export default {
  components: { callNum },
  layout () {
    return 'index'
  },
  data() {
    return {
        selectNum: '↓STARTをおしてね↓',
        loading: false,
        max: 75,
        callList: [],
        uncallList: [],
        calledList: []
    }
  },
  created() {
    this.max = Number(this.$route.query.max) ? Number(this.$route.query.max) : 75;
    this.callList = [...Array(this.max)].map((_, i) => i + 1)
    this.uncallList = [...Array(this.max)].map((_, i) => i + 1)
  },
  methods: {
    roulette() {
      this.loading = true;
      if (this.uncallList.length != 0) {
        this.selectNum = this.uncallList[Math.floor(Math.random() * this.uncallList.length)]
        this.uncallList = this.uncallList.filter((n) => n != this.selectNum)
        this.calledList.push(this.selectNum)
      } else {
        this.selectNum = 'おわり'
      }
      setTimeout(() => {
        this.loading = false
        this.calledList.push(this.selectNum)
      }, 500)
    },
    reset() {
      this.uncallList = [...Array(this.max)].map((_, i) => i + 1)
      this.calledList = []
      this.selectNum = '↓STARTをおしてね↓'
    },
  }
}
</script>
<style scoped>
.fs-80 { font-size: 80px; }
.tx-center { text-align: center; }
.p-12 { padding: 12px; }
.p-40 { padding: 40px; }
.pb-40 { padding-bottom: 40px; }
.bk-pink { background-color: #fed3e6; }
.b-dash-pink { border: dashed #ffe0ff; background-color: #ffffff; }
#list {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  flex-wrap: wrap;
}
</style>