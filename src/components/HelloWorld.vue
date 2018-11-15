<template>
  <el-container>
    <el-aside width="50%">
      <div v-for="group in Object.keys(UPPER_BLOCK_BUTTONS)"
              :key="group"
              class="block">
        <div class="title">{{group}}</div>
        <el-button v-for="(button, index) in UPPER_BLOCK_BUTTONS[group]"
                   class="button"
                   :key="button"
                   :type="isButtonSelected(1, button, group, index)"
                   @click="handleBtn1(group, button)">{{button}}
        </el-button>
      </div>
      <div class="block">
        <div class="title">EFFECTIVE STACK SIZE</div>
        <el-button v-for="(size, index) in EFFECTIVE_STACK_SIZE"
                   class="button"
                   :key="size"
                   :type="isButtonSelected(2, size, null, index)"
                   @click="handleBtn2(index)">{{size}}
        </el-button>
      </div>
    </el-aside>
    <el-main>
      <img :src="path">
    </el-main>
  </el-container>
</template>

<script>
const EFFECTIVE_STACK_SIZE = ['0-7', '7-10', '10-13', '13-17', '17-21', '21+']
const UPPER_BLOCK_BUTTONS = {
  'HU SB': ['ACTION'],
  'HU BB': [
    'SB MINRASE',
    'SB 3x RASE',
    'SB PUSH',
    'SB COMPLETE'
  ],
  '3MAX BU': ['ACTION'],
  '3MAX SB': [
    'BU MINRASE',
    'BU x3 RAISE',
    'BU PUSH',
    'BU LIMP',
    'BU FOLD'
  ],
  '3MAX BB': [
    'BU MINRASE/SB CALL',
    'BU MINRASE/SB 3BET PUSH',
    'BU PUSH/SB CALL',
    'BU LIMP',
    'BU LIMP/SB COMPLETE',
    'BU LIMP/SB ISO RAISE 3BB',
    'SB MINRASE',
    'SB 3X RAISE',
    'SB PUSH',
    'SB COMPLETE'
  ],
}

export default {
  name: 'HelloWorld',
  data() {
    return {
      EFFECTIVE_STACK_SIZE,
      UPPER_BLOCK_BUTTONS,
      btn1: 'HUSBACTION',
      btn2: '1'
    }
  },
  methods: {
    replaceWithEmpty(string){
      return string.replace(/\s|\//g, '');
    },
    handleBtn1(group, button) {
      this.btn1 = this.replaceWithEmpty(group+button);
    },
    handleBtn2(index) {
      this.btn2 = index+1
    },
    isButtonSelected(index, button, group, stackSizeIndex){
      switch (index) {
        case 1:
          return this[`btn${index}`].includes(this.replaceWithEmpty(group+button))
            ? 'primary'
            : 'plain';
        case 2:
          return stackSizeIndex === this.btn2 - 1
            ? 'primary'
            : 'plain';
      }
    }
  },
  computed: {
    path() {
      return require('../assets/' + this.btn1 + '/' + this.btn2 + '.png');
    }
  }
}
</script>

<style scoped>
.block {
  padding: 15px;
  display: flex;
  text-align: left;
  flex-wrap: wrap;
}
.button {
  margin-bottom: 10px;
}
.title {
  padding: 15px;
  font-weight: bold;
  padding-bottom: 10px;
}
</style>
