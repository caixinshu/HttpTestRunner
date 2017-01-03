# HttpTestRunner
# coding: utf-8
import sys
default_encoding = 'utf-8'
if sys.getdefaultencoding() != default_encoding:
    reload(sys)
    sys.setdefaultencoding(default_encoding)
'''这一坨我也不知道什么意思，但是解决ASCII  code can't decode byte 0xe9 in position 5627: ordinal not in range(128)'''
import unittest
import HTMLTestRunner
from selenium import webdriver
class Baidu(unittest.TestCase):
    @classmethod
    def setUpClass(cls):
        cls.driver = webdriver.Firefox()
        # cls.driver.maximize_window()
        cls.driver.implicitly_wait(30)
        cls.driver.get("http://www.baidu.com/")
    def test_001(cls):
        '''验证title是否正确'''
        cls.assertEqual(u'百度一下，你就知道', cls.driver.title)
    #@unittest.skip(u'不想跑额')
    def test_002(self):
        '''验证url是否正确'''
        self.assertEqual("https://www.baidu.com/",self.driver.current_url)
    @classmethod
    def tearDownClass(cls):
        cls.driver.quit()
if __name__=='__main__':
    suite=unittest.TestSuite()
    suite.addTest(Baidu('test_001'))
    filename="C:\Users\XM\PycharmProjects\untitled3\\test\\result.html"
    fp=file(filename,'wb')
    runner=HTMLTestRunner.HTMLTestRunner(stream=fp,title='Result',description='Test_report')
    runner.run(suite)
