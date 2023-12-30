## NVM(Node.js version manager) for Windowsで複数バージョンのNode.jsを使用する

``` diff
{
+   "useLocaleNames": {
+     "en": "English",
+     "ja": "Japanese"
+   },
    "Header": {
      "Home": "Home",
      "Dashboard": "Dashboard",
      "Newsletter": "Newsletter"
    },
    "Home": {
      "Demo project": "Demo project",
      "Nested layouts in Nextjs": "Nested layouts in Next.js"
    }
  }
```

### NVM の必要性

開発環境において、Node.jsを使用する場面が増えてきました。
Node.jsはバージョンアップのサイクルが早い上、バージョンによる環境依存が強いです。
そのため、プロジェクトが増えると、複数バージョンのNode.jsが必要になってきます。
めんどくさいですね。

NVMを使用すれば、複数バージョンのNode.jsをインストール、切替など、簡単に管理できます。

### Winget によるインストール

使用している Windows に Winget をインストールしてあれば、Winget から NVM をインストールできる。

NVM をインストール:  
``` console
winget install -e --id CoreyButler.NVMforWindows
```

次のコマンドを Windows Terminal（Git Bash）で実行して、NVM がインストールされた場所を確認する。

NVM のインストール場所を確認:  
``` console
which nvm
```

実行結果例:  
```
/c/Users/{ユーザ名}/AppData/Roaming/nvm/nvm
```

システム環境変数を確認すると、以下の2つの環境変数が設定されている。

|変数 |値 |
|:-- |:-- |
|NVM_HOME |C:\Users\{ユーザ名}\AppData\Roaming\nvm |
|NVM_SYMLINK |C:\Program Files\nodejs |

環境変数を反映させるために、Windows Terminal を開きなおす。

### 

以下のコマンドで、
インストールされている Node.js のバージョンと、現在適用されている Node.js のバージョンを確認できる。

インストール済みのバージョンと、適用されているバージョンを確認:  
``` console
nvm list
```

実行結果例（NVM をインストールしたばかりで、まだ Node.js を1つもインストールしていない場合）: 
```
No installations recognized.
```

###

以下のコマンドで、
インストール可能な Node.js のバージョン一覧が表示される。

インストール可能な Node.js バージョン一覧を表示:  
``` console
nvm list available
```

実行結果例（2023/08/31 時点）:  
```
|   CURRENT    |     LTS      |  OLD STABLE  | OLD UNSTABLE |
|--------------|--------------|--------------|--------------|
|    20.5.1    |   18.17.1    |   0.12.18    |   0.11.16    |
|    20.5.0    |   18.17.0    |   0.12.17    |   0.11.15    |
|    20.4.0    |   18.16.1    |   0.12.16    |   0.11.14    |
|    20.3.1    |   18.16.0    |   0.12.15    |   0.11.13    |
|    20.3.0    |   18.15.0    |   0.12.14    |   0.11.12    |
|    20.2.0    |   18.14.2    |   0.12.13    |   0.11.11    |
|    20.1.0    |   18.14.1    |   0.12.12    |   0.11.10    |
|    20.0.0    |   18.14.0    |   0.12.11    |    0.11.9    |
|    19.9.0    |   18.13.0    |   0.12.10    |    0.11.8    |
|    19.8.1    |   18.12.1    |    0.12.9    |    0.11.7    |
|    19.8.0    |   18.12.0    |    0.12.8    |    0.11.6    |
|    19.7.0    |   16.20.2    |    0.12.7    |    0.11.5    |
|    19.6.1    |   16.20.1    |    0.12.6    |    0.11.4    |
|    19.6.0    |   16.20.0    |    0.12.5    |    0.11.3    |
|    19.5.0    |   16.19.1    |    0.12.4    |    0.11.2    |
|    19.4.0    |   16.19.0    |    0.12.3    |    0.11.1    |
|    19.3.0    |   16.18.1    |    0.12.2    |    0.11.0    |
|    19.2.0    |   16.18.0    |    0.12.1    |    0.9.12    |
|    19.1.0    |   16.17.1    |    0.12.0    |    0.9.11    |
|    19.0.1    |   16.17.0    |   0.10.48    |    0.9.10    | 
```

### 最新の Node.js バージョンをインストール

以下のコマンドで最新バージョンをインストールすることができる。

最新の Node.js バージョンをインストール:  
``` console
nvm install latest
```

`nvm list` コマンドでインストールされているバージョンを確認する。

インストールされている Node.js のバージョンを確認:  
``` console
nvm list
```

実行結果例（最新バージョンをインストール後）:  
```
    20.5.1
```

Node.js のバージョンを確認すると、まだ Node.js を適用していないので、コマンドがエラーになる。

Node.js のバージョンを確認:  
``` console
node --version
```

実行結果例:  
```
bash: node: command not found
```

### 

以下のコマンドで、
アクティブにする Node.js のバージョンを指定することができる。

アクティブにする Node.js のバージョンを指定:  
``` console
nvm use {アクティブにしたいNode.jsのバージョン番号}
```

指定例:  
``` console
nvm use 20.5.1
```

実行結果例:  
```
Now using node v20.5.1 (64-bit)
```

再度、`nvm list` コマンドを実行してみると、指定したバージョンがアクティブになっていることが分かる。

`nvm use 20.5.1` 実行後の `nvm list` コマンド実行結果例:  
```
  * 20.5.1 (Currently using 64-bit executable)
```

### 安定版をインストール

以下のコマンドで安定版をインストールすることができる。

``` console
nvm install lts
```

実行結果例:  
```
Downloading node.js version 18.17.1 (64-bit)...
Extracting node and npm...
Complete
npm v9.6.7 installed successfully.


Installation complete. If you want to use this version, type

nvm use 18.17.1
```

実行結果例では Ver. 18.17.1 がインストールできているが、
`nvm list` で確認すると、Ver. 18.17.1 がアクティブになっていないことが分かる。

安定版（LTS）をインストール後の `nvm list` 実行結果例:  
```
  * 20.5.1 (Currently using 64-bit executable)
    18.17.1
```

`nvm use` コマンドで Ver. 20.5.1 から Ver. 18.17.1 にバージョンを切り替えてみる。

Ver. 18.17.1 にバージョンを切り替え:  
``` console
nvm use 18.17.1
```

切替後、`nvm list` を実行すると、想定通り Ver. 18.17.1 が有効になっていることが分かる。

Ver. 18.17.1 に切替後の `nvm list` コマンド実行結果例:   
```
    20.5.1
  * 18.17.1 (Currently using 64-bit executable)
```

以下のコマンドで、
Node.js のバージョンを確認してみると、NVM で有効にしたバージョンになっていることも分かる。

Node.js のバージョンを確認:  
``` console
node --version
```

実行結果例:  
```
v18.17.1
```

### バージョン番号を指定してインストール

NVM では、バージョン番号を指定して、Node.js をインストールすることもできる。

バージョン番号を指定して、NVM で Node.js をインストール
``` console
nvm install {バージョン番号}
```
Ver. 16.20.2 をインストールしてみる。

NVM で Ver. 16.20.2 の Node.js をインストール:  
 ``` console
 nvm install 16.20.2
 ```

 `nvm list` でインストールできたかを確認してみる。

 `nvm list` の実行結果例:  
 ```
     20.5.1
  * 18.17.1 (Currently using 64-bit executable)
    16.20.2
 ```

 ### アンインストール

 インストールと同じように、バージョン番号を指定してアンインストールすることもできる。

バージョン番号を指定して、NVM で Node.js をアンインストール
``` console
nvm uninstall {バージョン番号}
```

### まとめ

Windows システムに NVM をインストールする手順を紹介した。
NVM を使うことで、Windows システムに複数の Node.js バージョンをインストールしておくことができ、
インストールされてるバージョンの中からコマンドを使って指定バージョンに切り替えることができる。

利用している Windows 端末に複数のアカウントがある場合は、
NVM は特定のユーザーに対してインストールされることに注意する必要がある。
別のユーザーで NVM を使用するには、そのアカウントからも個別にインストールする必要がある。

以上。
