# FlexConf

Flexible Configure

## Installation

```sh
pip install flexconf
```

プロジェクト配下で以下のコマンドを実行すると、設定ファイルのテンプレートが作成されます。

```sh
python -m flexconf
```

## Examples

例えば以下の構成を考えます。

```sh
.
├─ .flexconf/
│   ├─ pattern1.conf
│   └─ pattern2.conf
└─ sample.py         # ライブラリを使用するスクリプト
```

それぞれの設定ファイルは以下のような構成にします。

```conf
# pattern1.conf
[DEFAULT]           # 必ず書く
A = 3               # パラメータ名 = 値 という書式で記述する
B = 1920 1080       # 値にものが文字列として読み込まれる
```

この設定を利用するサンプルプログラムです。

```py
# sample.py
from flexconf import FlexConf

class SubClass(FlexConf):
    # __init__を定義する必要はない
    # 定義する場合は、super().__init__()を実行する
    def __init__(self):
        # do something here
        super().__init__()

    def sample_method(self):
        # `./.flexconf/*.conf`に定義したパラメータの値を
        # self.パラメータ名 で取得することができる
        print(self.A)
        print(self.B)

if __name__ == "__main__":
    s = SubClass()
    s.sample_method()
```

実行例

```sh
// -p オプションで使用したい設定ファイルを選択します
$ python sample.py -p pattern1
3
1920 1080
$ python sample.py -p pattern2
4
hogehoge
```
