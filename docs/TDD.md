  
  
# テスト駆動開発
  
  
## 基本仕様
  
  
## TODOリスト
  
  
+ [x] ~~テストメソッドを呼び出す~~
+ [x] ~~setUpを最初に呼び出す~~
+ [ ] tearDownを後に呼び出す
+ [ ] テストメソッドが失敗したとしてもtearDownを呼び出す
+ [ ] 複数のテストを走らせる
+ [ ] 収集したテスト結果を出力する
  
  
## コアモデル
  

![](assets/4f720d7448016afafbb156e658618f7e0.png?0.9216343363220221)  
  
## `xunit.py`
  
```py
class TestCase:
    def __init__(self, name):
        self.name = name
  
    def setUp(self):
        pass
  
    def run(self):
        self.setUp()
        method = getattr(self, self.name)
        method()
  
  
class WasRun(TestCase):
    def setUp(self):
        self.wasRun = None
        self.wasSetUp = 1
  
    def testMethod(self):
        self.wasRun = 1
  
  
class TestCaseTest(TestCase):
    def setUp(self):
        self.test = WasRun("testMethod")
  
    def testRunning(self):
        self.test.run()
        assert (self.test.wasRun)
  
    def testSetUp(self):
        self.test.run()
        assert(self.test.wasSetUp)
  
  
TestCaseTest("testRunning").run()
TestCaseTest("testSetUp").run()
```  
  