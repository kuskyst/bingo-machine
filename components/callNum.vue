<template>
  <p class="icon" :class="[ 'bo-' + digit , called ? 'bk-' + digit : 'bk-white' ]" v-text="num" />
</template>
<script>
export default {
  props: {
    num: { type: Number },
    called: { type: Boolean, default: false }
  },
  data() { return { digit: 0 } },
  created() {
    this.digit = this.num <= 15 ? 1 : this.num <= 30 ? 2 : this.num <= 45 ? 3 : this.num <= 60 ? 4 : this.num <=75 ? 5 : 6
  }
}
</script>
<style scoped>
.icon {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  margin: 6px;
  transition: 1s;
  text-align: center;
  padding: 20px;
  font-size: 20px;
  font-weight: bold;
}
.bo-1 { border: 3px dashed #f45c19; }
.bo-2 { border: 3px dashed #4a96d6; }
.bo-3 { border: 3px dashed #28b25c; }
.bo-4 { border: 3px dashed #eaa317; }
.bo-5 { border: 3px dashed #d56d8b; }
.bo-6 { border: 3px dashed #8f5b98; }
.bo-7 { border: 3px dashed #9b9b9b; }
.bk-white {background-color: #ffffff; transition: 0.3s all; }
.bk-1 { background-color: #f45c19; transition: 0.3s all; }
.bk-2 { background-color: #4a96d6; transition: 0.3s all; }
.bk-3 { background-color: #28b25c; transition: 0.3s all; }
.bk-4 { background-color: #eaa317; transition: 0.3s all; }
.bk-5 { background-color: #d56d8b; transition: 0.3s all; }
.bk-6 { background-color: #8f5b98; transition: 0.3s all; }
.bk-7 { background-color: #9b9b9b; transition: 0.3s all; }
</style>