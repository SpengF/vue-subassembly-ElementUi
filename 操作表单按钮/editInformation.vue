<template>
  <div class="editInformation">
    <div class="editInformationLeft">
      <div @click="visibilityEle" class="leftIcon">
        <span class="el-icon-arrow-down" v-if="myarrowShow"></span>
        <span class="el-icon-arrow-right" v-if="!myarrowShow"></span>
        {{titleLeft}}
      </div>
    </div>
    <div class="editInformationRight">
      <slot></slot>
    </div>
  </div>
</template>

<script lang="ts">
import { Component,Prop,Vue,Emit} from 'vue-property-decorator';
@Component
export default class editInformation extends Vue{
  @Prop() private titleLeft?:String
  @Prop({
    type:Boolean,
    default:false
  }) private showList!:Boolean
  myarrowShow=this.showList
  @Emit()
  visibilityEle(){
    this.myarrowShow=!this.myarrowShow
  }
}
</script>
<style lang='scss'>
.editInformation{
  display: flex;
  justify-content: space-between;
  // background-image: linear-gradient(#27eac3, #2eb59a);
  background-color: #3f6fa0;
  height: 40px;
  line-height: 40px;
  .editInformationLeft{
    .leftIcon{
      cursor: pointer;
      user-select:none;
      padding-left:10px;
    }
  }
  .editInformationRight{
    .el-button{
      padding: 6px 12px;
    }
  }
}
</style>
