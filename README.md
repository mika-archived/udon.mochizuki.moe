# udon.mochizuki.moe

ブログに書いても良いんだけど、ブログに書くと私が身バレ (もう遅い) するのでサイトを分けるのだ。  
Udon および UdonSharp の情報を書いてるサイト。  
誰でも追記・修正歓迎。

## Development

開発方法について。

### Raw

GitHub でいじって、そのままプレビューを見ながらプルリクエストを投げつけてください。  
下記のどっちかについて詳しい人が直してくれます。

### Local Python

以下のコマンドを実行してください。

```bash
$ pip3 install -r requirements.txt
$ mkdocs serve
```

### Docker

環境を汚したくない人は Docker がオススメです。

```bash
$ docker build --tag natsuneko/udon-mochizuki-moe .
$ docker run --rm -it --publish 8000:8000 --volume "$(pwd):/docs" natsuneko/udon-mochizuki-moe
```

## License

CC-BY-4.0 International by [@6jz](https://twitter.com/6jz)
