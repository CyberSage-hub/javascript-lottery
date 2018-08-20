http://jssdk.demo.qiniu.io/#
客户端请求后，直接返回给客户端，服务器端继续执行
```php
 27         public function index()
 28         {
 29                 log_message('error','sssssssss');
 30                 if(function_exists('fastcgi_finish_request')){
 31                     // 刷新buffer
 32                     ob_flush();
 33                     flush();
 34                     // 断开浏览器连接
 35 //                  die(json_encode(array('code'=>1,'msg'=>'success'),TRUE));
 36                     fastcgi_finish_request();
 37                    // die(json_encode(array('code'=>1,'msg'=>'success'),TRUE));
 38                 }
 39 
 40                 // 这里是模拟你的耗时逻辑
 41                 sleep(6);
 42                 log_message('error','ssssssssqqqqqqqqqqqqqqqqqqqqqqqs');
 43                 //$this->load->view('welcome_message');
 44 
 45         }
```

javascript抽奖概率算法
```javascript
        var g = g || {};
        //奖品概率数组
        g.data = [
            {'name':'PSV2000','g':1,'deg':10},
            {'name':'PSV2001','g':2,'deg':100},
            {'name':'PSV2002','g':3,'deg':160},
            {'name':'PSV2003','g':4,'deg':230},
            {'name':'PSV2004','g':5,'deg':300},
        ];
        
        //* 抽奖概率
        var probably = function (prop){
            var res = '';
            if(Array.isArray(prop)){
                var sum = now = 0;
                // 计算概率总和
                prop.forEach(function(v,k,array){
                    sum += v.g;
                });
                var x = 1;
                var y = sum;

                var rand = parseInt(Math.random() * (x - y + 1) + y);
                //概率数组循环
                var len = prop.length;
                for(var j=0;j<len;j++){
                    now += prop[j].g;
                    if (rand <= now) {
                        res = j;
                        break;
                    }
                }
            }else{
                res = '';
            }
            return res;
        }
        
        //调用
        var result = probably(g.data);
        console.log(g.data[result]);        
```
