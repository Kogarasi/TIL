# Data Binding

### 説明

レイアウトとコードの関連付け機能
コード側でfindViewByIdをせずに済むようにする仕組み
各種Bindingを利用することで、簡単にViewにアクセス出来るようになる

### 使い方

**layout**タグで括る
その下にいつもと同じように配置していく

```xml
<?xml version="1.0" encoding="utf-8"?>
<layout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        xmlns:tools="http://schemas.android.com/tools">

    <androidx.constraintlayout.widget.ConstraintLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            tools:context=".MainActivity">

        <fragment
                android:name="androidx.navigation.fragment.NavHostFragment"
                android:layout_width="match_parent"
                android:layout_height="match_parent" app:navGraph="@navigation/nav_graph" app:defaultNavHost="true"
                android:id="@+id/fragment"/>
    </androidx.constraintlayout.widget.ConstraintLayout>
</layout>
```

コード側

Activityで利用する場合は**DataBindingUtil**を使う

```kotlin
DataBindingUtil.setContentView<ActivityMainBinding>( this, R.layout.activity_main )
```

Fragmentで利用する場合は各種バインディングクラスからbindして利用する

```kotlin
FragmentTopBinding.bind( view )
```
