# Etude for Python
---

# 目的 #
Pythonアプリケーションのための練習プログラム集

# 前提 #
| ソフトウェア   | バージョン   | 備考        |
|:---------------|:-------------|:------------|
| python         |3.6.1    |             |


# 構成 #
1. [構築](#構築)
1. [配置](#配置)
1. [運用](#運用)
1. [開発](#開発)

## 構築
#### 仮想マシンセットアップ
```bash
vagrant up
vagrant ssh
cd /vagrant
```

#### コンポーネントセットアップ
```bash
curl -L https://raw.githubusercontent.com/pyenv/pyenv-installer/master/bin/pyenv-installer | bash
echo 'export PATH="/home/vagrant/.pyenv/bin:$PATH"' >> ~/.bash_profile
echo 'eval "$(pyenv init -)"' >> ~/.bashrc
echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bash_profile
source ~/.bash_profile
pyenv -v
pyenv install 3.6.1
pyenv local 3.6.1
```

**[⬆ back to top](#構成)**

## 配置
**[⬆ back to top](#構成)**

## 運用
**[⬆ back to top](#運用)**

## 開発
**[⬆ back to top](#構成)**

