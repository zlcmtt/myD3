<template>
  <svg id="mySvg"></svg>
</template>

<script>
import * as d3 from 'd3'
export default {
  name: 'HelloWorld',
  data () {
    return {
      mySvg: null
    }
  },
  methods: {
    // 绘制箭头
    arrowMarker () {
      const defs = this.mySvg.append('defs')
      const arrowMarker = defs.append('marker')
        .attr('id', 'arrow')
        .attr('markerUnits', 'strokeWidth')
        .attr('markerWidth', 5)
        .attr('markerHeight', 5)
        .attr('viewBox', '-5 -5 10 10')
        .attr('refX', 20)
        .attr('refY', 0)
        .attr('stroke-width', 1)// 箭头宽度
        .attr('orient', 'auto')
      const arrowPath2 = 'M 0,0 m 5,5 L -5,0 L 5,-5 Z'
      const arrowPath1 = 'M 0,0 m -5,-5 L 5,0 L -5,5 Z'
      arrowMarker.append('path')
        .attr('d', arrowPath1)
        .attr('fill', '#4890FF')
      const arrowMarkers = defs.append('marker')
        .attr('id', 'arrows')
        .attr('markerUnits', 'strokeWidth')
        .attr('markerWidth', 5)
        .attr('markerHeight', 5)
        .attr('viewBox', '-5 -5 10 10')
        .attr('refX', -150)
        .attr('refY', 0)
        .attr('stroke-width', 1)// 箭头宽度
        .attr('orient', 'auto')
      arrowMarkers.append('path')
        .attr('d', arrowPath2)
        .attr('fill', '#FBA93A')
    },
    // 绘制文本
    textMarker (ele, text, y) {
      ele
        .append('text')
        .text(text)
        .attr('text-anchor', 'middle')
        .attr('fill', '#fff')
        .attr('stroke-width', 1)
        .attr('font-size', 24)
        .attr('font-weight', 900)
        .attr('y', y)
    }
  },
  mounted () {
    const mySvg = d3.select('#mySvg')
    this.mySvg = mySvg
    this.arrowMarker()
    const element = mySvg.node()
    const width = element.getBoundingClientRect().width
    const height = element.getBoundingClientRect().height
    const lineG = mySvg.append('g')
    const dataset = [
      { name: 'zs', obj1: 1, obj2: 2 },
      { name: 'zs', obj1: 3, obj2: 21 },
      { name: 'zs', obj1: 8, obj2: 9 },
      { name: 'zs', obj1: 1, obj2: 2 },
      { name: 'zs', obj1: 3, obj2: 21 },
      { name: 'zs', obj1: 8, obj2: 9 }
    ]
    lineG.selectAll('line')
      .data(dataset)
      .enter()
      .append('line')
      .attr('x1', width / 2)
      .attr('x2', width - 20)
      .attr('y1', height / 2)
      .attr('y2', height / 2)
      .attr('stroke-width', 2)
      .attr('stroke', '#D9D9D9')
      .attr('transform-origin', '50% 50%')
      .attr('transform', function (d, i) {
        return `rotate(${i * 360 / dataset.length})`
      })
      .attr('marker-end', 'url(#arrow)')
      .attr('marker-start', 'url(#arrows)')
    const circleG = mySvg.append('g').attr('transform', `translate(${width / 2},${height / 2})`)
    circleG
      .append('circle')
      .attr('id', 'myCircle')
      .attr('fill', '#21CCA5')
      .attr('r', '100px')
      .attr('stroke', '#e4fafb')
      .attr('stroke-width', 40)
    // 绘制文本
    this.textMarker(circleG, 586, 0)
    this.textMarker(circleG, '数据中心', 30)
  }
}
</script>

<style lang="less">
  svg{
    height: 600px;
    width: 600px;
    margin: auto;
    padding: 0;
  }
</style>
