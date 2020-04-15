# tabar 递归多级菜单栏
###  tabar
```
  tabar 组件
```
| 参数 | 说明 | 类型 |  默认值 | 是否必须 |
| --- | --- | --- | --- | --- | 
|menu-data|绑定数据|Array||是| 
|width|宽度|width|300|否|
|selectTabar|监听选中|function| |否|

``` 
     //数据形式
	 navigation: [
		{
			id: 1,
			name: '第一层',
			children: [
				{
					name: '第二层',
					id: 11
				},
				{
					name: '第二层',
					id: 12
				},
				{
					name: '第二层',
					id: 13
				}
			]
		},
		{
			id: 2,
			name: '第二层',
			children: [
				{
					name: '第二层',
					id: 21,
				},
				{
					name: '第二层',
					id: 22,
					children: [
						{
							name: '第三层',
							id: 221,
						},
						{
							name: '第三层',
							id: 222,
						}
					]
				}
			]
		}
	 ]
```
