ViewModel

## 概要

画面の回転などの要因により、再生成されるオブジェクト等を破棄されないように保持する作り

## Issue

### viewmodel has no zero argument constructor

生成対象のViewModelが引数0のコンストラクタを持っていないよ。自動生成出来ないよ。というお話  
独自のFactoryクラスをつくって、そこで対応させる

```kotlin

class TestModel( val fragment: Fragment ): ViewModel() {

    class Factory( val fragment: Fragment ): ViewModelProvider.NewInstanceFactory() {
        override fun <T : ViewModel?> create(modelClass: Class<T>): T {
            return TestModel( fragment ) as T
        }
    }
}

// 利用するときは、
val testModel: TestModel by viewModel { TestModel.Factory( fragment ) }
```
