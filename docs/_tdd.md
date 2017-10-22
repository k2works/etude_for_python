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
+ [ ] setUpを最初に呼び出す
+ [ ] tearDownを後に呼び出す
+ [ ] テストメソッドが失敗したとしてもtearDownを呼び出す
+ [ ] 複数のテストを走らせる
+ [ ] 収集したテスト結果を出力する


## コアモデル
```puml
class TestCase {
  name
  run()
}
class WasRun {
  wasRun  
  name
  testMethod()
}

class TestCaseTest {
  testRunning()
}
TestCaseTest -> WasRun
TestCase <|-- WasRun


```

## `xunit.py`
@import "../tdd/xunit.py"
