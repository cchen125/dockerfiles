# 构建镜像
`docker build -t py2-notebook:0.1 .`

# 进入容器，使用`zsh`
`docker run --rm -it py2-minimal:0.1 zsh`

# 启动Notebook
`docker run --name py2-notebook -p 8888:8888 -v "$PWD/notebooks:/root/notebooks" -d py2-notebook:0.1`
