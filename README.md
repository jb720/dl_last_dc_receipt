#! python3
# dl_last_dc_receipt.py downloads my latest datacamp invoice

from selenium import webdriver
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.common.action_chains import ActionChains
import time

# login and password 
login = '___'
password = '___'

# Chrome
browser = webdriver.Chrome(executable_path=r'/Users/magento/Desktop/fun_py_stuff/chromedriver')

# Open datacamp.com in new chrome window 
browser.get('https://www.datacamp.com')

# Open sign in page
browser.find_element_by_css_selector('.header__nav-link.js-modal-open').click()

# wait for page to load
time.sleep(3)

# Find login field and enter email
em = browser.find_element_by_css_selector('.dc-input-group__input.dc-input--text.js-sign-in-email')
em.send_keys(login)
em.send_keys(Keys.TAB)

# TAB to password field
actions = ActionChains(browser)
actions.send_keys(password)

# TAB to sign in button
actions.send_keys((Keys.TAB) * 2)
actions.send_keys(Keys.RETURN)
actions.perform()

# wait for page to load
time.sleep(3)

# Navigate to subscription page
browser.find_element_by_class_name('header-user').click()
browser.find_element_by_class_name('nav-user__email').click()

# wait for page to load
time.sleep(3)

# Go to payments page
browser.find_element_by_link_text('Payments').click()

# Wait and download the last pdf
time.sleep(3)
invoices = browser.find_elements_by_link_text('PDF')
last = invoices[-1]
last.click()
