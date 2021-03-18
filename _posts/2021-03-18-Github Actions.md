![IMG202002231](./images/山1.jpg)  
# Python 脚本获取仓库 Secrets
## 添加 Secrets
打开仓库「Settings」中的「Secrets」，点击「New secret」。
## 配置 GitHub Actions
编辑.yml文件
'''
name: 程序名称

on: 
  workflow_dispatch:
  schedule:
    - cron: '0 10  *  *  *'

jobs:
  run-tool:
    runs-on: ubuntu-latest
    environment: Production
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up Python
        uses: actions/setup-python@v2
        with:
          python-version: 3.8

      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r ./requirements.txt
      
      - name: Working
        env:
          SCKEY: ${{ secrets.SCKEY }}
        run: 
          python ./code/main.py

'''
## Python 脚本中获取环境变量
main.py
'''
import os

if __name__=='__main__':
    SCKEY=os.environ['SCKEY']
'''
