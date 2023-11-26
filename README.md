# 1、参考

- https://github.com/BioYue/WeChatLogin

# 2、使用教程

## （0）整个流程更详细可以查看小弟的博客

- https://blog.csdn.net/caip12999203000/article/details/134635055?spm=1001.2014.3001.5502

## （1）Django

> 下面要修改的信息在网址（申请得到）：https://mp.weixin.qq.com/debug/cgi-bin/sandboxinfo?action=showinfo&t=sandbox/index
>
> 修改的位置：wx_django\app\views.py

- 修改 appID 和 appSecret 

```
appID = "wx8ac3xxx9236efe2a"
appSecret = "131b8d9d8xxx74afb751ce6b2"
```

- 修改token（即yue_token）

```
class WeChatSignature(APIView):
    def get(self, request):
        ...
        yue_token = 'yueyue'
        ...

    def post(self, request):
   	 	...
```

- 可以获取小程序的独有id（OpenId）

```
	# 这里的from_user_name就是OpenID
	from_user_name = xml_data.find('FromUserName').text 
```

- 运行Django命令

```
python manage.py runserver 0.0.0.0:80
```

## （2）Vue2

> 修改的位置：wx_vue\src\components\HelloWorld.vue

- 修改发送发送的地址

> https://api.xxxx.pro   +  /api/weChatLogin   （前面这个是跑django的ip，需要公网）
>
> 'https://api.xxxx.pro/api/verifyLogin?scene=' + this.scene

```

  methods: {
    getQrUrl() {
      axios.get('https://api.xxxx.pro/api/weChatLogin').then((res) => {
       ....
      })
    },
    loginPoll() {
      axios.get('https://api.xxxx.pro/api/verifyLogin?scene=' + this.scene).then((res) => {
       	...
        }
      })
    }
}
```

- 运行vue2

```

# 安装相关依赖
npm install
 
# 运行服务
npm run serve
```

# 3、显示结果

![show1](./show_img/show1.png)