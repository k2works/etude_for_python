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
+ [x] ~~複数のテストを走らせる~~
+ [x] ~~収集したテスト結果を出力する~~
+ [x] ~~WasRunで文字列をログに記録する~~
+ [x] ~~失敗したテストを出力する~~
+ [ ] setUpのエラーをキャッチして出力する
+ [ ] TestCaseクラスからTestSuiteを作る

## コアモデル
```puml
class TestResult {
  runCount
  errorCount
  testStarted()
  testFailed()
}
class TestCase {
  name
  setUp()
  tearDown()
  run()
}
class WasRun {
  log
  setUp()  
  testMethod()
  testBrokenMethod()
  tearDown()
}
class TestCaseTest {  
  result
  setUp()
  testTemplateMethod()
  testResult()
  testFailedResult()
  testFailedResultFormatting()
  testSuite()
}
class TestSuite {
  tests
  add()
  run()
}
TestCase <|-- TestCaseTest
TestCase <|-- WasRun
TestCaseTest -> WasRun
TestCase -> TestResult
TestSuite o--r TestCaseTest
TestSuite --> TestResult
```

## `xunit.py`
@import "../tdd/xunit.py"
