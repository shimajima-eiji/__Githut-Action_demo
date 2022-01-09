## __Githut-Action_demo
mainブランチにコミットされるたびに、dummyファイルにコミットした時間を書き込むデモ

### 解説
https://github.com/shimajima-eiji/__Githut-Action_demo/blob/main/.github/workflows/add_dummy.yml

必要なのは、steps以下の`uses: actions/checkout@v2`で`git clone`していること。  
これを認識していないとgitコマンドをうまくつかえなくてハマってしまう。

### （任意）変数を非公開にしたい
https://github.com/(USER)/(REPOSITORY)/settings/secrets/actions で追加する。  
ここでは、EMAILという名前で何らかの値を入れていることが分かる。

### やらかし例
```
steps:
  name: 
  run: |
    git config --global user.email "${{ secrets.EMAIL }}"
    git config --global user.user "${{ secrets.USER }}"
    git clone (url)
    cd (repository)
    echo "test" >dummy
    git commit -m "test" -a  # ここでエラー
    git pull
    git push
```

見た目には問題なさそうだが、このコードでは動かない。
