## 解决unraid反代后无法使用虚拟机VNC的问题
### 环境：unraid6.11.5 反代使用NPM
#### 1.登录NPM，打开unraid反代的域名，点击编辑（Edit）
![](index_files/1678790153579-brn.png)


#### 2.选择Advanced标签页，将以下内容填入
![](index_files/1678790386331-qmj.png)

        location / {

            proxy_pass http://192.168.1.3:80;  //注意此行ip以及端口替换为你的unraid的本地IP和端口

            proxy_http_version 1.1;

            proxy_set_header Upgrade $http_upgrade;

            proxy_set_header Connection "upgrade";

            proxy_set_header Host $http_host;

            proxy_set_header Access-Control-Allow-Origin 192.168.1.3; //注意此行ip以及端口替换为你的unraid的本地IP

            proxy_set_header X-Real-IP $remote_addr;

            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

            proxy_set_header X-NginX-Proxy true;

        }
修改完成后点击Save保存。至此，工作全部完成，可以试试使用反代后的页面VNC连接虚拟机了。
