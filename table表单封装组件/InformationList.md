##InformationList
参数 | 说明 | 类型
--|:--:|--:
tableData | 需要给table表格穿的参 | Array<Object>
userRadio | 是否显示单选框（默认为false显示多选框） | Boolean
titleAndList | 整个表格需要显示哪些列数以及表头内容 | Array<Object>
size|每页显示页数(不传默认每页10条)|Bumber
total|总页数|Number
onInfinite | 组件方法（点击分页按钮的回调） | 回调函数为当前页码
---
获取选中的单选框内容this.$refs.informationList.radioInfomation      //Object
获取选中的多选框内容this.$refs.informationList.multipleSelection    //Array

``` javascript
 <InformationList v-show="a" ref="informationList" :total='total' :tableData="tableData" :titleAndList='titleAndList' @onInfinite='onInfinite>
      </InformationList>
      titleAndList=[
      {width:'120',lable:'xiaoming',prop:'dates'},
      {width:'120',lable:'dfasd',prop:'name',sortable:true}, //sortable是否需要排序，默认为false
      {width:'400',lable:'asdas',prop:'address',showoverflowtooltip:true}]  //showoverflowtooltip超出行是否缩略显示（默认为false）
    tableData=[{
        dates: '2016-05-03',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        dates: '2016-05-02',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1518 弄'
      }]
    total=20
    onInfinite(val: number=1){
      this.total=20
    }
```


