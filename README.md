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
