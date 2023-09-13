1.wget https://mirrors.bfsu.edu.cn/anaconda/miniconda/Miniconda3-latest-Linux-x86_64.sh
2.bash Miniconda3-latest-Linux-x86_64.sh
3.it will show you a protocol and ask you Do you wish...?[yes/no], here we input yes and enter
4.choose the location of miniconda3
5.restart the terminal! Important! Restart the terminal!
6.cancel the auto enter the conda base enviroment while every time you enter the terminal by using this command:
	conda config --set auto_activate_base false
Compelete.

ps:
	conda create --prefix ./env pandas numpy matplotlib scikit-learn
	conda install jupyter