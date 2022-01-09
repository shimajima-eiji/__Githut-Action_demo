## __Githut-Action_demo
mainブランチにコミットされるたびに、dummyファイルにコミットした時間を書き込むデモ。  
forkして変数を設定すればすぐ使えるようにしている。

## 解説
https://github.com/shimajima-eiji/__Githut-Action_demo/blob/main/.github/workflows/add_dummy.yml

### git cloneの仕方
必要なのは、steps以下の`uses: actions/checkout@v2`で`git clone`していること。  
これを認識していないとgitコマンドをうまくつかえなくてハマってしまう。

### `run |`の意味
以下に書くコマンドは１行で１つを意味する。非常に楽。

### （補足）変数を非公開にしたい
https://github.com/(USER)/(REPOSITORY)/settings/secrets/actions で追加する。  
ここでは、`USER`と`EMAIL`に何らかの値を入れていることが分かる。

### dateコマンドのタイムゾーン
Github Actionsで`date`コマンドを実行すると、タイムゾーンがUTCになっているため、JSTに変換したい場合は一手間必要。

## やらかし例
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
