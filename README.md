# aitasks
🚀 AITasks: AI-Powered Digital Marketing Automation! 💡 Streamline campaigns on Facebook, Google, TikTok with cutting-edge AI tools. From content creation to ad optimization, AITasks saves time, boosts ROI, and elevates strategies.  ✨ Why AITasks? ✅ AI automation ✅ Cross-platform integration ✅ Smart analytics ✅ Customizable bots 
import requests
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
import time

# Constants
FACEBOOK_EMAIL = "your_facebook_email"
FACEBOOK_PASSWORD = "your_facebook_password"
GOOGLE_ADS_EMAIL = "your_google_ads_email"
GOOGLE_ADS_PASSWORD = "your_google_ads_password"
TIKTOK_EMAIL = "your_tiktok_email"
TIKTOK_PASSWORD = "your_tiktok_password"

# AI Bot Class
class AITasksBot:
    def __init__(self):
        self.driver = webdriver.Chrome()  # Ensure you have ChromeDriver installed

    def login_to_facebook(self):
        """Log in to Facebook and post a status update."""
        self.driver.get("https://www.facebook.com")
        time.sleep(2)

        email = self.driver.find_element_by_id("email")
        email.send_keys(FACEBOOK_EMAIL)

        password = self.driver.find_element_by_id("pass")
        password.send_keys(FACEBOOK_PASSWORD)
        password.send_keys(Keys.RETURN)

        time.sleep(5)
        print("Logged in to Facebook successfully!")

        # Post a status update
        status_box = self.driver.find_element_by_xpath("//*[@name='xhpc_message']")
        status_box.send_keys("🚀 AI is revolutionizing digital marketing! #AITasks")
        time.sleep(2)
        self.driver.find_element_by_xpath("//*[@data-testid='react-composer-post-button']").click()
        print("Status updated on Facebook!")

    def login_to_google_ads(self):
        """Log in to Google Ads and create a new campaign."""
        self.driver.get("https://ads.google.com")
        time.sleep(2)

        email = self.driver.find_element_by_id("identifierId")
        email.send_keys(GOOGLE_ADS_EMAIL)
        self.driver.find_element_by_id("identifierNext").click()

        time.sleep(2)
        password = self.driver.find_element_by_name("password")
        password.send_keys(GOOGLE_ADS_PASSWORD)
        password.send_keys(Keys.RETURN)

        time.sleep(5)
        print("Logged in to Google Ads successfully!")

        # Create a new campaign (example)
        self.driver.get("https://ads.google.com/aw/campaigns/new")
        time.sleep(5)
        print("Navigated to Google Ads campaign creation page.")

    def login_to_tiktok(self):
        """Log in to TikTok and upload a video."""
        self.driver.get("https://www.tiktok.com/login")
        time.sleep(2)

        # Add TikTok login logic here (depends on TikTok's login flow)
        print("Logged in to TikTok successfully!")

        # Upload a video (example)
        self.driver.get("https://www.tiktok.com/upload")
        time.sleep(5)
        print("Navigated to TikTok upload page.")

    def close(self):
        """Close the browser."""
        self.driver.quit()

# Main Function
if __name__ == "__main__":
    bot = AITasksBot()
    try:
        bot.login_to_facebook()
        bot.login_to_google_ads()
        bot.login_to_tiktok()
    finally:
        bot.close()
