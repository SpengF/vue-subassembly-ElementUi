##InformationList
参数 | 说明 | 类型
--|:--:|--:
tableData | 需要给table表格穿的参 | Array<Object>
userRadio | 是否显示单选框（默认为false显示多选框） | Boolean
titleAndList | 整个表格需要显示哪些列数以及表头内容 | Array<Object>
paginationObject | 分页传的总数和每页显示条数 | Object,{total:5,size:1}
onInfinite | 不用在组件定义，直接写在父组件methods中(分页请求数据) | 回调函数为当前页码
---
获取选中的单选框内容this.$refs.informationList.radioInfomation      //Object
获取选中的多选框内容this.$refs.informationList.multipleSelection    //Array

``` javascript
<InformationList ref="informationList" :userRadio='true' :tableData="tableData" :paginationObject='paginationObject' :titleAndList='titleAndList'>
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
    paginationObject={total:5,size:1}  //size为每页几个
    onInfinite(val: number=1){
      this.paginationObject.total=val
    }
```


