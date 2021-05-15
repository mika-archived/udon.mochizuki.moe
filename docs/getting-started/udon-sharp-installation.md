# UdonSharp のインストール

C# プログラミングで Udon ロジックを作るためには、 UdonSharp のインストールが必要です。  
下記リンクから、 UdonSharp の最新版をダウンロードし、プロジェクトにインポートしてください。

-   [MerlinVR/UdonSharp - Latest Release](https://github.com/MerlinVR/UdonSharp/releases/latest){target=\_blank}

<figure>
  <img src="https://assets.mochizuki.moe/udon/getting-started/udon-sharp-download.png" data-zoomable="true">
  <figcaption>
    丸で囲まれている部分をクリックするとダウンロードできる<br>
    <code>UdonSharp_vX.X.X.unitypackage</code> をダウンロードしよう
  </figcaption>
</figure>

## トラブルシューティング

### インポートした瞬間にエラーが出る

以下の事を確認してください。

-   VRCSDK3 Worlds は最新版を使用していますか？
    -   Beta バージョンを使用していませんか？
-   VRCSDK3 Worlds のすべてのファイルをインポートしましたか？
    -   ファイルに抜けなどがあった場合、エラーが発生することがあります。この場合再インポートを行ってください。
-   パスに日本語などが含まれていませんか？
    -   最新版では治っているようですが、念のため
