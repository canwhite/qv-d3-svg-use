<template>
  <div class="hello">
    <p>svg基础示例-折线图</p>
    <!-- 矩形
    圆形
    椭圆
    线段
    折线
    多边形
    另外，还有一种比较特殊，也是功能最强的元素：

    路径  -->
    <!-- 
    Date |Amount
    -----|------
    2014-01-01 | $10
    2014-02-01 | $20
    2014-03-01 | $40
    2014-04-01 | $80 -->
    <p> 
      <svg width = "350" height = "160"> 
        <g class ="layer" transform="translate(60,10)" >
            <!-- 先画点，半径和坐标，默认是黑色 -->
            <circle r="5" cx="0"   cy="105" />
            <circle r="5" cx="90"  cy="90"  />
            <circle r="5" cx="180" cy="60"  />
            <circle r="5" cx="270" cy="0"   />

            <!-- 纵向坐标 -->
            <g class = "y axis">
              <line style="stroke:#333;stroke-width:3" x1="0" y1="0" x2="0" y2="120" />
              <!-- dy属性指示在元素或其内容的位置上沿着y轴的移位。究竟移动什么取决于设置该属性的元素 -->
              <text x="-40" y="105" dy="5">$10</text>
              <text x="-40" y="0"   dy="5">$80</text>
            </g>


            <g class="x axis" transform="translate(0, 120)">
              <line style="stroke:#333;stroke-width:3" x1="0" y1="0" x2="270" y2="0" />
              <text x="-30"   y="20">January 2014</text>
              <text x="240" y="20">April</text>
            </g>
        </g>
      </svg>
    </p>

  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }
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
