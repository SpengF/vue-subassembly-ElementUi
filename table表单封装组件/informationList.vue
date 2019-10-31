<template>
  <div class="informationList">
    <el-table ref="multipleTable" 
      :data="tableData" tooltip-effect="dark" 
      style="width: 100%" 
      @selection-change="handleSelectionChange">
        <el-table-column  width="35" v-if='userRadio' fixed>
          <template v-slot="scope">
            <el-radio :label="scope.$index" v-model="radio" @change="radioChange(scope.row)">&nbsp;</el-radio>
          </template>
        </el-table-column>
        <el-table-column
          type="selection"
          width="55"
          v-if='!userRadio'
          fixed
          >
        </el-table-column>
        <template v-for="item in titleAndList" :keys="item.prop">
          <el-table-column  :label="item.lable"
          :width="item.width"
          :prop="item.prop"
          :show-overflow-tooltip="item.showoverflowtooltip"
          :sortable="item.sortable"
          >
          </el-table-column>
        </template>
    </el-table>
    <el-pagination
      background
      layout="total,prev, pager, next,jumper"
      :hide-on-single-page='hidePage'
      :page-size='size'
      :total="total"
      @current-change='currentPage'
      >
    </el-pagination>
  </div>
</template>

<script lang ='ts'>
import { Component,Prop,Vue,Emit,Watch} from 'vue-property-decorator';
interface Page {
  total:number,
  size:number
}
@Component
export default class informationList extends Vue{
  private radio: number=-1;
  private radioInfomation: string='';  //单选框选中的数据
  private multipleSelection: Array<Object>=[]; //多选框选中的数据
  @Prop() private tableData?: Array<Object>;
  @Prop() private total!: Number;
  @Prop({
    default:10
  }) private size!: Number;
  @Prop() private titleAndList!: Array<Object>;
  @Prop({default:false}) private userRadio!: Boolean;
  get hidePage(): Boolean{   //当显示为一页的时候就隐藏掉
    return (this as any).total%(this as any).size<1||(this as any).total%(this as any).size==1;
  }
  radioChange(val: string):void{
    this.radioInfomation=val;
  };
  handleSelectionChange(val: Array<Object>):void{
    this.multipleSelection = val;
  }
  @Emit('onInfinite')
  currentPage(val: number):number{
    return val;
  }
  resetRadio(){
    this.radio=-1;
    this.radioInfomation='';   //选中数据清空，让用户自己再进行选择
  }
}
</script>

<style lang='scss'>
.el-pagination{
  text-align: center;
  padding-top: 20px;
}
.el-table__fixed{
  height:100% !important;
}
</style>
