---
title: vue-property-decorator
categories: vue
tags: vue装饰器
---

# vue-property-decorator

安装
引入
@Component
registerHooks
data
computed
@Prop
@PropSync
@Watch
@Ref
@Emit
@Model
@Provide/@Inject/@ProvideReactive/@InjectReactive
Mixins (在vue-class-component中定义)

怎么使vue支持ts写法呢,我们需要用到 vue-property-decorator，这个库完全依赖于 vue-class-component.

## 一？安装
```js
npm i -D vue-proporty-decorator
```
## 二？引入
当我们在vue单文件中使用TypeScript时,引入vue-property-decorator之后,script中的标签就变为这样:

<script lang="ts"></script>

## 三？@Component
注： 该属性完全继承于vue-class-component
属性参数：@Component(options: ComponentOptions = {})
参数说明：@Component 装饰器可以接收一个对象作为参数，可以在对象中声明 components ，filters，directives, beforeRouteLeave等未提供装饰器的选项，也可以声明computed，watch等

registerHooks
除了将beforeRouteLeave放在Component中之外,还可以全局注册,就是registerHooks
```js
<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'

Component.registerHooks([
  'beforeRouteLeave',
  'beforeRouteEnter',
]);

@Component
export default class App extends Vue { 
  beforeRouteEnter(to: any, from: any, next: any) {
    console.log('beforeRouteEnter')
    next()
  }

  beforeRouteLeave(to: any, from: any, next: any) {
    console.log('beforeRouteLeave')
    next()
  }
}
</script>
```
```js
data
对于data里的变量类型,我们可以直接按ts定义类变量的写法写就可以

<script lang="ts">
	 import {Vue, Component} from 'vue-property-decorator';

    @Component
    export default class "组件名" extends Vue{
        ValA: string = 'hello world';
        ValB: number = 1;
    }
</script>
等同于

<script>
    export default {
        data(){
            return {
                ValA: 'hello world',
                ValB: 1
            }
        }
    }
</script>
```
```js
computed
对于Vue中的计算属性,我们只需要将该计算属性名定义为一个函数,并在函数前加上get关键字即可.原本Vue中的computed里的每个计算属性都变成了在前缀添加get的函数.

<script lang="ts">
    import {Vue, Component} from 'vue-property-decorator';

    @Component
    export default class "组件名" extends Vue{
        get ValA(){
            return 1;
        }
    }
</script>

等同于

<script>
    export default {
        computed: {
            ValA: function() {
                return 1;
            }
        }
    }
</script>
```
## 四？@Prop
属性参数：@Prop(options: (PropOptions | Constructor[] | Constructor) = {})
参数说明：@Prop装饰器接收一个参数，这个参数可以有三种写法：
PropOptions，可以使用以下选项：type（类型），default（默认值），required（必填），validator（验证函数）;
Constructor[]，指定 prop 的可选类型；
Constructor，例如String，Number，Boolean等，指定 prop 的类型；

注意：属性的ts类型后面需要加上undefined类型；或者在属性名后面加上!，表示非null 和 非undefined的断言，告诉TypeScript我这里一定有值，否则编译器会给出错误提示；

比如子组件从父组件接收三个属性propA,propB,propC

propA类型为Number
propB默认值为default value
propC类型为String或者Boolean

export default {
  props: {
    propA: {
      type: Number
    },
    propB: {
      default: 'default value'
    },
    propC: {
      type: [String, Boolean]
    },
  }
}
1
2
3
4
5
6
7
8
9
10
11
12
13
我们使用vue-property-decorator提供的@Prop可以将上面的代码改造为如下:

<script lang="ts">
    import {Vue, Component, Prop} from 'vue-property-decorator';

    @Component
    export default class "组件名" extends Vue{
        @Prop(Number) propA!: number;
        @Prop({default: 'default value'}) propB!: string;
        @prop([String, Boolean]) propC: string | boolean;
    }
</script>
1
2
3
4
5
6
7
8
9
10
总结: @Prop接受一个参数可以是类型变量或者对象或者数组.@Prop接受的类型比如Number是JavaScript的类型,之后定义的属性类型则是TypeScript的类型.

@PropSync
属性参数：@PropSync(propName: string, options: (PropOptions | Constructor[] | Constructor) = {})

@PropSync装饰器与@prop用法类似，二者的区别在于：

@PropSync 装饰器接收两个参数：
propName: string 表示父组件传递过来的属性名；
options: Constructor | Constructor[] | PropOptions 与@Prop的第一个参数一致；
@PropSync 会生成一个新的计算属性。
注意：使用PropSync的时候是要在父组件配合.sync使用的

示例：

// 父组件
<template>
  <div class="PropSync">
    <h1>父组件</h1>
    like:{{like}}
    <hr/>
    <PropSyncComponent :like.sync="like"></PropSyncComponent>
  </div>
</template>

<script lang='ts'>
import { Vue, Component } from 'vue-property-decorator';
import PropSyncComponent from '@/components/PropSyncComponent.vue';

@Component({components: { PropSyncComponent },})
export default class PropSyncPage extends Vue {
  private like = '父组件的like';
}
</script>

// 子组件
<template>
  <div class="hello">
    <h1>子组件:</h1>
    <h2>syncedlike:{{ syncedlike }}</h2>
    <button @click="editLike()">修改like</button>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue, PropSync,} from 'vue-property-decorator';

@Component
export default class PropSyncComponent extends Vue {
  @PropSync('like', { type: String }) syncedlike!: string; // 用来实现组件的双向绑定,子组件可以更改父组件穿过来的值

  editLike(): void {
    this.syncedlike = '子组件修改过后的syncedlike!'; // 双向绑定,更改syncedlike会更改父组件的like
  }
}
</script>
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39
40
41
@Watch
属性参数：@Watch(path: string, options: WatchOptions = {})

参数说明：@Watch 装饰器接收两个参数：

path: string 被侦听的属性名；
options?: WatchOptions={} options可以包含两个属性 ：
immediate?:boolean 侦听开始之后是否立即调用该回调函数；
deep?:boolean 被侦听的对象的属性被改变时，是否调用该回调函数；
我们可以利用vue-property-decorator提供的@Watch装饰器来替换Vue中的watch属性,以此来监听值的变化.

在Vue中监听器的使用如下:

export default{
    watch: {
        'child': this.onChangeValue, // 这种写法默认 `immediate`和`deep`为`false`
        'person': {
            handler: 'onChangeValue',
            immediate: true,
            deep: true
        }
    },
    methods: {
        onChangeValue(newVal, oldVal){
            // todo...
        }
    }
}
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
那么我们如何使用@Watch装饰器来改造它呢?

import {Vue, Component, Watch} from 'vue-property-decorator';

@Watch('child')
onChangeValue(newVal: string, oldVal: string){
    // todo...
}

@Watch('person', {immediate: true, deep: true})
onChangeValue(newVal: Person, oldVal: Person){
    // todo...
}
1
2
3
4
5
6
7
8
9
10
11
总结: @Watch使用非常简单,接受第一个参数为要监听的属性名 第二个属性为可选对象.@Watch所装饰的函数即监听到属性变化之后的操作.

@Ref
属性参数：@Ref(refKey?: string)

参数说明：@Ref 装饰器接收一个可选参数，用来指向元素或子组件的引用信息。如果没有提供这个参数，会使用装饰器后面的属性名充当参数

<template>
  <div class="PropSync">
    <button @click="getRef()" ref="aButton">获取ref</button>
    <RefComponent name="names" ref="RefComponent"></RefComponent>
  </div>
</template>

<script lang="ts">
import { Vue, Component, Ref } from 'vue-property-decorator';
import RefComponent from '@/components/RefComponent.vue';

@Component({
  components: { RefComponent },
})
export default class RefPage extends Vue {
  @Ref('RefComponent') readonly RefC!: HTMLDocument;
  @Ref('aButton') readonly ref!: HTMLButtonElement;
  getRef() {
    console.log(this.RefC);
    console.log(this.ref);
  }
}
</script>
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
@Emit
属性参数：@Emit(event?: string)
参数说明：

@Emit 装饰器接收一个可选参数，充当事件名。如果没有提供这个参数，@Emit会将回调函数名的camelCase转为kebab-case，并将其作为事件名；
@Emit的回调函数的参数，会在回调函数没有返回值的情况下，被$emit当做第二个参数使用。
@Emit会将回调函数的返回值作为第二个参数，如果返回值是一个Promise对象，$emit会在Promise对象被标记为resolved之后触发；
<script lang="ts">
    import {Vue, Component, Emit} from 'vue-property-decorator';

    @Component
    export default class "组件名" extends Vue{
        mounted(){
            this.$on('emit-todo', function(n) {
                console.log(n)
            })
    
            this.emitTodo('world');
        }
    
        @Emit()
        emitTodo(n: string){
            console.log('hello');
        }
    }
</script>
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
运行上面的代码会打印 ‘hello’ ‘world’, 为什么呢? 让我们来看看它等同于什么

<script>
    import Vue from 'vue';

    export default {
        mounted(){
            this.$on('emit-todo', function(n) {
                console.log(n)
            })
    
            this.emitTodo('world');
        },
        methods: {
            emitTodo(n){
                console.log('hello');
                this.$emit('emit-todo', n);
            }
        }
    }
</script>
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
可以看到,在@Emit装饰器的函数会在运行之后触发等同于其函数名(驼峰式会转为横杠式写法)的事件, 并将其参数传递给$emit.
如果我们想触发特定的事件呢,比如在emitTodo下触发reset事件:

<script lang="ts">
    import {Vue, Component, Emit} from 'vue-property-decorator';

    @Component
    export default class "组件名" extends Vue{
    
        @Emit('reset')
        emitTodo(n: string){
    
        }
    }
</script>
1
2
3
4
5
6
7
8
9
10
11
12
我们只需要给装饰器@Emit传递一个事件名参数reset,这样函数emitTodo运行之后就会触发reset事件.

@Model
默认情况下，一个组件上的v-model 会把 value用作 prop且把 input用作 event，但是一些输入类型比如单选框和复选框按钮可能想使用 value prop来达到不同的目的。使用model选项可以回避这些情况产生的冲突。

下面是Vue官网的例子

Vue.component('base-checkbox', {
  model: {
    prop: 'checked',
    event: 'change'
  },
  props: {
    checked: Boolean
  },
  template: `
    <input
      type="checkbox"
      v-bind:checked="checked"
      v-on:change="$emit('change', $event.target.checked)"
    >
  `
})
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
<base-checkbox v-model="lovingVue"></base-checkbox>
1
注意：你仍然需要在组件的 props 选项里声明 checked 这个 prop。

使用vue-property-decorator提供的@Model改造上面的例子。

import { Vue, Component, Model} from 'vue-property-decorator';

@Component
export class myCheck extends Vue{
   @Model ('change', {type: Boolean})  checked!: boolean;
}
1
2
3
4
5
6
@Provide/@Inject/@ProvideReactive/@InjectReactive
属性参数：

@Provide(key?: string | symbol) / @Inject(options?: { from?: InjectKey, default?: any } | InjectKey) decorator
@ProvideReactive(key?: string | symbol) / @InjectReactive(options?: { from?: InjectKey, default?: any } | InjectKey) decorator
参数说明：

提供/注入装饰器,
key可以为string或者symbol类型,
相同点:Provide/ProvideReactive提供的数据,在内部组件使用Inject/InjectReactive都可取到
不同点:

如果提供(ProvideReactive)的值被父组件修改，则子组件可以使用InjectReactive捕获此修改。
// 最外层组件
<template>
  <div class="">
    <H3>ProvideInjectPage页面</H3>
    <div>
      在ProvideInjectPage页面使用Provide,ProvideReactive定义数据,不需要props传递数据
      然后爷爷套父母,父母套儿子,儿子套孙子,最后在孙子组件里面获取ProvideInjectPage
      里面的信息
    </div>
    <hr/>
    <provideGrandpa></provideGrandpa> <!--爷爷组件-->
  </div>
</template>

<script lang="ts">
import {
  Vue, Component, Provide, ProvideReactive,
} from 'vue-property-decorator';
import provideGrandpa from '@/components/ProvideGParentComponent.vue';

@Component({
  components: { provideGrandpa },
})
export default class ProvideInjectPage extends Vue {
  @Provide('foo') foo = 'foo'
  @ProvideReactive('reactiveKey1') reactiveKey1 = 'reactiveKey1'
  @ProvideReactive('reactiveKey2') reactiveKey2 = 'reactiveKey2'

  created() {
    // 此处验证@Provide @ProvideReactive 键值被修改
    this.foo = 'foo111'
    this.reactiveKey1 = 'reactiveKey111'
    this.reactiveKey2 = 'reactiveKey222'
  }
  }
}
</script>

// ...provideGrandpa调用父母组件
<template>
  <div class="hello">
    <ProvideParentComponent></ProvideParentComponent>
  </div>
</template>

// ...ProvideParentComponent调用儿子组件
<template>
  <div class="hello">
    <ProvideSonComponent></ProvideSonComponent>
  </div>
</template>

// ...ProvideSonComponent调用孙子组件
<template>
  <div class="hello">
    <ProvideGSonComponent></ProvideGSonComponent>
  </div>
</template>
 

// 孙子组件<ProvideGSonComponent>,经过多层引用后,在孙子组件使用Inject可以得到最外层组件provide的数据哦
<template>
  <div class="hello">
    <h3>孙子的组件</h3>
    爷爷组件里面的foo:{{ foo }}<br />
    爷爷组件里面的fooReactiveKey1:{{ reactiveKey1 }}<br />
    爷爷组件里面的fooReactiveKey2:{{ reactiveKey2 }}
  </div>
</template>

<script lang="ts">
import {
  Component, Vue, Inject, InjectReactive,
} from 'vue-property-decorator';

@Component
export default class ProvideGSonComponent extends Vue {
  @Inject('foo') foo!: string
  @InjectReactive('reactiveKey1') reactiveKey1!: string
  @InjectReactive('reactiveKey2') reactiveKey2!: string
}
</script>
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39
40
41
42
43
44
45
46
47
48
49
50
51
52
53
54
55
56
57
58
59
60
61
62
63
64
65
66
67
68
69
70
71
72
73
74
75
76
77
78
79
80
81
82
Mixins (在vue-class-component中定义)
在使用Vue进行开发时我们经常要用到混合,结合TypeScript之后我们有两种mixins的方法。

一种是vue-class-component提供的.

//定义要混合的类 mixins.ts
import Vue from 'vue'
import Component from 'vue-class-component'

@Component // 一定要用Component修饰
export default class MyMixins extends Vue {
  value = 'Hello'
}

1
2
3
4
5
6
7
8
9
// 引入
import Component, { mixins } from 'vue-class-component'
import myMixins from './Mixins'

@Component
export default class Project extends mixins(myMixins) {
  created() {
    console.log(this.value)
  }
}
1
2
3
4
5
6
7
8
9
10
等同于

// Mixins.ts
//定义要混合的类 mixins.ts
import Vue from 'vue'
import { Component } from 'vue-property-decorator'

@Component // 一定要用Component修饰
export default class MyMixins extends Vue {
  value = 'Hello'
}

// 引入

import { Component } from 'vue-property-decorator'
import myMixins from './Mixins'

@Component
export default class Project extends myMixins {
  created() {
    console.log(this.value)
  }
}
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
第二种方式是在@Component中混入.

我们改造一下mixins.ts,定义vue/type/vue模块,实现Vue接口

// mixins.ts
import { Vue, Component } from 'vue-property-decorator';


declare module 'vue/types/vue' {
    interface Vue {
        value: string;
    }
}

@Component
export default class myMixins extends Vue {
    value = 'Hello'
}
1
2
3
4
5
6
7
8
9
10
11
12
13
14
混入

import { Vue, Component} from 'vue-property-decorator';
import myMixins from './Mixins';

@Component({
    mixins: [myMixins],
    created(){
        console.log(this.value) // => Hello
    }
})
export default class myComponent extends Vue{}
1
2
3
4
5
6
7
8
9
10
总结: 两种方式不同的是在定义mixins时如果没有定义vue/type/vue模块, 那么在混入的时候就要继承该mixins; 如果定义vue/types/vue模块,在混入时可以在@Component中mixins直接混入。
————————————————
版权声明：本文为CSDN博主「定栓」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/weixin_44116302/article/details/111225763