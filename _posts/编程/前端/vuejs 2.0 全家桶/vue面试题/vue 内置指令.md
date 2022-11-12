



- v-bind - 绑定属性，动态更新HTML元素上的属性。例如 v-bind:class。
- v-on - 用于监听DOM事件。例如 v-on:click v-on:keyup
- v-html - 赋值就是变量的innerHTML -- 注意防止xss攻击
- v-text - 更新元素的textContent
- v-model - 1、在普通标签。变成value和input的语法糖，并且会处理拼音输入法的问题。2、再组件上。也是处理value和input语法糖。
- v-if / v-else / v-else-if。可以配合template使用；在render函数里面就是三元表达式。
- v-show - 使用指令来实现 -- 最终会通过display来进行显示隐藏
- v-for - 循环指令编译出来的结果是 -L 代表渲染列表。优先级比v-if高最好不要一起使用，尽量使用计算属性去解决。注意增加唯一key值，不要使用index作为key。