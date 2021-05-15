# 初めての Udon コンポーネント

このページでは、基本的な Udon Graph / UdonSharp コンポーネントの作り方について解説します。

## 共通操作

セットアップが終わったら、初めての Udon コンポーネントを作ってみましょう。  
ここでは、単純にキューブを回転させるだけのコンポーネントを作ってみます。  
面白くない？はい、どんなものでも始めて触ってみる場合はそんなものです。

まずは、空のシーンを作成してください。  
空のシーンはプロジェクトビューにて右クリックから「Create」→「Scene」にて作成できます。

<figure>
  <img src="https://assets.mochizuki.moe/udon/getting-started/create-empty-scene.png" width="400px" data-zoomable="true">
  <figcaption>上記画像にて、ハイライトされている部分を順にクリックしていく</figcaption>
</figure>

シーンを作成したら、 [SDK3 のインストール](/getting-started/installation)で行ったように、 `VRCWorld` をワールドに設置します。  
設置後、適当な Cube を作成してください。  
Cube はシーンヒエラルキーにて右クリックから「3D Object」→「Cube」にて作成することが出来ます。

<figure>
  <img src="https://assets.mochizuki.moe/udon/getting-started/create-cube-object.png" width="400px" data-zoomable="true">
  <figcaption>上記画像にて、ハイライトされている部分を順にクリックしていく</figcaption>
</figure>

Cube を設置したら、 Inspector から、Cube に対して Udon Behaviour というものを追加します。  
これは、 Udon Graph や UdonSharp コンポーネントをくっつけられるもので、基本的な動作などの設定を行うことが出来ます。

<figure>
  <img src="https://assets.mochizuki.moe/udon/getting-started/find-udon-behaviour.png" width="350px" data-zoomable="true">
  <figcaption>Cube を選択した状態で、 Inspector の「Add Component」をクリックし、「Udon Behaviour」を追加する</figcaption>
</figure>

## Udon Graph の場合

Udon Graph を用いて Udon コンポーネントを作成する場合は、 Udon Behaviour の「Program Source」に「Udon Graph Program Asset」を設定したのち、「New Program」をクリックしてください。

<figure>
  <img src="https://assets.mochizuki.moe/udon/getting-started/create-new-udon-graph-program-asset.gif" width="450px" data-zoomable="true">
  <figcaption>「Udon Graph Program Asset」になっていることを確認した上で、「New Program」を押す</figcaption>
</figure>

暫く待つとアセットが作成されるので、作成されたら、「Open Udon Graph」をクリックして、 Udon Graph Editor を開きましょう。

<figure>
  <img src="https://assets.mochizuki.moe/udon/getting-started/open-udon-graph-editor.png" width="450px" data-zoomable="true">
  <figcaption>横に長いこのボタンを押す</figcaption>
</figure>

<!-- prettier-ignore-start -->
??? info "Tips - プロジェクトビューからアセットを作成も出来る"
    今回はやりませんでしたが、プロジェクトビューからも Udon Graph Program Asset を作成することが出来ます。  
    その場合は、コンテキストメニューを開いた後、「Create」→「VRChat」→「Udon」→「Udon Graph Program Asset」と進んでください。  
    また、この場合はプロジェクトビューで作成したアセットを選択した状態で、インスペクターからエディターを開けます。
<!-- prettier-ignore-end -->

エディターが開いたら、適当な場所で右クリックし、「Create Node」を選択してください。  
その状態で、「FixedUpdate」と入力し `Event FixedUpdate` をクリックして、今回の処理の起点となるイベントノードを作成します。

<!-- prettier-ignore-start -->
??? info "Tips - イベントについて"
    Udon では、基本的にはすべての動作は `イベント` から開始します。  
    今回の `FixedUpdate` は、一定時間に1回だけ発生するイベントを指します。  
    他には、ボタンを押したときなどに発生する `Interact` や、初期化処理を行うための `Start` などがあります。
<!-- prettier-ignore-end -->

<figure>
  <img src="https://assets.mochizuki.moe/udon/getting-started/fixed-update.png" width="450px" data-zoomable="true">
  <figcaption>これを追加する</figcaption>
</figure>

追加したら、次は Variables の右にあるプラスボタンを押します。  
Variables は、変数と呼ばれるものを設定する場所で、いろいろな値を保存することが出来ます。

<!-- prettier-ignore-start -->
??? info "Tips - 変数について"
    変数とは、基本的にはなんらかの値を保持するための記憶領域を指します。  
    例えば、今回のプログラムの場合は、「回転させるキューブはどれか？」という値を保持します。  
    変数の値はプログラムの中で書き換えることも出来ますが、今回のように外部から入力することも可能です。  
    Udon においては、多くの場合、計算結果や文字列などを一時的に保存しておいたり、フレームを跨いだ処理を行うときに、前フレームの計算結果を保存しておいたり、設定を保存しておいたり等に使います。
<!-- prettier-ignore-end -->

プラスボタンを押すと先ほどと同様のダイアログが表示されるので、 `Transform` と入力し、追加してください。  
これは、 `Transform` コンポーネントを持った GameObject を保持する、という意味になります。  
追加できたら、変数を外部 (インスペクターなど) から設定可能にします。

左端にある矢印をクリックして、メニューを出し、 `public` の部分にチェックを入れてください。

<figure>
  <img src="https://assets.mochizuki.moe/udon/getting-started/mark-variable-as-public.png" width="250px" data-zoomable="true">
  <figcaption><code>public</code> にチェック, <code>synced</code> はまだ使いません</figcaption>
</figure>

このとき、楕円で囲まれた部分をダブルクリックすることで、変数の名前を変更することが出来ます。  
通常、ここはわかりやすい名前に設定しておくことで、あとで見直したときや、再編集する際などに見通しが良くなります。  
今回の場合は、 `Transform` コンポーネントを受け取る変数なので、 `_transform` と名付けました。

最後に、楕円形の部分をドラッグして、 `FixedUpdate` の下に持って行ってください。  
こうすることで、変数を使用するための準備が完了しました。

<figure>
  <img src="https://assets.mochizuki.moe/udon/getting-started/set-transform-variable.PNG" width="250px" data-zoomable="true">
  <figcaption>この時点で、こうなっていれば OK</figcaption>
</figure>

次は、回転する方向を定義します。  
先ほどと同じような操作で `Vector3` と `float` の変数を作成してください。  
`Vector3` は、高校数学で習った方もいるかもしれませんが、ベクトルについての変数です。  
X, Y, Z の方向に、どれだけ動くか、を入力することが出来ます。  
`float` は、何らかの数値を指します。 `0` や `-1.5`, `3.14` など、小数も含めた数値です。

<figure>
  <img src="https://assets.mochizuki.moe/udon/getting-started/create-axis-variable.gif" width="350px" data-zoomable="true">
  <figcaption>Vector3 の作成例</figcaption>
</figure>

最後に、回転する処理を追加します。  
これは、 `Transform` コンポーネントにある `Rotate` というノードを呼び出すことで達成できます。  
まずは、イベントノードを追加したのと同じように、ノードの追加メニューを開いてください。  
その後、 `Transform` と入力し、選択した後、 `Rotate` を再度選択します。

<figure>
  <img src="https://assets.mochizuki.moe/udon/getting-started/create-transform-rotate.gif" width="400px" data-zoomable="true">
  <figcaption>操作の流れはこんな感じ</figcaption>
</figure>

最後に、それぞれのノードをくっつけます。  
Udon Graph では、ノードのそれぞれに矢印、もしくは色つきの丸が付いています。  
それらを、**ノードの左側の部分から、ノードの**同じ形の同じ色の場所にくっつけることによって、処理を繋げることが出来ます。  
繋げるには、**ノードの右側にある**矢印や丸の部分をドラッグして、同じ色の別のノードの**左側**の部分へドロップします。

<figure>
  <img src="https://assets.mochizuki.moe/udon/getting-started/first-udon-graph-component.png" width="400px" data-zoomable="true">
  <figcaption>こうなっていれば OK</figcaption>
</figure>

最後に、 `Ctrl + S` で保存すれば、初めての Udon Graph プログラムの完成です。

## UdonSharp の場合

<!-- prettier-ignore-start -->
!!! info
    Udon Graph と共通の説明部分 (例: イベントとは？、変数とは？) については、 Udon Graph 側の説明に記述しているので、そちらを参照してください。
<!-- prettier-ignore-end -->

Udon Graph を用いて Udon コンポーネントを作成する場合は、 Udon Behaviour の「Program Source」に「Udon C# Program Asset」を設定したのち、「New Program」をクリックしてください。

<figure>
  <img src="https://assets.mochizuki.moe/udon/getting-started/create-udon-csharp-asset.gif" width="450px" data-zoomable="true">
  <figcaption>「Udon Graph C# Asset」になっていることを確認した上で、「New Program」を押す</figcaption>
</figure>

次に、 `Create Script` ボタンを押して、 UdonSharp スクリプトを作成します。  
ファイル保存ダイアログが出るので、適当な場所にわかりやすい名前で保存してください。

<figure>
  <img src="https://assets.mochizuki.moe/udon/getting-started/create-csharp-script.png" width="450px" data-zoomable="true">
  <figcaption>これを押す</figcaption>
</figure>

保存後、任意のテキストエディターを開いてください。  
無料の場合は [Visual Studio Code](https://code.visualstudio.com/) がオススメですが、お金に余裕がある場合は [JetBrains Rider](https://www.jetbrains.com/rider/) や [Visual Studio](https://visualstudio.microsoft.com/ja/) [(with ReSharper)](https://www.jetbrains.com/ja-jp/resharper/) がオススメです。  
夏猫さんは Visual Studio with ReSharper ですが、 JetBrains Rider 派が多いです。

テキストエディターを開いたら、先ほど保存したファイルを開いてください。  
このとき、上記エディターをインストールしている場合は、ダブルクリックすることで良い感じに開いてくれます。

開いたら、初めは以下のようなコードが書かれています。

```csharp
using UdonSharp;
using UnityEngine;
using VRC.SDKBase;
using VRC.Udon;

public class CubeTransform : UdonSharpBehaviour
{
    void Start()
    {

    }
}
```

ここからは基本的には宗派があったりするのですが、基本的には以下のように書き換えるとベストです。
このとき `Mochizuki.Examples` の部分は、アルファベット、数字、および `.` の好きな名前に置き換えてください。  
基本的には `ショップ名英語.商品名` 等のようにするとよいと思います。  
なぜこれをやった方が良いかというと、他の人が作った UdonSharp スクリプトと名前 (今回の場合は `CubeTransform` という部分) が被ってしまった際、エラーが発生しないようにするためです。

```csharp
using UdonSharp;
using UnityEngine;
using VRC.SDKBase;
using VRC.Udon;

namespace Mochizuki.Examples
{
    public class CubeTransform : UdonSharpBehaviour
    {
        void Start()
        {

        }
    }
}
```

次に、コードを書き換えていきます。  
まずは、使わないイベントを削除し、新しくイベントを定義します。

```csharp
using UdonSharp;
using UnityEngine;
using VRC.SDKBase;
using VRC.Udon;

namespace Mochizuki.Examples
{
    public class CubeTransform : UdonSharpBehaviour
    {
        void FixedUpdate()
        {

        }
    }
}
```

このとき、使えるイベント名はなんでも良いわけではなく、特定の名前である必要があります。  
詳しくは [Unity 公式ドキュメント](https://docs.unity3d.com/2018.4/Documentation/ScriptReference/MonoBehaviour.html)を参照してください。  
VRChat のイベント (Interact など) の場合は以下のように記述します。

```csharp
// 共通部分略
public override void Interact()
{
}
```

次に、変数を定義します。  
今回はすべての値をインスペクターで設定できるようにしたいので、以下のように定義してください。

```csharp
// public class ... のカッコの中に書く
[SerializeField]
private Transform _transform;

[SerializeField]
private Vector3 _axis;

[SerializeField]
private float _angle;
```

変数の定義は `型名 変数名` の用に行います。  
今回の場合は、 `Transform` を受け取るための変数 `_transform` を定義、といったようになります。  
また、 `[SerializeField]` というもの (アトリビュートといいます) を変数に付けることによって、インスペクターから設定可能になります。

最後に、キューブを回転させる処理を記述します。

```csharp
void FixedUpdate()
{
    _transform.Rotate(_axis, _angle);
}
```

これは、 `Transform` という型にある回転するための処理 `Rotate` を、 `_axis` と `_angle` というパラメータで呼ぶ、という意味になります。  
これでコードは完成です。

```csharp
using UdonSharp;
using UnityEngine;
using VRC.SDKBase;
using VRC.Udon;

namespace Mochizuki.Examples
{
    public class CubeTransform : UdonSharpBehaviour
    {
        [SerializeField]
        private float _angle;

        [SerializeField]
        private Vector3 _axis;

        [SerializeField]
        private Transform _transform;

        void FixedUpdate()
        {
            _transform.Rotate(_axis, _angle);
        }
    }
}
```

## インスペクターで設定を行う

最後に、それぞれ設定できるようにした値を、インスペクターから設定します。  
UdonSharp の場合は、 Transform については、自身の値を設定してください。  
その他の値については、好きな値を入力してもかまいませんが、以下のように設定するとわかりやすいです。

<figure>
  <img src="https://assets.mochizuki.moe/udon/getting-started/udon-graph-inspector-value.png" width="450px" data-zoomable="true">
  <figcaption>Udon Graph の場合の設定例</figcaption>
</figure>

<figure>
  <img src="https://assets.mochizuki.moe/udon/getting-started/udon-sharp-inspector-value.png" width="450px" data-zoomable="true">
  <figcaption>UdonSharp の場合の設定例</figcaption>
</figure>

最後に、 Unity Editor にて、再生ボタンを押すと、実際の動作が確認できます。  
お疲れさまでした！

<figure>
  <img src="https://assets.mochizuki.moe/udon/getting-started/first-udon-component.gif" width="450px" data-zoomable="true">
  <figcaption>左が UdonSharp, 右が Udon Graph</figcaption>
</figure>
