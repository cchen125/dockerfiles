# Base image
FROM ubuntu:18.04

# mirrors.163.com
RUN echo "deb http://mirrors.163.com/ubuntu/ bionic main restricted universe multiverse" > /etc/apt/sources.list \
    && echo "deb http://mirrors.163.com/ubuntu/ bionic-security main restricted universe multiverse" >> /etc/apt/sources.list \
    && echo "deb http://mirrors.163.com/ubuntu/ bionic-updates main restricted universe multiverse" >> /etc/apt/sources.list \
    && echo "deb http://mirrors.163.com/ubuntu/ bionic-proposed main restricted universe multiverse" >> /etc/apt/sources.list \
    && echo "deb http://mirrors.163.com/ubuntu/ bionic-backports main restricted universe multiverse" >> /etc/apt/sources.list \
    && echo "deb-src http://mirrors.163.com/ubuntu/ bionic main restricted universe multiverse" >> /etc/apt/sources.list \
    && echo "deb-src http://mirrors.163.com/ubuntu/ bionic-security main restricted universe multiverse" >> /etc/apt/sources.list \
    && echo "deb-src http://mirrors.163.com/ubuntu/ bionic-updates main restricted universe multiverse" >> /etc/apt/sources.list \
    && echo "deb-src http://mirrors.163.com/ubuntu/ bionic-proposed main restricted universe multiverse" >> /etc/apt/sources.list \
    && echo "deb-src http://mirrors.163.com/ubuntu/ bionic-backports main restricted universe multiverse" >> /etc/apt/sources.list

# Updating Ubuntu packages
RUN apt-get update && apt-get upgrade -y

# Install required packages
RUN apt-get install -y wget bzip2 zsh git vim

# Install zsh
RUN git clone https://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh \
    && cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc \
    && chsh -s /bin/zsh

# Install anaconda
RUN wget https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/Anaconda3-5.3.1-Linux-x86_64.sh \
    && bash Anaconda3-5.3.1-Linux-x86_64.sh -b \
    && rm Anaconda3-5.3.1-Linux-x86_64.sh

# Config python path
ENV PATH /root/anaconda3/bin:$PATH

# Config pip
# Install xgboost (from tuna mirror)
RUN pip install pip -U \
    && pip install -i https://pypi.tuna.tsinghua.edu.cn/simple xgboost \
    && pip install -i https://pypi.tuna.tsinghua.edu.cn/simple lightgbm

# Config access to Jupyter
# passwd: macbook1234
RUN mkdir /root/notebooks
RUN jupyter notebook --generate-config --allow-root
RUN echo "c.NotebookApp.password = u'sha1:2231e194927e:480c03780596a11dc50ff9b1eeb1cb92edcadcda'" >> /root/.jupyter/jupyter_notebook_config.py

# Jupyter listens port: 8888
EXPOSE 8888

# Set working directory
WORKDIR /root/notebooks

# Run Jupytewr notebook as Docker main process
CMD ["jupyter", "notebook", "--allow-root", "--notebook-dir=/root/notebooks", "--ip='*'", "--port=8888", "--no-browser"]
