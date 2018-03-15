

配置tensorflow环境，并在IPython notebook中引入tensorflow

1. 安装pyenv,管理多个版本的python；
2. 安装tensorflow官网的步骤，选择Installing tensorflow with anaconda;
3. activate tensorflow;
4. 在tensorflow环境下，安装IPython和jupyter；


通过docker 安装tensorflow机器学习所需环境：
docker run -it -p "127.0.0.1:8081:8080" -v "${HOME}:/content" \
    gcr.io/cloud-datalab/datalab:local-20170224

    