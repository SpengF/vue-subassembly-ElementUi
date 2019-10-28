##editInformation
参数 | 说明 | 类型
--|:--|:--|
titleLeft|栏目显示标题|string
visibility-ele|点击展开关闭回调函数|function
showList|是否为展开状态（默认为false）|Boolean
```javascript
<EditInformation titleLeft='不定期承保管理' @visibility-ele='callback'>
  <el-button type="primary">主要按钮</el-button>
  <el-button type="success">成功按钮</el-button>
  <el-button type="info">信息按钮</el-button>
</EditInformation>
export default class mainView extends Vue{
  callback(){
    
  }
}
```


