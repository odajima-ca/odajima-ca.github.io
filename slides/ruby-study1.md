class: center, middle
# メソッドについて

---

class: center, middle
## インスタンスメソッド

---

class: left, middle
### インスタンスメソッドとは

- 何かしらのクラスのインスタンスから呼び出すメソッド

```ruby
class Foo
  def bar
    :hoge
  end
end

foo = Foo.new
foo.bar
=> :hoge
```

---

class: center, middle
## クラスメソッド

---

class: left, middle
### クラスメソッドとは

- クラスから呼び出すメソッド

```ruby
class Foo
  def self.bar
    :hoge
  end
end

Foo.bar
=> :hoge
```

---

class: center, middle
## 関数的メソッド

---

class: left, middle
### 関数的メソッドとは

- レシーバを省略して呼ばれるメソッド

```ruby
puts 'a'
a
=> nil

print 'a'
a=> nil

p 'a'
"a"
=> "a"
```

---

class: center, middle
### その他に

---
class: left, middle
#### privateメソッド

- クラス内でprivateで定義したメソッド
- これも関数的メソッドになる

```ruby
class Foo
  def bar
    hoge
  end

  private
    def hoge
      :hoge
    end
end

foo = Foo.new
foo.bar
=> :hoge
```

---

class: center, middle
### ちなみに

先ほどの`puts`、`print`、`p`は`Object`クラスのprivateメソッドにあたる

---

class: center, middle
## 特異クラス・特異メソッド

---

class: left, middle
### 特異クラス・特異メソッドとは

- 特定のオブジェクトにしか存在しないクラス
- そのクラスにあるメソッドを`特異メソッド`と呼びます
- 逆に特異クラスは特異メソッドのために存在するクラス

*これについては奥深いので詳細は本など読んでください*

---

class: center, middle
### とりあえずコードで説明すると

---

class: left, middle
### 特異クラスとは

- こんな感じです

```ruby
class Foo
end

Foo.superclass
=> Object

foo = Foo.new
=> #<Foo:0x007fd4291898b8>
foo.class
=> Foo
foo.class.superclass
=> Object

foo.singleton_class
=> #<Class:#<Foo:0x007fd4291898b8>>
foo.singleton_class.superclass
=> Foo
foo.singleton_class.superclass.superclass
=> Object
```

---

class: left, middle
### 特異メソッド

- 特異クラス内で定義されているメソッド
- 定義方法はいくつか方法がある

---

class: left, middle
### 特異メソッド

#### 定義方法１

```ruby
class Foo
end

def Foo.bar
  :HOGE
end

Foo.bar
=> :HOGE

foo = Foo.new

def foo.bar
  :hoge
end

foo.bar
=> :hoge
```

---

class: left, middle
### 特異メソッド

#### 定義方法２

```ruby
class Foo
end

class << Foo
  def bar
    :HOGE
  end
end

Foo.bar
=> :HOGE

foo = Foo.new

class << foo
  def bar
    :hoge
  end
end

foo.bar
=> :hoge
```

---

class: center, middle
## 何がいいたいかというと

---

class: center, middle
### クラスメソッドは特異メソッドである

ということ

頭の片隅に入れておくと、幸せになれるかも

---