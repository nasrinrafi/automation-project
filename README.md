# automation-project
#assigment

# -*- coding: utf-8 -*-
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.support.ui import Select
from selenium.common.exceptions import NoSuchElementException
from selenium.common.exceptions import NoAlertPresentException
import unittest, time, re

class AutomationProjectFinal(unittest.TestCase):
    def setUp(self):
        self.driver = webdriver.Firefox()
        self.driver.implicitly_wait(30)
        self.base_url = "https://saucelabs.com/"
        self.verificationErrors = []
        self.accept_next_alert = True
    
    def test_automation_project_final(self):
        driver = self.driver
      #  driver.get(self.base_url)
        driver.get(self.base_url + "/home")
        driver.find_element_by_css_selector("a.hamburger").click()
        driver.find_element_by_css_selector("a[title=\"Resources\"]").click()
        self.assertEqual("Resources", driver.title)
        driver.find_element_by_css_selector("a.hamburger").click()
        driver.find_element_by_css_selector("li.page.pull-left > a[title=\"Pricing\"]").click()
        self.assertEqual("Sauce Labs: Pricing", driver.title)
        driver.find_element_by_css_selector("a.hamburger").click()
        driver.find_element_by_xpath("(//a[contains(text(),'Features')])[3]").click()
        self.assertEqual("Sauce Labs: Features", driver.title)
        driver.find_element_by_css_selector("a.hamburger").click()
        driver.find_element_by_css_selector("li.page.pull-left > a[title=\"Docs\"]").click()
        self.assertEqual("Sauce Labs Docs", driver.title)
        driver.find_element_by_css_selector("button.navbar-toggle").click()
        driver.find_element_by_css_selector("img.sauce-logo-img").click()
        driver.find_element_by_css_selector("a.hamburger").click()
        driver.find_element_by_xpath("(//a[contains(text(),'Company')])[2]").click()
        self.assertEqual("Sauce Labs: Values", driver.title)
        driver.find_element_by_css_selector("a.hamburger").click()
        driver.find_element_by_css_selector("li.page.pull-left > a[title=\"Enterprise\"]").click()
        self.assertEqual("Sauce Labs: Enterprise-grade testing on Sauce", driver.title)
        driver.find_element_by_css_selector("a.hamburger").click()
        driver.find_element_by_css_selector("a[title=\"Open Sauce\"]").click()
        self.assertEqual("Open Sauce", driver.title)
        driver.find_element_by_css_selector("a[title=\"Partners\"]").click()
        self.assertEqual("Partners", driver.title)
        driver.find_element_by_css_selector("a[title=\"Appium\"]").click()
        self.assertEqual("Appium", driver.title)
        driver.find_element_by_css_selector("#signinout > a").click()
        driver.find_element_by_id("username").clear()
        driver.find_element_by_id("username").send_keys("nasrinrafi2000@gmail.com")
        driver.find_element_by_id("password").clear()
        driver.find_element_by_id("password").send_keys("jasmine")
        driver.find_element_by_id("submit").click()
        driver.find_element_by_css_selector("button.btn.btn-navbar").click()
        driver.find_element_by_link_text("Sign up").click()
        driver.find_element_by_id("name").clear()
        driver.find_element_by_id("name").send_keys("mahtabrostami")
        driver.find_element_by_id("email").clear()
        driver.find_element_by_id("email").send_keys("mahtabrostami@yahoo.com")
        driver.find_element_by_id("company").clear()
        driver.find_element_by_id("company").send_keys("iran")
        Select(driver.find_element_by_id("company-size")).select_by_visible_text("2-10")
        driver.find_element_by_id("phone-number").clear()
        driver.find_element_by_id("phone-number").send_keys("4087854678")
        driver.find_element_by_id("password").clear()
        driver.find_element_by_id("password").send_keys("mahtab")
        driver.find_element_by_id("submit-button").click()
    
    def is_element_present(self, how, what):
        try: self.driver.find_element(by=how, value=what)
        except NoSuchElementException, e: return False
        return True
    
    def is_alert_present(self):
        try: self.driver.switch_to_alert()
        except NoAlertPresentException, e: return False
        return True
    
    def close_alert_and_get_its_text(self):
        try:
            alert = self.driver.switch_to_alert()
            alert_text = alert.text
            if self.accept_next_alert:
                alert.accept()
            else:
                alert.dismiss()
            return alert_text
        finally: self.accept_next_alert = True
    
    def tearDown(self):
        self.driver.quit()
        self.assertEqual([], self.verificationErrors)

if __name__ == "__main__":
    unittest.main()
