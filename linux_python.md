* pip 

```
sudo apt-get install python3-pip
```

* pipx

```
python3 -m pip install --user pipx
python3 -m pipx ensurepath
```

* conda

```
wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh
bash ~/miniconda.sh
export PATH=$PATH:~/miniconda3/bin
conda init bash
```

(might need to reopen terminal in between the commands)

* venv

```
sudo apt-get install python3-venv
```

* poetry - inside base

```
pipx install poetry
```
