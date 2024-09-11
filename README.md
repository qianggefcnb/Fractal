# CAT Protocol 铸造教程
1、
    r、docker-compose、node.js
   1-0 必须安装DOCKER、docker-compose、node.js
      自行百度，很简单
   
   1-1 （以下操作在一个窗口）
    # 更新软件包列表
    sudo apt update

    # 升级已安装的软件包
    sudo apt upgrade -y

    # 安装所需的软件包
    sudo apt install make gcc chrony curl build-essential pkg-config libssl-dev git wget jq -y

    # 拉取 fractald 库，进入目录
    git clone https://github.com/CATProtocol/cat-token-box
    cd cat-token-box

    # 编译
    sudo yarn install && sudo yarn build

    # 运行Fractal 全节点 docker 容器
    cd ./packages/tracker/
    sudo docker-compose up （如果你想后台运行运行时使用 sudo docker-compose up -d )

    1-2 新开命令窗口，启动CAT Protocol 索引器，索引器需要同步100%，sudo docker run  \我没有加 -d ，让运行显示在窗口内
    cd cat-token-box
    sudo docker build -t tracker:latest .
    sudo docker run  \
    --name tracker \
    --add-host="host.docker.internal:host-gateway" \
    -e DATABASE_HOST="host.docker.internal" \
    -e RPC_HOST="host.docker.internal" \
    -p 3000:3000 \
    tracker:latest

     1-3新开窗口创建钱包
     cd cat-token-box/packages/cli
     sudo yarn cli wallet create
     （注意保存出现的助记词）
     1-4 开始mint   （其中 --fee-rate 90 可以自定义GAS） 
     sudo yarn cli mint -i 45ee725c2c5993b3e4d308842d87e973bf1951f5f7a804b21e4dd964ecd12d6b_0 5 --fee-rate 800

    
