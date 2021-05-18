# 基本構文

ここでは、 Udon ギミックを組むために必要な Udon Graph および UdonSharp の基本的な考え方について説明しています。

## 共通の考え方・処理

ある程度複雑なギミックを組むためには、処理の種類を把握しておくことで、スムーズにかつより短いノード・コードでギミックをくみ上げることが可能になります。  
このセクションでは、 Udon Graph と UdonSharp の共通で存在する処理の種類について解説していきます。

### 型

型とは、わかりやすく言えば「どのようなデータを持っているか」についての種類を表したものです。  
Unity でよく出てくる例で言えば、 Transform 型というものがあり、これにはどの位置か、どの角度か、大きさはどれくらいか、といったデータが含まれています。  
また、型にはそのデータに関連する処理も含まれていて、[初めての Udon コンポーネント](/getting-started/your-first-udon-component/)で使った `Rotate` などがそれに当たり、一般的には「メソッド」や「関数」と呼ばれます。  
メソッドについては、数学の関数をイメージするとわかりやすいかもしれません (ある入力 A にたいして、一定の結果 B を出力する)。

Udon や UdonSharp では、型は通常以下のように表示されます。

<!-- prettier-ignore-start -->
=== "Udon Graph"

    変数の型は以下の丸で囲まれている部分に記載されている。

    <img src="https://assets.mochizuki.moe/udon/references/udon-graph-images/types-in-udon-graph-1.png" width="250px" data-zoomable="true">

    また、メソッドの型は、以下の丸で囲まれている部分に記載されている。

    <img src="https://assets.mochizuki.moe/udon/references/udon-graph-images/types-in-udon-graph-2.png" width="250px" data-zoomable="true">

=== "UdonSharp"

    ```csharp
    using UnityEngine;

    namespace NatsunekoLaboratory.Examples
    {
        // TestClass も型
        public class TestClass
        {
            private float _a; // この場合は、変数名 (_a) の左にある部分が型を表している

            // 下記の `void` という部分も戻り値(計算結果)の型を示している
            private void FixedUpdate()
            {
                transform.Rotate(/* ... */); // この場合は、エディター上で `transform` にマウスカーソルを持って行くと、型情報がホバーされる
            }
        }
    }
    ```
<!-- prettier-ignore-end -->

また、ある特定の型を複数まとめたものを「配列」と呼び、変数名に `[]` と言ったものが付く。  
例えば、 `float[]` の場合は、 `float` という型が複数集まったものを指します。

<!-- prettier-ignore-start -->
??? info "Tips - 型エイリアス"
    Udon や UdonSharp (C#) では、型エイリアスという別名が存在しており、以下の型は、表記が異なる場合があります。  
    例えば、上記の例として出してある Udon Graph では、変数の型 `float` とメソッドの型 `Single` は同じものを指しています。

    | 元の型 | エイリアス名 (別名) |
    | --------- | ---------- |
    | `Boolean` | `bool`     |
    | `Byte`    | `byte`     |
    | `SByte`   | `sbyte`    |
    | `Char`    | `char`     |
    | `Decimal` | `decimal`  |
    | `Double`  | `double`   |
    | `Single`  | `float`    |
    | `Int32`   | `int`      |
    | `UInt32`  | `uint`     |
    | `Int64`   | `long`     |
    | `UInt64`  | `ulong`    |
    | `Int16`   | `short`    |
    | `UInt16`  | `ushort`   |
    | `Object`  | `object`   |
    | `String`  | `string`   |
    | `Void`    | `void`     |

<!-- prettier-ignore-end -->

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

<!-- prettier-ignore-end -->

ただし、通常の場合は四則演算は同じ型同士でのみ行えます。  
多くの場合はそれで十分なのですが、それ以外の場合は、それ専用の関数が用意されていますので、そちらを使うようにすると、計算が行えます。

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

### ブロック

ブロック (Block) は、1 つ以上のいくつかの処理をまとめたもの (コードブロック) を指します。  
Udon では、同名のノードが存在していますが、どちらかというとグループ機能がより近いものとなります。

<!-- prettier-ignore-start -->
=== "Udon Graph"

    <img src="https://assets.mochizuki.moe/udon/references/udon-graph-images/block-statement.png" width="400px" data-zoomable="true">

=== "UdonSharp"

    ```csharp
    // { } で囲まれている部分がブロックとして見なされる
    {
        // なんらかの処理
    }
    ```


<!-- prettier-ignore-end -->

### 条件分岐

例えば、プレイヤーが自分だったらある特定の処理を行いたい、それ以外の場合は無視したい、といった場合は、条件分岐というものを行う必要があります。  
条件分岐は、条件を満たした場合 (True となった場合) は特定の処理を行う、もしくはその逆、条件を満たさなかった場合 (False) は特定の処理を行う、といったものを記述できます。

<!-- prettier-ignore-start -->
=== "Udon Graph"

    下記は `Equals` ノードの結果が `False` であれば、 `Set Tracking` ノードを実行する。  
    `Branch` ノードの `bool` の値が正しいものであれば `True` が、それ以外の場合は `False` が実行される。

    <img src="https://assets.mochizuki.moe/udon/references/udon-graph-images/conditional-statement.png" width="450px" data-zoomable="true">

=== "UdonSharp"

    ```csharp
    public override void Interact()
    {
        var player = Networking.LocalPlayer;

        if (player == null)
        {
            // 条件を満たした場合の処理
        }
        else
        {
            // 条件を満たさなかった場合の処理
            // else 以降は、必要が無ければ省略することが出来る
        }
    }
    ```


<!-- prettier-ignore-end -->

