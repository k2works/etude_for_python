  
  
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
  

```
ImageMagick is required to be installed to convert svg to png.
Error: Command failed: magick /var/folders/r9/tltm498s7g516t2prbpxr3pw0000gn/T/mume-svg117925-34633-12gz5rw.vx87uy2e29.svg /Users/k2works/Projects/k2works/etude_for_python/docs/assets/4f720d7448016afafbb156e658618f7e0.png
magick: xmlParseComment: invalid xmlChar value 8
 `No such file or directory` @ error/svg.c/SVGError/2680.

```  

  
## `xunit.py`
  
```py
class TestCase:
    def __init__(self, name):
        self.name = name
  
    def setUp(self):
        pass
  
    def tearDown(self):
        pass
  
    def run(self):
        self.setUp()
        method = getattr(self, self.name)
        method()
        self.tearDown()
  
  
class WasRun(TestCase):
    def setUp(self):
        self.log = "setUp "
  
    def testMethod(self):
        self.log = self.log + "testMethod "
  
    def tearDown(self):
        self.log = self.log + "tearDown "
  
  
class TestCaseTest(TestCase):
    def setUp(self):
        self.test = WasRun("testMethod")
  
    def testTemplateMethod(self):
        self.test.run()
        assert("setUp testMethod tearDown " == self.test.log)
  
  
TestCaseTest("testTemplateMethod").run()
```  
  