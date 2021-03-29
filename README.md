#  小程序9宫格抽奖插件

[查看GitHub仓库最新文档(源码)](<https://github.com/flyingdwang/flyingd-fruit-slots>)

` https://github.com/flyingdwang/flyingd-fruit-slots.git`

#### [查看在线演示(支付宝扫码) ](https://github.com/flyingdwang/flyingd-fruit-slots/blob/master/alipay-preview.png?raw=true)



![](<https://raw.githubusercontent.com/flyingdwang/flyingd-fruit-slots/master/alipay-preview.png>)

###  安装

` cnpm install  flyingd-fruit-slots --save`

###  注册

```js
// .json
{
  "usingComponents": {
	"fl-fruit-slots": "flyingd-fruit-slots/fl-fruit-slots"
  }
}
```



###  演示代码

```html

<!-- .axml -->
<fl-fruit-slots 
    prizeList="{{prizeList}}"
    prizeActiveIndex="{{prizeActiveIndex}}"
    disabled="{{disabled}}"
    currentIndex="{{currentIndex}}"
    onStart="onStart"
    onFinish="onFinish"
  />
```

```
// .js

Page({
    data:{
        prizeList:[
            {
                'name': '谢谢参与',
                'icon':'https://zos.alipayobjects.com/rmsportal/dexmbhnbsLRGIZGBqTcA.png'
            },
            {
                'name': '666元红包',
                'icon':'https://zos.alipayobjects.com/rmsportal/nxpXbcNBOmbeIOVCUsuS.png'
            },
            {
                'name': '1元红包',
                'icon':'https://zos.alipayobjects.com/rmsportal/RxQruKQwiQCeYXhvwCfP.png'
            },
            {
                'name': '3元红包',
                'icon':'https://zos.alipayobjects.com/rmsportal/tyMAYvTdjRFOVxqWVhsj.png'
            },
            {
                'name': '谢谢参与',
                'icon':'https://zos.alipayobjects.com/rmsportal/dexmbhnbsLRGIZGBqTcA.png'
            },
            {
                'name': '1元红包',
                'icon':'https://zos.alipayobjects.com/rmsportal/RxQruKQwiQCeYXhvwCfP.png'
            },
            {
                'name': '谢谢参与',
                'icon':'https://zos.alipayobjects.com/rmsportal/dexmbhnbsLRGIZGBqTcA.png'
            },
            {
                'name': '5元红包',
                'icon':'https://zos.alipayobjects.com/rmsportal/qanDEFeGBoiPflYxkhJY.png'
            },
        ],
        prizeActiveIndex: null,
        disabled: false,
        currentIndex: 0,
        tipText: '',
    },
    /** 开始抽奖 */
    onStart(resolve) {
    	/** 有resolve 返回值 则抽奖 否则 不执行  */
    	/** 
        	if(true){
        		resolve(index)
        	}else{
        		return
        	}
        */
        /** 抽奖 */
        this.requestFun().then(res=>{
            console.log(res.index);
            /** 成功回调 */
            resolve(res.index);
            this.setData({
                prizeActiveIndex:res.index,
                tipText: '正在抽奖...'
            })
        })
    },
    /** 抽奖结束回调 */
    onFinish(index, prizeItem) {
        this.setData({
            tipText: `抽奖结果：${prizeItem.name}`
        });
    },
    /** 模拟请求数据 */
    requestFun(){
        return new Promise((resolve, reject)=>{
            let index = Math.floor(Math.random() * 8);
            let { name } = this.data.prizeList[index];
            resolve({name,index});
        })
    },
});

```

###  属性

| 参数             | 说明                                                         | 类型     | 默认值                 | 必填 |
| ---------------- | ------------------------------------------------------------ | -------- | ---------------------- | ---- |
| width            | 组件宽度，单位 rpx。                                         | Number   | 700                    | 否   |
| margin           | 格子间的边距，单位 rpx。                                     | Number   | 20                     | 否   |
| prizeList        | 奖项列表，长度必须为8，须包含 name 和 icon字段。             | Array    | []                     | 是   |
| prizeActiveIndex | 抽奖结果的奖品 索引(0-8)，其值必须位于 prizeList 中。        | Number   | null                   | 是   |
| rollTimes        | 转动圈数。                                                   | Number   | 3                      | 否   |
| currentIndex     | 转动开始的格子下标。                                         | Number   | 0                      | 否   |
| speed            | 转动速度，单位 ms。                                          | Number   | 100                    | 否   |
| class            | 自定义类名。                                                 | String   | -                      | 否   |
| disabled         | 抽奖按钮是否可点击。                                         | Boolean  | false                  | 否   |
| onStart          | 抽奖转动方法; 需要有成功回调 resolve();                      | Function | () => {}               | 是   |
| onFinish         | 转动结束的回调, @params(index: 奖品所在格子下标，prizeItem: 奖品详情参数)。 | Function | (index, prizeItem)=>{} | 否   |

**说明：** 组件中格子自左上角顺时针开始标号，围绕中间按钮，下标从 0 开始递增到 7。当需要组件从左下角的格子为初始位置开始转动，只需要设置 `currentIndex = 6` 即可。

[查看格子顺序详情(图片)](https://gw.alipayobjects.com/zos/skylark-tools/public/files/6b024a982c9fd681d2549561d01e3d48.png)

![](<https://raw.githubusercontent.com/flyingdwang/flyingd-fruit-slots/master/index-info.png>)

