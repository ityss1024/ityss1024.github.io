

监听对象中的子属性:

```javascript

watch: {
    'jielun.jcjg': {
      handler: function(val, oldVal) {
          console.log(val)   // 输出 当前jielun.jcjg 的值
        if(val=='符合'){
          this.jielun.jcjgcl = '通过'
        } else if(val=='不符合'){
          this.jielun.jcjgcl = '食品生产经营者立即停止食品生产经营活动'
        } else if(val=='基本符合'){
          this.jielun.jcjgcl = '书面限期整改'
        }
      },
      deep: true,  // 深度监听   监听对象中的子属性
      immediate: true  // 进入即执行
    }
  }
```

方式2   可使用  @change 这个属性来监听值得改变  注意 @change只针对select框

```javascript
<el-form-item label="检查结果" prop="jcjg" >
<el-select v-model="jielun.jcjg" @change="changeJGCL">  // 添加监听方法
<el-option value="符合" label="符合" />
<el-option value="不符合" label="不符合" />
<el-option value="基本符合" label="基本符合" />
</el-select>
</el-form-item>

changeJGCL(val){   // 监听方法得实现
if(val=='符合'){
this.jielun.jcjgcl = '通过'
} else if(val=='不符合'){
this.jielun.jcjgcl = '食品生产经营者立即停止食品生产经营活动'
} else if(val=='基本符合'){
this.jielun.jcjgcl = '书面限期整改'
}
},
```

