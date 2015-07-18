---
layout: post
title: Echarts
categories: [技术]
tags: [Echarts]
icon: code
---
test

<!-- 为ECharts准备一个具备大小（宽高）的Dom -->
<div id="barMain" style="height:400px"></div>

test

<div id="lineMain" style="height:400px"></div>

test2

<div id="lineMain2" style="height:400px"></div>

<!-- -->
<!-- ECharts单文件引入 -->
<script src="http://echarts.baidu.com/build/dist/echarts.js"></script>
<script type="text/javascript">
// 路径配置
		require.config(
				{
						paths: {
								echarts: 'http://echarts.baidu.com/build/dist'
            }
        }
		);

    require(
    		[
        　　'echarts',
        　　'echarts/chart/bar', 
        　　'echarts/chart/line'
        ],
        drawEcharts
    );

    function drawEcharts(ec){
        drawBar(ec);
        drawLine(ec);
        drawLine2(ec);
    }
    
    function drawBar(ec){
        var myBarChart = ec.init(document.getElementById('barMain')); 
        option = {
						title : {
                text: "各渠道销量"
						},
            tooltip : {
                trigger: 'axis'
            },
            legend: {
                data:['邮件营销','联盟广告','视频广告','直接访问','搜索引擎']
            },
            calculable : true,
            xAxis : [
                {
                    type : 'category',
                    boundaryGap : false,
                    data : ['周一','周二','周三','周四','周五','周六','周日']
                }
            ],
            yAxis : [
                {
                    type : 'value'
                }
            ],
            series : [
                {
                    name:'邮件营销',
                    type:'line',
                    stack: '总量',
                    data:[120, 132, 101, 134, 90, 230, 210]
                },
                {
                    name:'联盟广告',
                    type:'line',
                    stack: '总量',
                    data:[220, 182, 191, 234, 290, 330, 310]
                },
                {
                    name:'视频广告',
                    type:'line',
                    stack: '总量',
                    data:[150, 232, 201, 154, 190, 330, 410]
                },
                {
                    name:'直接访问',
                    type:'line',
                    stack: '总量',
                    data:[320, 332, 301, 334, 390, 330, 320]
                },
                {
                    name:'搜索引擎',
                    type:'line',
                    stack: '总量',
                    data:[820, 932, 901, 934, 1290, 1330, 1320]
                }
            ]
        };    
        myBarChart.setOption(option,true); //当setOption第二个参数为true时，会阻止数据合并
    }

    function drawLine(ec){
		    var myLineChart = ec.init(document.getElementById('lineMain')); 
        var option2 = {
		        title : {
		    				text: "一周气温变化"
		    		},
		    		tooltip : {
		    				trigger: 'axis'
		    		},
		    		legend: {
		    				data:['最高气温','最低气温']
		    		},
		    		calculable : true,
		    		xAxis : [{
		    		    type : 'category',
		    				boundaryGap : false,
		    				data : ['周一','周二','周三','周四','周五','周六','周日']
		    		}],
		    		yAxis : [{
		    				type : 'value',
		    				axisLabel : {
		    				    formatter: '{value} °C'
		    				}
		    		}],
		    		series : [
		    		    {
		    				    name:'最高气温',
		    				    type:'line',
		    				    data:[11, 11, 15, 13, 12, 13, 10],
		    				    markPoint : {
		    				    		data : [
		    				    				{type : 'max', name: '最大值'},
		    				    				{type : 'min', name: '最小值'}
		    				    		]
		    				    },
		    				    markLine : {
		    				    		data : [
　　    　　　　            {type : 'average', name: '平均值'}
　　    　　            ]
                    }
                },

		    				{
                    name:'最低气温',
		    	         	type:'line',
		    	         	data:[1, -2, 2, 5, 3, 2, 0],
		    	         	markPoint : {
		    	         			data : [
		    	         					{name : '周最低', value : -2, xAxis: 1, yAxis: -1.5}
		    	         			]
		    	     	    },
                    markLine : {
		    				        data : [
　　    　　　　            {type : 'average', name : '平均值'}
　　    　　            ]
                    },
                },
            ]
        };
        myLineChart.setOption(option2,true); 
    }

    function drawLine2(ec){
		    var myLineChart2 = ec.init(document.getElementById('lineMain2')); 
        var option3 = {
		        title : {
		    				text: "一周气温变化"
		    		},
		    		tooltip : {
		    				trigger: 'axis'
		    		},
		    		legend: {
		    				data:['最高气温','最低气温']
		    		},
		    		calculable : true,
		    		xAxis : [{
		    		    type : 'category',
		    				boundaryGap : false,
		    				data : ['周一','周二','周三','周四','周五','周六','周日']
		    		}],
		    		yAxis : [{
		    				type : 'value',
		    				axisLabel : {
		    				    formatter: '{value} °C'
		    				}
		    		}],
		    		series : [
		    		    {
		    				    name:'最高气温',
		    				    type:'line',
		    				    data:[11, 11, 15, 13, 12, 13, 10],
		    				    markPoint : {
		    				    		data : [
		    				    				{type : 'max', name: '最大值'},
		    				    				{type : 'min', name: '最小值'}
		    				    		]
		    				    },
		    				    markLine : {
		    				    		data : [
　　    　　　　            {type : 'average', name: '平均值'}
　　    　　            ]
                    }
                },

		    				{
                    name:'最低气温',
		    	         	type:'line',
		    	         	data:[1, -2, 2, 5, 3, 2, 0],
		    	         	markPoint : {
		    	         			data : [
		    	         					{name : '周最低', value : -2, xAxis: 1, yAxis: -1.5}
		    	         			]
		    	     	    },
                    markLine : {
		    				        data : [
　　    　　　　            {type : 'average', name : '平均值'}
　　    　　            ]
                    },
                },
            ]
				}
        myLineChart2.setOption(option3,true); 
    };
</script>
<!-- end -->
