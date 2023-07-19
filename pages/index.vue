<template>
  <div class="app-container">
    <div class="text-frame">
      <p>{{ message }}</p>
    </div>
    <div>
      <center>
        <h1>สวัสดีค่ะ กรุณาป้อนข้อมูล</h1>
        <br>
        <label>กรุณาใส่ตัวเลข:</label>
        <input type="" v-model="rows">
        <button @click="submit">Submit</button>

        <ul v-if="showPyramids">
          <div class="pyramid-container">
            <h2></h2>
            <ul v-for="(row, index) in pyramid" :key="index">
              <span v-for="num in row" :key="num" class="asterisk">*</span>
            </ul>
          </div>
          <div class="pyramid-container">

            <ul v-for="(row, index) in reversedPyramid" :key="index">
              <span v-for="(num, numIndex) in row" :key="numIndex" class="asterisk">
                {{ num }}
              </span>
            </ul>
          </div>
        </ul>
      </center>
      <div v-if="pyramid.length === 0 && reversedPyramid.length === 0"></div>
    </div>
  </div>
</template>

<style>
.pyramid-container {
  margin-bottom: 0px;
}

h2 {
  margin-bottom: 1px;
}

.asterisk {
  margin-right: 25px;
}
</style>

<script>
export default {
  data() {
    return {
      rows: 0,
      pyramid: [],
      reversedPyramid: [],
      showPyramids: false,
    };
  },
  methods: {
    generatePyramids() {
      const rows = parseInt(this.rows);
      if (!isNaN(rows) && rows > 0) {
        let pyramid = [];
        let reversedPyramid = [];
        let prev = "";
        let curr = "*";

        for (let i = 0; i < rows; i++) {
          let row = [];
          let reversedRow = [];
          for (let j = 0; j <= i; j++) {
            row.push(curr);
            reversedRow.unshift(curr);
            let temp = curr;
            curr = temp;
            prev = temp;
          }
          pyramid.push(row);
          reversedPyramid.push(reversedRow);
        }

        this.pyramid = pyramid;
        this.reversedPyramid = reversedPyramid.reverse();
      } else {
        this.pyramid = [];
        this.reversedPyramid = [];
      }
    },
    submit() {
      this.generatePyramids();
      this.showPyramids = true;
    },
  },
};
</script>
