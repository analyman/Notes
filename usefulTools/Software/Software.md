[comment1]: id "rgb(44,44,110)四级标题"
[comment2]: id "rgb(110,110,0)三级标题"
[comment3]: id "rgb(0,110,110)二级标题"
[comment4]: id "rgb(110,0,110)一级标题"

<h1 align="center"><span style="color: rgb(110,0,110)">Software</span></h1>

<h2 align="center"><span style="color:rgb(0,110,110)">Table of contents</span></h2>

* [1.1 VIM](#1.1)
* [1.2 TeX,enscript,gimli](#1.2)
* [1.3 Essential](#1.3)

<h2 name="1.1"><span style="color: rgb(0,110,110)">1.1 VIM</span></h2>

<h3 name=""><span style="color: rgb(110,110,0)">VIM Install</span></h3>

``` bash
# 从源码安装
# Ubuntu
sudo apt build-dep vim-gtk  		# 依赖安装, gtk包
git clone git://github/vim/vim.git	# 源码

./configure --enable-gui=gtk3 --with-features=huge\
--enable-python3interp=yes --enable-pythoninterp=yes\
--enable-rubyinterp=yes --enable-perlinterp=yes\
--enable-luainterp=yes --enable-tclinterp=yes

make
sudo make install
```

<h2 name="1.2"><span style="color: rgb(0,110,110)">1.2 TeX,enscript,gimli</span></h2>

<h3 name=""><span style="color: rgb(110,110,0)">TeX</span></h3>

使用**Texlive**, 从官网或者镜像网站下载**texlive.iso**, 挂载镜像  

* Linux: `install-tl`, 接着`I`继续安装即可
* Windows: 直接使用批处理

<h3 name=""><span style="color: rgb(110,110,0)">enscript</span></h3>

<span style="color:green">converts text to Postscript, HTML or RTF with syntax highlighting</span>  

``` bash
# use apt install it
$ sudo apt install enscript

# basic use
$ enscript -E {highlight language} -p {<output-file>} -i {num-indent(c i l p)} {<source-file>}
```

<h3 name=""><span style="color: rgb(110,110,0)">gimli</span></h3>

``` bash
# Install
$ sudo apt install ruby ruby-dev libz-dev
$ sudo gem install gimli

# Basic use
gemli -file {src-file|src-fold} -outputfilename {<file-name>only use one file} -merge
```

<h2 name="1.3"><span style="color: rgb(0,110,110)">1.3 Essential</span></h2>

<h3 name="1.3.1"><span style="color: rgb(110,110,0)">google chrome</span></h3>

``` bash
# download signing-key
wget https://dl.google.com/linux/linux_signing_key.pub

# use apt-key add the key
sudo apt-key add linux_signing_key.pub

# 加入google-chrome源
# 64bit的系统才可以使用, 32bit系统使用chrominu
sudo sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'

# and you should update before installing chrome
sudo apt update

# installing chrome, three type
sudo apt install google-chrome-stable
sudo apt install google-chrome-beta
sudo apt install google-chrome-unstable
```

<h3 name="1.3.2"><span style="color: rgb(110,110,0)">grub customizer</span></h3>

``` bash
# add ppa
sudo add-apt-repository ppa:danielrichter2007/grub-customizer

# update and install
sudo apt update
sudo apt install grub-customizer
```

<h3 name="1.3.3"><span style="color: rgb(110,110,0)">btsync</span></h3>

**Description:** 用于同步文件

``` bash

# Add source
echo "deb http://linux-packages.resilio.com/resilio-sync/deb resilio-sync non-free" | sudo tee /etc/apt/sources.list.d/resilio-sync.list

# Add key
wget -qO - https://linux-packages.resilio.com/resilio-sync/key.asc | sudo apt-key add -

# update
sudo apt update

# Install
sudo apt install resilio-sync

# 使用, 启动
sudo systemctl start resilio-sync
sudo systemctl enable resilio-sync        # 开机自启
google-chrome 127.0.0.1:8888        # 浏览器打开 127.0.0.1:8888
```