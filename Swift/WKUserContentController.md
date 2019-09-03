# WKUserContentController

## WKScriptMessage

WKScriptMessage周りが面倒だったので、ちょくちょくライブラリ化していく。

message.bodyにはSDK側でよしなにしたStringなりFrozenDictionaryなりが飛んでくる。
渡すときにJSON.stringifyしてから渡すと受け取り側でjson: Stringってまとめて受け取ってよしなに出来るのでよさそう。
後は、細かいルーティングを良い感じにする方法を見つけたい

## BlueCompass

上のライブラリ化しました！！

BlueCompass(https://github.com/Kogarasi/BlueCompass)
