  
  
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
  

![](assets/4f720d7448016afafbb156e658618f7e0.png?0.721972493913489)  
  
## `xunit.py`
  
```py
class TestCase:
    def __init__(self, name):
        self.name = name
  
    def run(self):
        method = getattr(self, self.name)
        method()
  
  
class WasRun(TestCase):
    def __init__(self, name):
        self.wasRun = None
        super().__init__(name)
  
    def testMethod(self):
        self.wasRun = 1
  
  
class TestCaseTest(TestCase):
    def testRunning(self):
        test = WasRun("testMethod")
        assert (not test.wasRun)
        test.run()
        assert (test.wasRun)
  
  
TestCaseTest("testRunning").run()
  
```  
  