---
markdown:
  image_dir: ./assets
  path: ./TDD.md
  ignore_from_front_matter: true
  absolute_image_path: false
---

# テスト駆動開発

## 基本仕様

## TODOリスト

+ [x] ~~テストメソッドを呼び出す~~
+ [x] ~~setUpを最初に呼び出す~~
+ [x] ~~tearDownを後に呼び出す~~
+ [ ] テストメソッドが失敗したとしてもtearDownを呼び出す
+ [ ] 複数のテストを走らせる
+ [ ] 収集したテスト結果を出力する
+ [x] ~~WasRunで文字列をログに記録する~~


## コアモデル
```puml
class TestCase {
  name
  setUp()
  tearDown()
  run()
}
class WasRun {
  log
  setUp()  
  tearDown()
  testMethod()
}

class TestCaseTest {  
  test
  setUp()
  testTemplateMethod()
}
TestCase <|-- TestCaseTest
TestCase <|-- WasRun
TestCaseTest -> WasRun


```

## `xunit.py`
@import "../tdd/xunit.py"
