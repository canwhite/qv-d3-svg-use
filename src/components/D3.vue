<template>
  <div class="hello" id = "d3-use">
    <p class="mp" id="p1">d3基础示例</p>
    <!-- 做一些基础操作 -->
    <p class="mp" id = "p2"></p>
    <svg width="1040" height="500" id="mainsvg" class="svgs"></svg> 
  </div>
</template>

<script> 
import * as d3 from "d3"
export default {
  name: 'HelloWorld',
  props: {
    msg: String,
  },
  mounted() {
    //一些基础操作
    this.initAction(); //v.x通用
    this.simpleCharts();  //v4

  },

  updated() {
     //更新的时候重新画
    //  var svg =  d3.select("svg");
    //  svg.remove()
  },

  methods: {
    simpleCharts(){
      //html提供两种强有力的画布，svg和canvas
      //d3没有明文规定一定要使用svg绘图，但是d3提供了众多svg图形的生成器
      //它们都是只支持svg的，因此建议使用svg画布

      var width  = 300;//画布的宽度
      var height = 300;//画布的高度

      var svg = d3.select("body")
                .append("svg")
                .attr("width",width)
                .attr("height",height);
      //然后在svg上画矩形

      //scale比例尺
      // 在数学中，x 的范围被称为定义域，y 的范围被称为值域。
      // D3 中的比例尺，也有定义域和值域，分别被称为 domain 和 range。
      // 开发者需要指定 domain 和 range 的范围，如此即可得到一个计算关系。
      // 这里主要介绍两种比例尺，线性比例尺和序数比例尺
      
      
      //固定宽度
      //var dataset = [ 250 , 210 , 170 , 130 , 90 ]; 
      
      //线性宽度
      var dataset = [1.2, 2.3, 0.9, 1.5, 3.3];
      var max = d3.max(dataset);
      /*
        //线性比例尺，能将一个连续的区间，映射到另一区间。要解决柱形图宽度的问题，就需要线性比例尺。
        //将dataset里边的值值，根据最大最小，映射到0～300
        线性比例尺
        d3.scale.linear() 返回一个线性比例尺。V4改为了scaleLinear
        domain() 和 range() 分别设定比例尺的定义域和值域。
        定义域来自于自己的数据，值域来自于自己确定的范围

      */
      /* 
        如果离散对应我们可以使用序数比例尺
        var index = [0, 1, 2, 3, 4];//序数，实际上就是下标
        var color = ["red", "blue", "green", "yellow", "black"]; 
        var ordinal = d3.scale.ordinal()//V4之后的版本sh使用  d3.scaleOrdinal() .domain(index) .range(color);建立一个序数比例尺
        .domain(index)
        .range(color);

        ordinal(0); //返回 red
        ordinal(2); //返回 green
        ordinal(4); //返回 black
      */
      var linear = d3.scaleLinear() //返回线性比例尺，并且返回值可以作为函数使用
        .domain([0, max])
        .range([0, 300]);

      /* linear(0.9);    //返回 0
      linear(2.3);    //返回 175
      linear(3.3);    //返回 300 */



      var rectHeight = 25;   //每个矩形所占的像素高度(包括空白)
      svg.selectAll("rect")
        .data(dataset)
        .enter()//进入
        .append("rect")//添加足够数量的react
        .attr("x",100)
        .attr("y",function(d,i){
            return i * rectHeight;
        })
        .attr("width",function(d){
           return linear(d);   //在这里用比例尺
        })
        .attr("height",rectHeight-2)
        .attr("fill","steelblue");//给矩形设置颜色
      

       //添加坐标轴，这里是x轴 
       var xAxis = d3.axisBottom(linear).ticks(7);//设置刻度数目//定义一个axis，由bottom可知，是朝下的
       svg.append("g").attr("transform","translate("+100+","+(dataset.length*rectHeight)+")").call(xAxis);

    },

    //初始的一些增删改查工作
    initAction(){

      //获取节点,也可以通过id获取
      var body = d3.select("#d3-use");
      console.log(body)

      //可以链式使用
      var ps = body.selectAll("p");
      console.log(ps);

      //将一个字符串和两个p绑定
      let str = "China";
      ps.datum(str).text(function(item, index){
        if(index ==1){
          return "第 "+ index + " 个元素绑定的数据是 " + item;
        }
      });

      //data常用，相当于数组赋值
      var dataset = ["I like dog","I like cat","I like snake"];

      //两个p标签都变化了，第三个因为没有直接越过去了
      ps.data(dataset).text(function(d){
            return d;
      });

      //直接选择p返回的是第一个元素
      let p1 = body.select("p");
      //然后给它设置属性
      p1.style("color","red");

      //取第二个元素，这个可以直接用id
      var p2 = body.select("#p2");
      p2.style("color","green");

      //选择后两个元素,用.获取
      var mp = body.selectAll(".mp");
      mp.style("color","purple");

      //append在选择集末尾插入元素
      body.append("p").text("append an element");

      //insert在某个元素前插入元素,可以通过id识别元素
      body.insert("p","#p2").text("insert an element");

      //删除元素-删除元素比较简单，直接通过id删除就ok
      var dp = body.select("#p1");
      dp.remove();


    }
  },

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
