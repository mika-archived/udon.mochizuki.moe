# 基本構文

ここでは、 Udon ギミックを組むために必要な Udon Graph および UdonSharp の基本的な考え方について説明しています。

## 共通の考え方・処理

ある程度複雑なギミックを組むためには、処理の種類を把握しておくことで、スムーズにかつより短いノード・コードでギミックをくみ上げることが可能になります。  
このセクションでは、 Udon Graph と UdonSharp の共通で存在する処理の種類について解説していきます。

### 型

型とは、わかりやすく言えば「どのようなデータを持っているか」についての種類を表したものです。  
Unity でよく出てくる例で言えば、 Transform 型というものがあり、これにはどの位置か、どの角度か、大きさはどれくらいか、といったデータが含まれています。  
また、型にはそのデータに関連するための処理も含まれていて、[初めての Udon コンポーネント](/getting-started/your-first-udon-component/)で使った `Rotate` などがそれに当たり、一般的には「メソッド」や「関数」と呼ばれます。  
数学の関数をイメージするとわかりやすいかもしれませんね (ある入力 A にたいして、一定の結果 B を出力する)。

### 四則演算

大雑把なことを言えば、 Udon のギミックとは、基本的にはすべて四則演算、つまりは何らかの値を加工する処理の塊で出来ていると言っても過言ではありません。  
単純な例である足し算、引き算、かけ算、割り算を例にすると、下記のように処理を書きます。

<!-- prettier-ignore-start -->
=== "Udon Graph"

    <img src="https://assets.mochizuki.moe/udon/references/udon-graph-images/value-calculation.png" data-zoomable="true">

    [Udon Graph サンプルをダウンロード](https://assets.mochizuki.moe/udon/references/udon-graph-packages/ValueCalculationReferenceSample.unitypackage){ .md-button .md-button--primary }


=== "UdonSharp"

    ```csharp
    using UdonSharp;

    using UnityEngine;

    namespace NatsunekoLaboratory.Examples
    {
        public class ValueCalculation : UdonSharpBehaviour
        {
            [SerializeField]
            private float _a;

            [SerializeField]
            private float _b;

            private void Start()
            {
                // 足し算
                var value1 = _a + _b;
                Debug.Log(value1);

                // 引き算
                var value2 = _a + _b;
                Debug.Log(value2);

                // かけ算
                var value3 = _a * _b;
                Debug.Log(value3);

                // 割り算
                var value4 = _a / _b;
                Debug.Log(value4);
            }
        }
    }
    ```

ただし、通常の場合は四則演算は同じ型同士でのみ行えます。  
多くの場合はそれで十分なのですが、それ以外の場合は、それ専用の関数が用意されていますので、そちらを使うようにすると、計算が行えます。

<!-- prettier-ignore-end -->

### コメント

何らかの複雑な処理を行った場合や、ちょっとしたメモ書きや注意事項などを、「コメント」として、 Udon Graph や UdonSharp コードの中に残すことが出来ます。  
このコメントは、 Udon Graph や UdonSharp コードの中には存在しますが、なんらかの処理として実行されることはないので、好きなことを書くことが出来ます。  
基本的には、先ほど述べたようなことをこまめに書いておくと、後から見直すときなどに役立ちます。  
これは、ある程度の人は 1 ヶ月前に書いた自分の Udon Graph や UdonSharp コードなんぞ見てもわからないことが発生することがあるからです。

以下に Udon Graph と UdonSharp でのコメントの書き方を載せています。

<!-- prettier-ignore-start -->
=== "Udon Graph"

    <img src="https://assets.mochizuki.moe/udon/references/udon-graph-videos/comment.gif" data-zoomable="true">

=== "UdonSharp"

    ```csharp
    // この行はコメントとして扱われる
    /* この範囲だけがコメントとして扱われる */
    ```


<!-- prettier-ignore-end -->

