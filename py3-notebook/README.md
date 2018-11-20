# 构建镜像
`docker build -t py3-notebook .`

# 进入容器，使用`zsh`
`docker run --rm -it py3-notebook zsh`

# 启动Notebook
`docker run --name py3-notebook -p 8888:8888 -v "$PWD/notebooks:/root/notebooks" -d py3-notebook`
