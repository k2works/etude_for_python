  
  
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
  

![](assets/4f720d7448016afafbb156e658618f7e0.png?0.8500021906420505)  
  
## `xunit.py`
  
```py
class TestResult:
    def __init__(self):
        self.runCount = 0
        self.errorCount = 0
  
    def testStarted(self):
        self.runCount = self.runCount + 1
  
    def testFailed(self):
        self.errorCount = self.errorCount + 1
  
    def summary(self):
        return "%d run, %d failed" % (self.runCount, self.errorCount)
  
class TestCase:
    def __init__(self, name):
        self.name = name
  
    def setUp(self):
        pass
  
    def tearDown(self):
        pass
  
    def run(self, result):
        result.testStarted()
        self.setUp()
        try:
            method = getattr(self, self.name)
            method()
        except:
            result.testFailed()
        self.tearDown()
  
class TestSuite:
    def __init__(self):
        self.tests = []
  
    def add(self, test):
        self.tests.append(test)
  
    def run(self, result):
        for test in self.tests:
            test.run(result)
  
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
        self.result = TestResult()
  
    def testTemplateMethod(self):
        test = WasRun("testMethod")
        test.run(self.result)
        assert("setUp testMethod tearDown " == test.log)
  
    def testResult(self):
        test = WasRun("testMethod")
        test.run(self.result)
        assert("1 run, 0 failed" == self.result.summary())
  
    def testFailedResult(self):
        test = WasRun("testBrokenMethod")
        test.run(self.result)
        assert("1 run, 1 failed" == self.result.summary())
  
    def testFailedResultFormatting(self):
        self.result.testStarted()
        self.result.testFailed()
        assert("1 run, 1 failed" == self.result.summary())
  
    def testSuite(self):
        suite = TestSuite()
        suite.add(WasRun("testMethod"))
        suite.add(WasRun("testBrokenMethod"))
        suite.run(self.result)
        assert("2 run, 1 failed" == self.result.summary())
  
suite = TestSuite()
suite.add(TestCaseTest("testTemplateMethod"))
suite.add(TestCaseTest("testResult"))
suite.add(TestCaseTest("testFailedResult"))
suite.add(TestCaseTest("testFailedResultFormatting"))
suite.add(TestCaseTest("testSuite"))
result = TestResult()
suite.run(result)
print(result.summary())
```  
  