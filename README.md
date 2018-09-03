### Vue Code
MVVM 双向绑定 观察者模式

Observe 时机 -- Vue实例化时调用 即new Vue

Observe 角色 -- 遍历data,然后调用Object.defineReactive

1、 识别子对象是否嵌套 递归 
2、 定义对象 
    1）数据读取时 是否要给Observe添加一个观察者 getter
    2）数据变化 通知观察者 setter

Dep 角色 -- 维护一个dep列表, 添加列表 通知更新 通知观察者对象 

Watcher 每个实例对象有个update函数 update在Watcher中定义 执行编译时初始化 value赋值时 触发get 触发Observer通过defineProperty代理的getter函数上，从而添加观察者列表addSub

new Vue 基本配置属性 
observe 监听所有数据 
compile编译，对模板分析，指令 双向绑定 自定义事件处理，执行watcher ,不同的watcher实例化的过程中会找到observer,把当前的watcher对象塞进去，后续data变化，可以通过列表找到watcher对象当初实例化时指定的回调并执行赋值操作 从而实现数据的绑定。（从Data->View）

如果是v-model input双向绑定  则是通过在编译时判断了节点类型 注册事件 从而实现了View到Data的数据流更新