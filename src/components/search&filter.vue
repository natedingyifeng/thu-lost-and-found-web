<template>
  <div>
    <el-input placeholder="请输入内容"
              v-model="input">
      <el-select v-model="select"
                 class="select"
                 slot="prepend"
                 placeholder="请选择">
        <el-option v-for="item in options"
                   :key="item.value"
                   :label="item.label"
                   :value="item.value">
        </el-option>
      </el-select>
      <el-button slot="append"
                 icon="el-icon-search"
                 @click="search"></el-button>
    </el-input>
  </div>
</template>
<style scoped>
.select {
  width: 150px;
}
</style>
<script>
export default {
  props: {
    options: Array
  },
  data: function () {
    return {
      select: 'search',
      input: ''
    }
  },
  methods: {
    search: function () {
      this.$emit('search', this.select, this.input)
    }
  }

}
</script>
