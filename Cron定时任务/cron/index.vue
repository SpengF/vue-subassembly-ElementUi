<template>
  <div class="cron" :val='value_'>
    <el-tabs v-model="activeName" type="border-card" >
      <el-tab-pane label="秒" name="s">
        <Second-and-minutes v-model="Stime" names='秒'></Second-and-minutes>
          {{Stime}}
      </el-tab-pane>
      <el-tab-pane label="分" name="mi">
        <Second-and-minutes v-model="Mitime" names='分'></Second-and-minutes>
        {{Mitime}}
      </el-tab-pane>
      <el-tab-pane label="时" name="h">
        <Hour v-model="Htime"></Hour>
        {{Htime}}
      </el-tab-pane>
      <el-tab-pane label="天" name="d">
        <Day v-model="Dtime"></Day>
        {{Dtime}}
      </el-tab-pane>
      <el-tab-pane label="周" name="w">
        <Week v-model="Wtime"></Week>
        {{Wtime}}
      </el-tab-pane>
      <el-tab-pane label="月" name="mo">
        <Month v-model="Motime"></Month>
        {{Motime}}
      </el-tab-pane>
    </el-tabs>
    <el-table
      :data="tableData"
      height="250"
      border
      style="width: 100%">
      <el-table-column
        prop="Stime"
        label="秒">
      </el-table-column>
      <el-table-column
        prop="Mitime"
        label="分">
      </el-table-column>
      <el-table-column
        prop="Htime"
        label="时">
      </el-table-column>
      <el-table-column
        prop="Dtime"
        label="天">
      </el-table-column>
      <el-table-column
        prop="Wtime"
        label="周">
      </el-table-column>
      <el-table-column
        prop="Motime"
        label="月">
      </el-table-column>
    </el-table>
  </div>
</template>
<script lang="ts">
import { Component,Prop,Vue,Emit,Watch} from 'vue-property-decorator';
import SecondAndMinutes from './secondAndMinutes.vue'
import Hour from './hour.vue'
import Day from './day.vue'
import Week from './week.vue'
import Month from './month.vue'
@Component({
  components:{
    SecondAndMinutes,
    Hour,
    Day,
    Week,
    Month
  }
})
export default class Cron extends Vue{
  activeName='d'
  Stime:string='*'
  Mitime:string='*'
  Htime:string='*'
  Dtime='?'
  Wtime='*'
  Motime='*'
  a=''
  created(){
    this.backshow()
  }
  get tableData():Array<object>{
    return [{
      Stime:this.Stime,
      Mitime:this.Mitime,
      Htime:this.Htime,
      Dtime:this.Dtime,
      Wtime:this.Wtime,
      Motime:this.Motime,
    }]
  }
  get value_(){
    if (!this.Dtime && !this.Wtime) {
      return ''
    }
    if (this.Dtime === '?' && this.Wtime === '?') {
      this.$message.error('日期与星期不可以同时为“不指定”')
    }
    if (this.Dtime === '?' && this.Motime === '?') {
      this.$message.error('日期与月不可以同时为“不指定”')
    }
    if (this.Dtime !== '?' && this.Wtime !== '?') {
      this.$message.error('日期与星期必须有一个为“不指定”')
    }
    let allMsg=`${this.Stime} ${this.Mitime} ${this.Htime} ${this.Dtime} ${this.Wtime} ${this.Motime}`
    this.a=allMsg
    this.$emit('input',allMsg)
    return;
  }
  @Prop() value!:string;
  @Watch('value')
  backshow(){
    if(!this.value){
      return;
    }
    let arrs=this.value.split(' ')
    this.Stime=arrs[0]
    this.Mitime=arrs[1]
    this.Htime=arrs[2]
    this.Dtime=arrs[3]
    this.Wtime=arrs[4]
    this.Motime=arrs[5]
  }
}
</script>
<style lang="less">
.cron{
  color: #000;
  width: 630px;
  .el-tabs__header.is-top{
    .el-tabs__nav{
      width: 100%;
      display: flex;
      justify-content: space-around;
      .el-tabs__item{
        flex: 1;
      }
    }
  }
  #pane-1,#pane-2,#pane-6,#pane-5{
    display: flex;
    align-items: center;
    .el-input-number{
      width: 120px;
    }
  }
  .second{
    height: 100%;
    .el-tabs--left{
      height: 100% !important;
    }
  }
  .el-checkbox-group{
    text-align: left;
    .el-checkbox{
      margin-right: 6px;
      padding-top: 10px;
    }
  }
  .has-gutter{
    tr{
      th{
        background-color: #f5f7fa;
      }
    }
  }
}
</style>