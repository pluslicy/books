# day04 表单&crud小案例

react中的表单工作方式与原生html表单工作方式有些不同，html的每个表单元素都有一个单独的状态。在react中，我们将每个表单元素的状态都与state建立一种联系，以达到双向数据绑定目的，这样极大的简化了表单操作，可以方便的获取表单数据。



## 1. 单行文本框/密码框/多行文本框

为input绑定onChange事件，每当用户输入改变的时候就会执行handleChange函数，在该函数内部，获取当前输入框的name以及value，通过name修改state中相对应的值，由于state值改变，而input中的value值又与state中的值绑定，所以会引起render函数的再次执行，此时input中的值与state对应的值保持一致，即完成了双向数据绑定。

```javascript
class MyForm extends React.Component{
  constructor(props){
    super(props);
    this.state = {
      username:'',
      password:'',
      description:''
    };
  }


  // 每当表单元素状态改变的时候将表单元素中的值关联到state中。进而渲染到页面
  handleChange=(event)=>{
    let name = event.target.name;
    let value = event.target.value;
    this.setState((state)=>({
        [name]:value
    }))
  }

  render(){
    return (
      <form onSubmit={this.handleSubmit}>
        {JSON.stringify(this.state)} 
        用户名: 
        <input type="text" name="username" value={this.state.username} 
            onChange={this.handleChange}/> <br/>
         密码: 
        <input type="password" name="password" value={this.state.password}
            onChange={this.handleChange}/><br/>
        介绍：
        <textarea name="description" value={this.state.description} 
              onChange={this.handleChange}></textarea> <br/>
      </form>
    )
  }
}
```



##2. 单选按钮，复选按钮

单选按钮比较复杂，首先，name应该保持一致，然后value值为该元素的值，最后要默认选中的话需要设置checked属性。

复选按钮与单行文本框类型，但是要注意，它的默认值value是绑定到select元素上的

```javascript
class MyForm extends React.Component{
      constructor(props){
        super(props);
        this.state = {
          gender:'男',
          address:'山西'
        };
      }
      
      // 每当表单元素状态改变的时候将表单元素中的值关联到state中。进而渲染到页面
      handleChange=(event)=>{
        let name = event.target.name;
        let value = event.target.value;
        this.setState((state)=>({
            [name]:value
        }))
      }

      render(){
        return (
          <form onSubmit={this.handleSubmit}>
            {JSON.stringify(this.state)} 
            <hr/>
            性别：
            <label>
              <input type="radio" name="gender" value="男" onChange={this.handleChange} 
                checked={this.state.gender=="男"?true:false}/>男
            </label>
            <label>
              <input type="radio" name="gender" value="女" onChange={this.handleChange}  
                checked={this.state.gender=="女"?true:false}/>女
            </label><br/>
            地址:
            <select name="address" 
			  value={this.state.address} 
              onChange={this.handleChange}>
              <option value="江苏">江苏</option>
              <option value="山西">山西</option>
              <option value="河南">河南</option>
              <option value="陕西">陕西</option>
            </select>  <br/>
           
          </form>
        )
      }
    }
```

## 3. curd备忘录

完成一个备忘信息的增删改查功能



[视频链接](https://pan.baidu.com/s/1EHh9sYa4sbZwYT6tbmGx8A)提取码: zv2i 

