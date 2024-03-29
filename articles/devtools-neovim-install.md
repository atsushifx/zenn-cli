---
title: "wingetを使ったNeovimのインストール"
emoji: "🍣"
type: "tech"
topics: [ "tips", "winget", "Neovim", "開発環境" ]
published: true
---

## はじめに

`Neovim`[^1]は、`Vim`から派生した高機能テキストエディタで、拡張性とモダンな機能が特徴です。
この記事では、Windows の公式パッケージマネージャー`winget`[^2]を使用して`Neovim`をインストールする方法について説明します。

[^1]: `Neovim`: `Vim`から派生したテキストエディタで、拡張性にモダンな機能が特徴
[^2]: `winget`: Windows の公式パッケージマネージャー

## 1. `Neovim`のインストール

### 1.1. `winget`のオプション

`winget`には多くのオプションがありますが、パッケージによっては対応していないものがあります。
`Neovim`は、`--location`オプションと`--interactive`オプションには対応していません。
その代わり、`--override`オプションを使ってインストーラーのオプションを指定することで対応できます。

### 1.2. インストール先ディレクトリの設定

`Neovim`では、`INSTALL_ROOT`[^3]プロパティを用いてインストール先ディレクトリを指定します。
GitHub にある[Neovimの`WiX`インストーラーの設定](https://github.com/Neovim/Neovim/blob/master/cmake.packaging/WixPatch.xml)を参照してください。

インストールコマンドでは、"`INSTALL_ROOT`=<インストール先ディレクトリ>"を指定して、インストール先ディレクトリを設定します。

[^3]: `INSTALL_ROOT`: `WiX`インストーラーで、ソフトウェアのインストール先を指定するプロパティ

### 1.3. 対話形式インストールの設定

`Neovim`のインストーラーは`msiexec`[^4]コマンドを使用しています。
`msiexec`は Windows 標準のインストーラーであり、GUI の対話形式でのインストールが可能です。
インストール時に`/qf`オプションを指定すると、`フルUI`でインストールできます。

[^4]: `msiexec`:Windows のインストーラーコンポーネントであり、インストール、保守、アンインストールを行なうためのツール

### 1.4. `winget`によるインストール

以下のコマンドを実行することで、`Neovim`を"`c:\bin\nvim`"ディレクトリにインストールします。

```powershell
winget install --id Neovim.Neovim --override "/qf INSTALL_ROOT=c:\bin\nvim"

```

このコマンドは、`Neovim`を"`c:\bin\nvim`"にインストールします。

## 2. `Neovim`の設定

インストールした`Neovim`をコンソールから実行できるように Windows の環境変数を設定します。

### 2.1. "Path"の追加

コンソールから`Neovim`を実行できるように、環境変数 "Path" に"`c:\bin\nvim\bin`"を追加します。
次の手順で、"Path"を設定します。

1. \[環境変数]ダイアログを開く:
   ![環境変数](https://i.imgur.com/evyEYgP.jpg)

2. システム環境変数"Path"に"`c:\bin\nvim\bin`"を追加:

   システム環境変数"Path"を選んで\[編集]をクリックし、"`c:\bin\nvim\bin`"を追加して\[OK]をクリックします。

3. \[環境変数]ダイアログを閉じる:
   \[OK]をクリックして、ダイアログを閉じます。

または、PowerShell コマンドで"Path"を追加します:

<!-- markdownlint-disable line-length -->
```powershell
[System.Environment]::SetEnvironmentVariable("Path",  [System.Environment]::GetEnvironmentVariable("Path", "Machine")+";c:\bin\nvim\bin", "Machine")

```
<!-- markdownlint-enable -->
**注意**
上記コマンドの実行には、管理者権限が必要です。

以上で、"Path"の追加は終了です。
PC を再起動すると、変更した"Path"がシェルに反映されます。

### 2.2. `vim.exe`の作成

多くのユーザーが`Vim`テキストエディタを起動することに慣れているため、`Neovim`の実行ファイル`nvim.exe` へのシンボリックリンクとして`vim.exe`を作成します。

次の PowerShell コマンドを実行します:

```powershell
New-Item -Path C:\bin\nvim\bin\vim.exe -ItemType SymbolicLink -Value C:\bin\nvim\bin\nvim.exe

```

以上で、`vim`で`Neovim`が立ち上がります。

## おわりに

この記事では、`winget`を使って`Neovim`を Windows 上に簡単にインストールする方法を説明しました。

`Neovim` の魅力は、カスタマイズ性が高く、プラグインを活用してさらに拡張できることです。
`Neovim`を自分好みにカスタマイズし、素晴らしいプログラミング環境を構築しましょう。

それでは、Happy Hacking!

## 参考資料

### Webサイト

- [`Neovim` 公式サイト](http://neovim.io/)
- [`Neovim` GitHubリポジトリ](https://github.com/neovim/neovim)
