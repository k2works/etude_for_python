  
  
# テスト駆動開発
  
  
## 基本仕様
  
  
## TODOリスト
  
  
+ [x] ~~テストメソッドを呼び出す~~
+ [x] ~~setUpを最初に呼び出す~~
+ [x] ~~tearDownを後に呼び出す~~
+ [ ] テストメソッドが失敗したとしてもtearDownを呼び出す
+ [ ] 複数のテストを走らせる
+ [x] ~~収集したテスト結果を出力する~~
+ [x] ~~WasRunで文字列をログに記録する~~
  
  
## コアモデル
  

```
ImageMagick is required to be installed to convert svg to png.
Error: Command failed: magick /var/folders/r9/tltm498s7g516t2prbpxr3pw0000gn/T/mume-svg117925-34633-ulumir.mr2d927qfr.svg /Users/k2works/Projects/k2works/etude_for_python/assets/7f51d579f1e287ad1c2d16b6690ec7be0.png
magick: xmlParseComment: invalid xmlChar value 8
 `No such file or directory` @ error/svg.c/SVGError/2680.

```  

  
## `xunit.py`
  
```py
class TestResult:
    def __init__(self):
        self.runCount = 0
  
    def testStarted(self):
        self.runCount = self.runCount + 1
  
    def summary(self):
        return "1 run, 0 failed"
  
class TestCase:
    def __init__(self, name):
        self.name = name
  
    def setUp(self):
        pass
  
    def tearDown(self):
        pass
  
    def run(self):
        result = TestResult()
        result.testStarted()
        self.setUp()
        method = getattr(self, self.name)
        method()
        self.tearDown()
        return result
  
  
class WasRun(TestCase):
    def setUp(self):
        self.log = "setUp "
  
    def testMethod(self):
        self.log = self.log + "testMethod "
  
    def testBrokenMethod(self):
        raise Exception
  
    def tearDown(self):
        self.log = self.log + "tearDown "
  
  
class TestCaseTest(TestCase):
    def setUp(self):
        self.test = WasRun("testMethod")
  
    def testTemplateMethod(self):
        self.test.run()
        assert("setUp testMethod tearDown " == self.test.log)
  
    def testResult(self):
        test = WasRun("testMethod")
        result = test.run()
        assert("1 run, 0 failed" == result.summary())
  
    def testFailedResult(self):
        test = WasRun("testBrokenMethod")
        result = test.run()
        assert("1 run, 1 failed" == result.summary())
  
  
TestCaseTest("testTemplateMethod").run()
TestCaseTest("testResult").run()
# TestCaseTest("testFailedResult").run()
```  
  