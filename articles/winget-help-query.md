---
title: "Windows: winget: wingetでのパッケージ指定方法"
emoji: "🪆"
type: "tech" 
topics: ["windows","SCM","winget","構成管理","CLI"]
published: true
---

## tl;dr

winget では、キーワードを使ってパッケージ一覧からパッケージを検索します。これを query といいます。この記事では、さまざまなパッケージの検索方法を紹介します。
詳しいことは、Microsoft のドキュメント "[search コマンド ~(winget)~](https://docs.microsoft.com/ja-jp/windows/package-manager/winget/search)" を参照してください。

## パッケージ検索 ~(基本編)~ : キーワードで検索する

### キーワード検索

query になにか文字列を入力した場合、キーワードとして検索します。キーワードがパッケージ名やタグなどに含まれていれば、一覧に表示します。

 ``` :PowerShell
 /workspaces > winget search python
 名前                         ID                                  バージョン  一致            ソース
 ----------------------------------------------------------------------------------------------------
 Python 3                     Python.Python.3                     3.9.6150.0  Moniker: python winget
 Python 2                     Python.Python.2                     2.7.18150   Command: python winget
 winpython-dot                winpython.winpython-dot             3.9.4.0     Tag: python     winget
 winpython                    winpython.winpython                 3.9.4.0     Tag: python     winget
 Orange                       UniversityofLjubljana.Orange        3.28.0      Tag: Python     winget
 stackless                    stackless.stackless                 3.7.5       Tag: python     winget
 qutebrowser                  qutebrowser.qutebrowser             2.3.0       Tag: python     winget
 GWSL                         opticos.gwsl                        1.3.8       Tag: python     winget
 Mu                           Mu.Mu                               1.0.3       Tag: python     winget
 IronPython 2                 Microsoft.Ironpython2               2.7.11.1000 Tag: python     winget
 kdevelop                     KDE.kdevelop                        5.5.0       Tag: python     winget
 PyCharm Professional Edition JetBrains.PyCharm.Professional      211.7142.13 Tag: python     winget
 pyaudio                      intxcc.pyaudio                      0.2.11      Tag: python     winget
 Miniforge3                   CondaForge.Miniforge3               4.10.1.4    Tag: python     winget
 Miniconda3                   Anaconda.Miniconda3                 4.9.2       Tag: python     winget
 Anaconda Individual Edition  Anaconda.Anaconda3                  2021.05     Tag: Python     winget
 EduPython                    V.MAILLE.EduPython                  3.0                         winget
 SomePythonThings Zip Manager SomePythonThings.ZipManager         4.1.0                       winget
 WingetUI Store               SomePythonThings.WingetUIStore      0.2                         winget
 Python Tk Gui Builder        CarlWenrich.PythonTkGuiBuilder      1.0.0                       winget
 IronPython 3                 Microsoft.Ironpython3               3.4.0.0001                  winget
 InstantPython                13742StephanBrenner.InstantPython   Latest                      msstore
 Python 3.7                   PythonSoftwareFoundation.Python.3.7 Latest                      msstore
 Python 3.8                   PythonSoftwareFoundation.Python.3.8 Latest                      msstore
 Python 3.9                   PythonSoftwareFoundation.Python.3.9 Latest                      msstore
 ```

### 空白文字入りのキーワード

パッケージ名に空白が入っている場合は、引用符('',"")でくくります。

``` :PowerShell
PS> winget search 'python 3'

名前          ID                                  バージョン  ソース
--------------------------------------------------------------------
Python 3     Python.Python.3                     3.9.6150.0 winget
IronPython 3 Microsoft.Ironpython3               3.4.0.0001 winget
Python 3.7   PythonSoftwareFoundation.Python.3.7 Latest     msstore
Python 3.8   PythonSoftwareFoundation.Python.3.8 Latest     msstore
Python 3.9   PythonSoftwareFoundation.Python.3.9 Latest     msstore

```

## パッケージ検索 ~(発展編)~ : 種別ごとの検索

### 名前、id、モニカー(別名)

パッケージには、パッケージ名やパッケージ ID のほかに、タグやモニカーといった別名がついています。
通常はこれらすべてを検索しますが、種別を指定した検索もできます。

### 名前検索

`--name`オプションをつけると、パッケージ名で検索します。

``` :PowerShell
PS> winget search --name python

名前                         ID                                  バージョン  ソース
-------------------------------------------------------------------------------------
winpython-dot                winpython.winpython-dot             3.9.4.0     winget
winpython                    winpython.winpython                 3.9.4.0     winget
EduPython                    V.MAILLE.EduPython                  3.0         winget
SomePythonThings Zip Manager SomePythonThings.ZipManager         4.1.0       winget
Python 3                     Python.Python.3                     3.9.6150.0  winget
Python 2                     Python.Python.2                     2.7.18150   winget
IronPython 2                 Microsoft.Ironpython2               2.7.11.1000 winget
Python Tk Gui Builder        CarlWenrich.PythonTkGuiBuilder      1.0.0       winget
IronPython 3                 Microsoft.Ironpython3               3.4.0.0001  winget
InstantPython                13742StephanBrenner.InstantPython   Latest      msstore
Python 3.7                   PythonSoftwareFoundation.Python.3.7 Latest      msstore
Python 3.8                   PythonSoftwareFoundation.Python.3.8 Latest      msstore
Python 3.9                   PythonSoftwareFoundation.Python.3.9 Latest      msstore

```

### id検索

`--id`オプションをつけると、パッケージID で検索します。

``` :PowerShell
/workspaces > winget search --id python

名前                         ID                                  バージョン  ソース
-------------------------------------------------------------------------------------
winpython-dot                winpython.winpython-dot             3.9.4.0     winget
winpython                    winpython.winpython                 3.9.4.0     winget
EduPython                    V.MAILLE.EduPython                  3.0         winget
SomePythonThings Zip Manager SomePythonThings.ZipManager         4.1.0       winget
WingetUI Store               SomePythonThings.WingetUIStore      0.2         winget
Python 3                     Python.Python.3                     3.9.6150.0  winget
Python 2                     Python.Python.2                     2.7.18150   winget
IronPython 2                 Microsoft.Ironpython2               2.7.11.1000 winget
Python Tk Gui Builder        CarlWenrich.PythonTkGuiBuilder      1.0.0       winget
IronPython 3                 Microsoft.Ironpython3               3.4.0.0001  winget
InstantPython                13742StephanBrenner.InstantPython   Latest      msstore
Python 3.7                   PythonSoftwareFoundation.Python.3.7 Latest      msstore
Python 3.8                   PythonSoftwareFoundation.Python.3.8 Latest      msstore
Python 3.9                   PythonSoftwareFoundation.Python.3.9 Latest      msstore

```

### モニカー検索

モニカー(moniker)とは、パッケージにつけられる別名のことです。Python のようにバージョンごとにパッケージがある場合などに使用されます。

`--moniker`オプションをつけると、モニカーで検索します。

``` :PowerShell
PS> winget search --moniker python

名前      ID             バージョン   一致             ソース
-----------------------------------------------------------
Python 3 Python.Python.3 3.9.6150.0 Moniker: python  winget
Python 2 Python.Python.2 2.7.18150  Moniker: python2 winget

```

### タグ検索

タグ検索は、パッケージにつけられたタグで一覧を検索します。

`--tag`オプションをつけると、タグでパッケージを検索します。

``` : PowerShell
PS> winget search --tag python

名前                         ID                              バージョン   一致        ソース
------------------------------------------------------------------------------------------
winpython-dot                winpython.winpython-dot        3.9.4.0     Tag: python winget
winpython                    winpython.winpython            3.9.4.0     Tag: python winget
Orange                       UniversityofLjubljana.Orange   3.29.3      Tag: Python winget
stackless                    stackless.stackless            3.7.5       Tag: python winget
qutebrowser                  qutebrowser.qutebrowser        2.3.0       Tag: python winget
Python 3                     Python.Python.3                3.9.6150.0  Tag: python winget
Python 2                     Python.Python.2                2.7.18150   Tag: python winget
GWSL                         opticos.gwsl                   1.3.8       Tag: python winget
Mu                           Mu.Mu                          1.0.3       Tag: python winget
IronPython 2                 Microsoft.Ironpython2          2.7.11.1000 Tag: python winget
kdevelop                     KDE.kdevelop                   5.5.0       Tag: python winget
PyCharm Professional Edition JetBrains.PyCharm.Professional 211.7142.13 Tag: python winget
pyaudio                      intxcc.pyaudio                 0.2.11      Tag: python winget
Miniforge3                   CondaForge.Miniforge3          4.10.1.4    Tag: python winget
Miniconda3                   Anaconda.Miniconda3            4.9.2       Tag: python winget
Anaconda Individual Edition  Anaconda.Anaconda3             2021.05     Tag: Python winget

```

### コマンド検索

パッケージには、タグと同じようにコマンド名がつけられたパッケージもあります。

`--command`オプションで、コマンド名でパッケージを検索します。

``` : PowerShell

/workspaces > winget search --command python

名前                        ID                 バージョン   一致              ソース
---------------------------------------------------------------------------------
Python 3                    Python.Python.3    3.9.6150.0 Command: python  winget
Python 2                    Python.Python.2    2.7.18150  Command: python  winget
Anaconda Individual Edition Anaconda.Anaconda3 2021.05    Command: python3 winget

```

## パッケージ検索 ~(発展編 2)~: その他のオプション

検索時にオプションを指定することで、さらに細かい検索ができます。オプションを指定した検索例を掲載します。

- -e --exact
   英単語の大文字／小文字をふくめ、入力した文字列に完全一致するパッケージを検索します

   ``` : PowerShell
   PS> winget search 'Python 3' --exact
   名前      ID              バージョン   ソース
   -------------------------------------------
   Python 3 Python.Python.3  3.9.6150.0 winget

   ```

- -n --count
   一覧の表示行数を制限します。

   ``` :PowerShell
   PS> winget search python -n 5
   
   名前           ID                           バージョン  一致             ソース
   ----------------------------------------------------------------------------
   Python 3      Python.Python.3              3.9.6150.0 Moniker: python winget
   Python 2      Python.Python.2              2.7.18150  Command: python winget
   winpython-dot winpython.winpython-dot      3.9.4.0    Tag: python     winget
   winpython     winpython.winpython          3.9.4.0    Tag: python     winget
   Orange        UniversityofLjubljana.Orange 3.29.3     Tag: Python     winget
   <結果制限により、エントリがさらに切り捨てられました>
   
   ```

- -s --source
   指定したソースのパッケージのみで検索します。
   現状、source には Windows Package Manager 標準の`winget`とマイクロソフトストア`msstore`が指定できます。

   ``` :PowerShell
   PS> winget search python --source msstore
   
   名前           ID                                 バージョン
   ------------------------------------------------------------
   InstantPython 13742StephanBrenner.InstantPython   Latest
   Python 3.7    PythonSoftwareFoundation.Python.3.7 Latest
   Python 3.8    PythonSoftwareFoundation.Python.3.8 Latest
   Python 3.9    PythonSoftwareFoundation.Python.3.9 Latest
   
   ```
