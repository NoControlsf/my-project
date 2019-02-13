<style xmlns:v-bind="http://www.w3.org/1999/xhtml">
  .class1{
    background: #444;
    color: #eee;
  }
  table {
    border: 1px solid black;
  }
  table {
    width: 100%;
  }

  th {
    height: 50px;
  }
  th, td {
    border-bottom: 1px solid #ddd;
  }
</style>

<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h1>site : {{site}}</h1>
    <h1>url : {{url}}</h1>
    <h1>{{details()}}</h1>
    <div v-html="alexa"></div>
    <label for="r1">修改颜色</label><input type="checkbox" v-model="use" id="r1">
    <br><br>
    <div v-bind:class="{'class1': use}">
      v-bind:class 指令
    </div>

    {{5+5}}<br>
    {{ ok ? 'YES' : 'NO' }}<br>
    {{ message.split('').reverse().join('') }}
    <div v-bind:id="'list-' + id">菜鸟教程</div>

    <p v-if="seen">现在你看到我了</p>

    <pre><a v-bind:href="url">菜鸟教程</a></pre>
    <a :href="url">菜鸟教程(v-bind简化)</a>

    <p>{{ message1 }}</p>
    <button v-on:click="reverseMessage">反转字符串</button>


    <a @click="reverseMessage">反转字符串(v-on简化)</a>


    <ol>
      <li v-for="site in sites">
        {{ site.name }}
      </li>
    </ol>

    <ul>
      <template v-for="site in sites">
        <li>{{ site.name }}</li>
        <li>--------------</li>
      </template>
    </ul>


    <ul>
      <li v-for="value in object">
        {{ value }}
      </li>
    </ul>

    <ul>
      <li v-for="(value, key) in object">
        {{ key }} : {{ value }}
      </li>
    </ul>

    <ul>
      <li v-for="(value, key, index) in object">
        {{ index }}. {{ key }} : {{ value }}
      </li>
    </ul>

    <ul>
      <li v-for="n in 10">
        {{ n }}
      </li>
    </ul>

    <table>
      <tr>
        <th>序号</th>
        <th>商品名称</th>
        <th>商品价格</th>
        <th>购买数量</th>
        <th>操作</th>
      </tr>
      <tr v-for="iphone in Ip_Json">
        <td>{{ iphone.id }}</td>
        <td>{{ iphone.name }}</td>
        <td>{{ iphone.price }}</td>
        <td>
          <button v-bind:disabled="iphone.count === 0" v-on:click="iphone.count-=1">-</button>
          {{ iphone.count }}
          <button v-on:click="iphone.count+=1">+</button>
        </td>
        <td>
          <button v-on:click="iphone.count=0">移除</button>
        </td>
      </tr>
    </table>
    总价：${{totalPrice()}}


    <button v-on:click="counter += 1">增加 1</button>
    <p>这个按钮被点击了 {{ counter }} 次。</p>

    <button v-on:click="say('hi')">Say hi</button>
    <button v-on:click="say('what')">Say what</button>

    <p>input 元素：</p>
    <input v-model="message" placeholder="编辑我……">
    <p>消息是: {{ message }}</p>

    <p>textarea 元素：</p>
    <textarea v-model="message2" placeholder="多行文本输入……"></textarea>
    <p style="white-space: pre">{{ message2 }}</p>

    <p>单个复选框：</p>
    <input type="checkbox" id="checkbox" v-model="checked">
    <label for="checkbox">{{ checked }}</label>

    <p>多个复选框：</p>
    <input type="checkbox" id="runoob" value="Runoob" v-model="checkedNames">
    <label for="runoob">Runoob</label>
    <input type="checkbox" id="google" value="Google" v-model="checkedNames">
    <label for="google">Google</label>
    <input type="checkbox" id="taobao" value="Taobao" v-model="checkedNames">
    <label for="taobao">taobao</label>
    <br>
    <span>选择的值为: {{ checkedNames }}</span>


    <select v-model="selected" name="fruit">
      <option value="">选择一个网站</option>
      <option value="www.runoob.com">Runoob</option>
      <option value="www.google.com">Google</option>
    </select>

    <div id="output">
      选择的网站是: {{selected}}
    </div>

  </div>
</template>

<script>

export default {
  name: 'HelloWorld',
  methods: {
    details: function() {
      return  this.site + " - 学的不仅是技术，更是梦想！";
    },
    totalPrice : function(){
      var totalP = 0;
      for (var i = 0,len = this.Ip_Json.length;i<len;i++) {
        totalP+=this.Ip_Json[i].price*this.Ip_Json[i].count;
      }
      return totalP;
    },
    say: function (message) {
      alert(message)
    },

    reverseMessage: function () {
      this.message1 = this.message1.split('').reverse().join('')
    }
  },
  data () {
    return {
      site: "菜鸟教程",
      url: "http://www.runoob.com",
      alexa: "<a href='#'>百度</a>",

      use: false,

      ok: true,
      message: 'RUNOOB',
      id : 1,

      seen: true,

      message1: 'Runoob!',

      sites: [
        { name: 'Runoob' },
        { name: 'Google' },
        { name: 'Taobao' }
      ],

      object: {
        name: '菜鸟教程',
        url: 'http://www.runoob.com',
        slogan: '学的不仅是技术，更是梦想！'
      },

      Ip_Json: [{
        id: 1,
        name: 'iphone 8',
        price: 5099,
        count: 1
      },
        {
          id: 2,
          name: 'iphone xs',
          price: 8699,
          count: 1
        },
        {
          id: 3,
          name: 'iphone xr',
          price: 6499,
          count: 1
        }],
      counter: 0,

      checked : false,
      checkedNames: [],

      selected: '',

      msg: 'Welcome to My App'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
