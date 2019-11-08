<template>
<div class="second" :val='value_'>
  <el-tabs :tab-position="'left'" style="height: 200px;" v-model="activeName">
    <el-tab-pane label="每时执行">
      <el-radio v-model="radio" label="1">是</el-radio>
    </el-tab-pane>
    <el-tab-pane label="周期">
      从
      <el-input-number v-model="cycle.start" :min="0" :max="59"></el-input-number>
      至
      <el-input-number v-model="cycle.end" :min="2" :max="59"></el-input-number>
      时
    </el-tab-pane>
    <el-tab-pane label="循环">
      从
      <el-input-number v-model="loop.start" :min="0" :max="59"></el-input-number>
      时开始，每
      <el-input-number v-model="loop.times" :min="1" :max="59"></el-input-number>
      时执行一次
    </el-tab-pane>
    <el-tab-pane label="指定">
      <el-checkbox-group v-model="checkboxpoint">
        <div v-for='i in 3' :key="i">
          <el-checkbox v-for="j in 10" :key="i+''+j" :label="(i-1)+''+(j-1)" v-if="((i-1)+''+(j-1))<24"></el-checkbox>
        </div>
    </el-checkbox-group>
    </el-tab-pane>
  </el-tabs>
</div>
</template>
<script lang="ts">
import { Component,Prop,Vue,Emit,Watch} from 'vue-property-decorator';
interface cycleAndloop{
  start:string,
  end?:string,
  times?:string 
}
@Component
export default class SecondAndMinutes extends Vue{
  cycle:cycleAndloop={
    start:'',
    end:''
  }
  loop:cycleAndloop={
    start:'',
    times:''
  }
  checkboxpoint:Array<string>=[]
  radio:string='1'
  activeName:string='1'
  created(){
    this.show()
  }
  get value_():void{
    let result=[];
    if(this.activeName=='0'){
      result.push('*')
    }
    if(this.activeName=='1'){
      result.push(`${this.cycle.start}-${this.cycle.end}`)
    }
    if(this.activeName=='2'){
      result.push(`${this.loop.start}/${this.loop.times}`)
    }
    if(this.activeName=='3'){
      result.push(this.checkboxpoint.join(','))
    }
    this.$emit('input',result.join(''))
    return;
  }
  @Prop() value!:string;
  @Watch('value')
  bankshow():void{
    this.show()
  }
  show(){
    if(this.value==='*'){
      this.activeName='0'
    }
    if(this.value.indexOf('-')!==-1){
      this.activeName='1'
      let arrs=this.value.split('-')
      this.cycle.start=arrs[0]
      this.cycle.end=arrs[1]
    }
    if(this.value.indexOf('/')!==-1){
      this.activeName='2'
      let arrs=this.value.split('/')
      this.loop.start=arrs[0]
      this.loop.times=arrs[1]
    }
    if(this.value.indexOf(',')!==-1 || !Number.isNaN(Number(this.value))){
      this.activeName='3'
      let arrs=this.value.split(',')
      this.checkboxpoint=arrs;
    }
    if(this.value==='?'){
      this.activeName='4'
    }
  }
}
</script>
<style lang="less">

</style>