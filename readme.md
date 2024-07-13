
1.安装pm2：
bash <(curl -s https://raw.githubusercontent.com/k0baya/alist_repl/main/serv00/install-pm2.sh)
2.安装vless：
进入所在目录：cd ~/domains/<你的域名目录>
克隆serv00-vless项目（前提是安装了git）：
git clone https://github.com/qwer-search/serv00-vless && mv -f serv00-vless vless && cd vless && rm -f README.md
3.安装依赖：
npm install
4.使用PM2启动，守护vless进程
~/.npm-global/bin/pm2 start app.js --name vless
4.添加vless配置：
vless://37a0bd7c-8b9f-4693-8916-bd1e2da0a817@<域名地址>:<端口>?flow=&security=none&encryption=none&type=ws&host=<域名地址>&path=/&sni=&fp=&pbk=&sid=#%E4%B8%80%E4%BC%91vless%EF%BC%8CTG%E7%BE%A4%EF%BC%9Ahttps://t.me/yxjsjl
5.自动化
新建opt目录,并进入：
mkdir ~/opt
新建 auto-autonew.sh 脚本：
cat > auto-autonew.sh << EOF
#!/bin/bash
 
while true; do
  sshpass -p '密码' ssh -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null -tt 用户名@地址 "exit" &
  sleep 259200  #30天为259200秒
done
EOF
给 auto-autonew.sh添加可执行权限：
chmod +x auto-autonew.sh
使用PM2启动：
~/.npm-global/bin/pm2 start ./auto-autonew.sh
保存快照：
~/.npm-global/bin/pm2 save
6.自动启动
serv00管理页面——Cron jobs选项卡——Add cron job——Command写入：/home/你的用户名/.npm-global/bin/pm2 resurrect
