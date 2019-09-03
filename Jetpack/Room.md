# Room

## 説明

便利になって帰ってきたSQLite的な（全然違う）

## 使い方

* 前準備に3つクラスを作ります
* 非同期じゃないとダメなので、CoroutineもしくはRx辺りを利用する

**Entity**

* 1行ごとのデータ構造

```kotlin
@Entity
data class EntityName {
  @PrimaryKey
  var id: Int;
  
  var name: String;
  var anyanyany: String;
}
```

**DAO**

* SQL文をまとめて書くところみたいな感じ

```kotlin
@Dao
interface EntityNamePlusDAO {

  @Insert
  suspend fun insert( entity: EntityName );
  
  @Delete
  suspend fun delete( entity: EntityName );
  
  @Query( "SELECT * FROM :tableName" )
  suspend fun any();
}
```

**Database**

* 利用する物をまとめて書く。
* Databaseクラスをもとに利用する

```kotlin
@Database( entities = [ EntityName::class ], version = 1 )
abstract class AppDatabase: RoomDatabase() {
  abstract fun entityNameDao: EntityNamePlusDao
}
```
