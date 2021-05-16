# Unity のイベント

Udon で使える Unity のイベントについて、使い方のサンプルとともに解説しています。  
イベントの種類については、[こちらのページ](/getting-started/kinds-of-event)を参照してください。

## FixedUpdate

`FixedUpdate` イベントは、一定周期毎 (Unity 時間) に 1 回だけ呼ばれるイベントです。  
物理演算などの処理をこのイベントで処理することで、スムーズに見せることが出来ます。

<!-- prettier-ignore-start -->
!!! example "イベントサンプル"

    ここでは、指定した Transform コンポーネントを回転させるだけのサンプルを記載しています。

    === "Udon Graph"

        <img src="https://assets.mochizuki.moe/udon/references/udon-graph-images/fixed-update.png" width="400px" data-zoomable="true">

        [Udon Graph サンプルをダウンロード](https://assets.mochizuki.moe/udon/references/udon-graph-packages/FixedUpdateReferenceSample.unitypackage){ .md-button .md-button--primary }

    === "UdonSharp"

        ```csharp
        using UdonSharp;

        using UnityEngine;

        namespace NatsunekoLaboratory.Examples
        {
            public class CubeTransform : UdonSharpBehaviour
            {
                [SerializeField]
                private float _angle;

                [SerializeField]
                private Vector3 _axis;

                [SerializeField]
                private Transform _transform;

                private void FixedUpdate()
                {
                    _transform.Rotate(_axis, _angle);
                }
            }
        }
        ```

    === "実行結果"

        <img src="https://assets.mochizuki.moe/udon/references/udon-graph-videos/fixed-update.gif" width="400px" data-zoomable="true">

<!-- prettier-ignore-end -->

