# SDK3 のインストール

このページでは、 Udon および UdonSharp を始めるための準備について解説します。

## SDK のインストール

Udon を始めるためには、 Udon SDK が必要です。  
VRChat 公式サイトから、「VRCHAT SDK3」と書かれた方にある、「Download SDK3 - Worlds」をクリックして、最新版の SDK をダウンロードしてください。

<figure>
  <img src="https://assets.mochizuki.moe/udon/getting-started/udon-sdk.PNG" width="400px" data-zoomable="true">
  <figcaption>上記画像にて、丸で囲まれている部分をクリック</figcaption>
</figure>

ダウンロードしたら、新規 Unity プロジェクトを作成して、 SDK のインポートを行ってください。  
このとき、 Unity のバージョンは **2018.4.20f1** (アバターと同じバージョン) を使うようにしてください。

<!-- prettier-ignore-start -->
??? info "Tips - Worlds と Avatars の違い"
    VRChat SDK3 には、ワールドを作るための SDK である「Worlds」と、アバターを作るための SDK である「Avatar」の2種類があります。  
    Worlds にはワールドを作るための機能や Udon が含まれており、 Avatar にはアバターを作るためのアセット類が含まれています。  
    逆に、 Avatar の SDK でワールドを作ることは出来ませんし、 Worlds の SDK でアバターを作ることも出来ません。  
    ふたつは共存可能ですが、プロジェクトが重くなるためあまり推奨はしません。  
    基本的には、用途に合わせたパッケージを使うようにしてください。
<!-- prettier-ignore-end -->

## プロジェクト設定

SDK のインストールが終わったら、プロジェクト設定を行います。  
`VRChat Examples/Prefabs` の中にある、 `VRCWorld` をシーンの中にドラッグアンドドロップしてください。

<figure>
  <img src="https://assets.mochizuki.moe/udon/getting-started/configure-project.png" width="300px" data-zoomable="true">
  <figcaption>上記画像にて、丸で囲まれているものをシーンに入れる</figcaption>
</figure>

その後、 Unity のメニューバーの「VRChat SDK」から、「Show Control Panel」をクリックし、コントロールパネルを表示し、 VRChat へログインしてください。  
ログイン後、「Builder」タブを開いてください。  
開いたら、まずは「Setup Layers for VRChat」ボタンをクリックします。

<figure>
  <img src="https://assets.mochizuki.moe/udon/getting-started/builder-tab-in-control-panel.png" width="300px" data-zoomable="true">
  <figcaption>三角に！マークが表示されてて仰々しい感じですが、無視して良いです</figcaption>
</figure>

するとダイアログが表示されるので、「Do It!」を押してください。

<figure>
  <img src="https://assets.mochizuki.moe/udon/getting-started/setup-layers-confirm.png" width="300px" data-zoomable="true">
  <figcaption>丸で囲まれている部分を押してください</figcaption>
</figure>

このとき、 Unity においてレイヤーというものが設定されます。  
レイヤーは、カメラオブジェクトに一部分だけ映したい、またはライトで一部分だけ照らしたい、といった場合に使用されます。  
今回は使いませんので、詳しい解説については、[Unity 公式ドキュメント](https://docs.unity3d.com/ja/2018.4/Manual/Layers.html)を参照してください。

レイヤーの設定が終わったら、次に「Set Collision Matrix」ボタンをクリックします。

<figure>
  <img src="https://assets.mochizuki.moe/udon/getting-started/builder-tab-in-control-panel-2.png" width="300px" data-zoomable="true">
  <figcaption>丸で囲まれている部分を押してください</figcaption>
</figure>

すると再度ダイアログが表示されるので、もう一度「Do It!」を押してください。

<figure>
  <img src="https://assets.mochizuki.moe/udon/getting-started/setup-collision-matrix-confirm.png" width="300px" data-zoomable="true">
  <figcaption>丸で囲まれている部分を押してください</figcaption>
</figure>

ここでは、レイヤー同士の当たり判定について設定されます。  
これについても、今回は使いませんので、詳しい解説については [Unity 公式ドキュメント](https://docs.unity3d.com/ja/2018.4/Manual/LayerBasedCollision.html)を参照してください。

SDK のセットアップはここまでで終了です、お疲れさまでした。  
なお、 UdonSharp を使う場合は、[UdonSharp のインストール](/getting-started/udon-sharp-installation)も行ってください。
