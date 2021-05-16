# デバッグ方法

Udon のデバッグ方法は大きく分けて 2 つあります。  
1 つは Unity Editor 上で直接デバッグする方法、もう一つは、 VRChat で実際にテスト動作させることです。  
単純なギミック類であれば、 Udon Editor 上でデバッグしても問題はありませんが、実際の動作と異なる可能性があるので、ワールドをアップロードする前に一度実際に動作させることをオススメしています。

ここでは、後者の VRChat で動作テストを行う方法について説明します。

## 設定

VRChat SDK のバグかどうかは知りませんが、次の操作を行う必要があります。  
初期設定のままでも問題は無いのですが、初期設定のままだと、不具合が発生しているので、一度設定を行う必要があるのです。
まず、 VRChat SDK のコントロールパネルを開いてください。  
これは、 Unity のメニューバーの「VRChat SDK」→「Show Control Panel」から表示させることが出来ます。

次に、コントロールパネルの「Settings」ページを開き、ページ下部にある「VRChat Client Installed Path」の値を、「Edit」ボタンを押して変更してください。

<figure>
  <img src="https://assets.mochizuki.moe/udon/getting-started/configure-client-location.png" width="400px" data-zoomable="true">
  <figcaption>上記画像にて、丸で囲まれている部分をクリック</figcaption>
</figure>

すると、ファイル選択ダイアログが表示されるので、 VRChat をインストールした場所にある、「VRChat.exe」を選択します。  
インストールする場所を変更していない場合は、下記の場所にインストールされているはずです。

| Platform | Location                                                                          |
| -------- | --------------------------------------------------------------------------------- |
| Steam    | `C:\Program Files (x86)\Steam\steamapps\common\VRChat\VRChat.exe`                 |
| Oculus   | `C:\Program Files\Oculus\Software\Software\vrchat-vrchat\VRChat.exe`              |
| Viveport | `C:\Viveport\ViveApps\469fbcbb-bfde-40b5-a7d4-381249d387cd\1597468388\VRChat.exe` |

これで、必要最低限の設定は完了です。

## ローカルテスト

VRChat では、ワールドを実際に公開する前に、ローカル環境で動作の確認を行うことが出来ます。  
Udon においても、基本的にはこの方法を用いて動作の確認を行います。

まず、コントロールパネルから「Builder」タブを開きます。  
そして、一番下にある「Local Testing」とある項目にある、「Build & Test」をクリックすることで、ローカル環境で動作確認ができます。

<figure>
  <img src="https://assets.mochizuki.moe/udon/getting-started/local-testing.png" width="450px" data-zoomable="true">
  <figcaption>Local Testing の項目</figcaption>
</figure>

このとき、 `Number of Clients` を 2 より大きい数にすることで、複数人での挙動を確認できますし、「Force Non-VR」にチェックを入れることで、デスクトップモードで動作確認を行うことも出来ます。

## ログの出し方

Udon 開発においては、なにをどうした、といったログを出力することで、よりスムーズにギミックをくみ上げることが可能になります。  
ログ出力の方法はいくつかありますが、最も簡単な例は、 Unity 標準のログ出力を行うことです。  
これは、それぞれ以下の方法で行うことが出来ます。  
※ここでは Start イベントにて出力していますが、実際はどこでやっても問題ありません。

<!-- prettier-ignore-start -->
=== "Udon Graph"

    <img src="https://assets.mochizuki.moe/udon/getting-started/logging-example.png" width="400px" data-zoomable="true">

=== "UdonSharp"

    ```csharp
    using UdonSharp;

    using UnityEngine;

    namespace NatsunekoLaboratory.Examples
    {
        public class LoggingExample : UdonSharpBehaviour
        {
            private void Start()
            {
                Debug.Log("Hello, World");
            }
        }
    }
    ```

=== "出力例"

    ```
    Hello, World
    ```

<!-- prettier-ignore-end -->

この方法で出力したログは、 `C:\Users\ユーザー名\AppData\LocalLow\VRChat\VRChat` に、 `output_log_XX-XX-XX.txt` の形式で出力されます。  
また、 VRChat 内でリアルタイムに表示することもでき、その場合は、キーボードの `右 Shift + @ + 3` で出力することが出来ます。  
ただし、これを行うためには、 `--enable-debug-gui` というオプションを渡す必要があるので、個人的には特に理由もなければ、初めのログファイルを閲覧する方法が良いと思います。

## エラーの探し方

VRChat では、 Udon ギミックでエラーが発生した場合は、それ以降そのギミックが発生しないように無効化 (`Disabled` を設定) されます。  
このとき、発生したエラー内容が上記ログファイルに出力されています。

多くの場合は、次の文字列をファイル内で検索することで見つけることが出来ます。

```
[UdonBehaviour] An exception occurred during Udon execution, this UdonBehaviour will be halted.
```

## エラーログの見方

TODO
