## 管理包
```cmd
# 确认conda已安装: conda --version
# 更新conda版本: conda update conda
# 查询conda信息: conda info
# 升级anaconda: conda update anaconda
1. 安装包：
conda install package_name
2. 同时安装多个包：
conda install numpy scipy pandas
3. 安装指定版本
conda install numpy=1.10
4. 移除包
conda remove package_name
5. 更新包
conda update package_name
5. 更新所有包
conda update --all
6. 查看所有已经安装的包：
conda list
7. 查询某个包，也可以进行模糊查询：
conda search search_key_word
```
## 环境管理
```cmd
1. 创建一个新环境：
conda create -n env_name list of packages
其中 -n 代表name，env_name是需要创建的环境名称，list of packages 则是列出在新环境中同时需要安装的工具包。
例如：
conda create -n py3 python=3.7 pandas
或者复制一个已有的环境
conda create --name new_env --clone old_env
2. 进入名为env_name的环境：
source activate env_name
3. 退出当前环境：
source deactivate
在Windows系统中，使用activate env_name和deactivate来进入和退出某个环境。
4. 删除名为env_name的环境：
conda env remove -n env_name
5. 显示所有的环境：
conda env list
6. 查看环境信息
conda info --envs
7. 当分享代码给别人的时候，同时也需要将运行环境分享，执行如下命令可以将当前环境下的package信息存入名为environment的YAML文件中。
conda env export --name env_name > environment.yaml
同样，当执行他人的代码时，也需要配置相应的环境。这时你可以用对方分享的YAML文件来创建一摸一样的运行环境。
conda env create -f environment.yaml
```