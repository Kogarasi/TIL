* flatMap

subscribeが重なってしまうのを避けられる。

```swift
button.rx.tap.subscribe { _ in
  load.subscribe { in
    ...
  }
}
```

みたいなコードが対象

```swift
button.rx.tap.flatMap { _ in
  return load
}.subscribe { in
  ...
}
```

的な感じかな？
