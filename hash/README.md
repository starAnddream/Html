#历史记录管理---HTML5定义了两种历史记录的机制
##利用location.hash与hashchange事件
设置location.hash属性会更新显示地址栏中的URL，同时会在浏览器历史记录中增加一条记录。接下来用户前进后退会切换不同的文档状态，
这个时候应用必须想办法检测出来。浏览器一旦发现片段标识符发生改变，就会在window对象上触发hashchange事件。
##利用history.pushState()方法和window.popstate事件。
* pushState（argu1,arg2,arg3）:当web进入一个新的状态的时候，history.pushState将状态添加到历史记录中
arg1:Object,该对象包含用于恢复当前文档状态所需要的信息
arg2:可选标题
arg3:可选URL，表示当前状态位置
* History还定义了replaceState()方法，该方法和pushState接收同样的参数，不同的是他不将新的状态添加到历史记录，而是用新的状态代替
当前状态。
* 点击前进后退按钮时，Windows会触发popstate事件，该事件对象有一个event属性，包含了传递给pushState()方法状态对象的副本
```javascript
function save(state){
   if(!history.pushState)return;
   var url="#guess"+state.guesstimes;
   history.pushState(state,"",url);
}
function popState(event){
   if(event.state){
   console.log(event);
   state=event.state;
   display(state);
   }
   else{
   console.log(2222);
   history.replaceState(state,"","#guess"+state.guesstimes);
   }
   ````
