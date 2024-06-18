参考：[Installing SageMath 10.3 in Ubuntu](https://sagemanifolds.obspm.fr/install_ubuntu.html)
注意按照本文安装会在您的（虚拟）机器中编译一整个Python且占用巨大的空间（几个G），如果您是Arch Linux，您可以选择使用pacman包管理器进行安装。
### 在Ubuntu 22.04中安装SageMath 9.5：
SageMath 9.5作为系统包提供在Ubuntu 22.04中；要安装它，只需运行以下命令：
```bash
sudo apt install sagemath-jupyter
```
然而，目前版本9.5已经相当老了。而且，它不允许安装额外的包。如果您想安装10.3版本，请先移除已安装的系统包sagemath，然后按照以下说明进行操作：
### 在Ubuntu 20.04或22.04中安装SageMath 10.3：
系统包提供的SageMath版本对于Ubuntu 20.04是9.0，对于Ubuntu 22.04是9.5。然而，在Ubuntu 20.04或22.04中从源代码构建SageMath 10.3非常简单。<br />首先，安装依赖项，即构建SageMath所需的Ubuntu软件包：只需打开终端并输入以下单行命令（很长）：
```bash
sudo apt install bc binutils bzip2 ca-certificates cliquer cmake curl ecl eclib-tools fflas-ffpack flintqs g++ gengetopt gfan gfortran git glpk-utils gmp-ecm lcalc libatomic-ops-dev libboost-dev libbraiding-dev libbrial-dev libbrial-groebner-dev libbz2-dev libcdd-dev libcdd-tools libcliquer-dev libcurl4-openssl-dev libec-dev libecm-dev libffi-dev libflint-arb-dev libflint-dev libfreetype6-dev libgc-dev libgd-dev libgf2x-dev libgiac-dev libgivaro-dev libglpk-dev libgmp-dev libgsl-dev libhomfly-dev libiml-dev liblfunction-dev liblrcalc-dev liblzma-dev libm4rie-dev libmpc-dev libmpfi-dev libmpfr-dev libncurses5-dev libntl-dev libopenblas-dev libpari-dev libpcre3-dev libplanarity-dev libppl-dev libprimesieve-dev libpython3-dev libqhull-dev libreadline-dev librw-dev libsingular4-dev libsqlite3-dev libssl-dev libsuitesparse-dev libsymmetrica2-dev libz-dev libzmq3-dev libzn-poly-dev m4 make nauty openssl palp pari-doc pari-elldata pari-galdata pari-galpol pari-gp2c pari-seadata patch perl pkg-config planarity ppl-dev python3-distutils python3-venv r-base-dev r-cran-lattice singular sqlite3 sympow tachyon tar tox xcas xz-utils
```
为了在运行SageMath时获得额外的功能（例如将Jupyter笔记本导出为pdf），建议安装一些额外的Ubuntu软件包：
```bash
sudo apt install texlive-latex-extra texlive-xetex latexmk pandoc dvipng
```
然后，您可以下载SageMath 10.3的源代码并启动构建，只需在终端中键入以下命令（从主目录或您希望安装SageMath的目录中）：
```bash
# git clone --branch master https://github.com/sagemath/sage.git
wget https://mirrors.ustc.edu.cn/sagemath/src/sage-10.3.tar.gz
cd sage
make configure
./configure
MAKE="make -j8" make
```
最后一条命令以8个线程（由-j8指定）并行启动构建；根据您的CPU进行调整（通常可以选择CPU核心数的两倍作为线程数）。构建时间在现代CPU上约为半小时。完成后，您可以通过键入以下命令创建一个符号链接：
```
sudo ln -sf $(pwd)/sage /usr/bin
```
然后，您可以切换到任何目录并通过运行以下命令启动Jupyter中的SageMath：
```bash
sage -n
```
这时终端会开启一个网络服务。而如果您有图形化界面的话，这将在浏览器中打开一个Jupyter页面。点击“New”，然后选择“SageMath 10.3”以打开一个带有SageMath内核的Jupyter笔记本。<br />要使用Jupyterlab，您首先必须通过以下命令安装它：
```bash
sage -i jupyterlab
```
然后，您可以通过以下命令启动带有SageMath内核的Jupyterlab：
```bash
sage -n jupyterlab
```
### 在Ubuntu 20.04或22.04中安装SageMath 10.4.beta*：
要安装最新的开发版本（beta系列），请按照上述SageMath 10.3的说明进行操作，只是将git clone的命令替换为：
```bash
git clone --branch develop https://github.com/sagemath/sage.git
```
