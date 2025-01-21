# aitasks
🚀 AITasks: AI-Powered Digital Marketing Automation! 💡 Streamline campaigns on Facebook, Google, TikTok with cutting-edge AI tools. From content creation to ad optimization, AITasks saves time, boosts ROI, and elevates strategies.  ✨ Why AITasks? ✅ AI automation ✅ Cross-platform integration ✅ Smart analytics ✅ Customizable bots 
import requests
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
import time
import requests
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
import time
import logging
import openai  # For AI content generation
import pandas as pd  # For analytics
from datetime import datetime

# Constants
OPENAI_API_KEY = "your_openai_api_key"
FACEBOOK_EMAIL = "your_facebook_email"
FACEBOOK_PASSWORD = "your_facebook_password"
INSTAGRAM_EMAIL = "your_instagram_email"
INSTAGRAM_PASSWORD = "your_instagram_password"
LINKEDIN_EMAIL = "your_linkedin_email"
LINKEDIN_PASSWORD = "your_linkedin_password"
TWITTER_EMAIL = "your_twitter_email"
TWITTER_PASSWORD = "your_twitter_password"

# Configure logging
logging.basicConfig(filename="aitasks.log", level=logging.INFO, format="%(asctime)s - %(levelname)s - %(message)s")

# Initialize OpenAI
openai.api_key = OPENAI_API_KEY

# AI Bot Class
class AITasksBot:
    def __init__(self):
        self.driver = webdriver.Chrome()  # Ensure you have ChromeDriver installed
        self.analytics_data = []

    def generate_ai_content(self, prompt):
        """Generate AI-powered content using OpenAI's GPT."""
        try:
            response = openai.Completion.create(
                engine="text-davinci-003",
                prompt=prompt,
                max_tokens=100,
                n=1,
                stop=None,
                temperature=0.7,
            )
            return response.choices[0].text.strip()
        except Exception as e:
            logging.error(f"Error generating AI content: {e}")
            return None

    def login_to_facebook(self):
        """Log in to Facebook and post a status update."""
        try:
            self.driver.get("https://www.facebook.com")
            time.sleep(2)

            email = self.driver.find_element_by_id("email")
            email.send_keys(FACEBOOK_EMAIL)

            password = self.driver.find_element_by_id("pass")
            password.send_keys(FACEBOOK_PASSWORD)
            password.send_keys(Keys.RETURN)

            time.sleep(5)
            logging.info("Logged in to Facebook successfully!")

            # Generate AI content
            prompt = "Write a catchy Facebook post about AI in digital marketing."
            post_content = self.generate_ai_content(prompt)

            if post_content:
                status_box = self.driver.find_element_by_xpath("//*[@name='xhpc_message']")
                status_box.send_keys(post_content)
                time.sleep(2)
                self.driver.find_element_by_xpath("//*[@data-testid='react-composer-post-button']").click()
                logging.info("Status updated on Facebook!")
                self.analytics_data.append({"platform": "Facebook", "action": "post", "timestamp": datetime.now()})
        except Exception as e:
            logging.error(f"Error in Facebook login or posting: {e}")

    def login_to_instagram(self):
        """Log in to Instagram and post a photo with AI-generated caption."""
        try:
            self.driver.get("https://www.instagram.com/accounts/login/")
            time.sleep(2)

            email = self.driver.find_element_by_name("username")
            email.send_keys(INSTAGRAM_EMAIL)

            password = self.driver.find_element_by_name("password")
            password.send_keys(INSTAGRAM_PASSWORD)
            password.send_keys(Keys.RETURN)

            time.sleep(5)
            logging.info("Logged in to Instagram successfully!")

            # Generate AI caption
            prompt = "Write a creative Instagram caption for a digital marketing post."
            caption = self.generate_ai_content(prompt)

            if caption:
                # Add logic to upload a photo and set caption
                logging.info(f"AI-generated caption: {caption}")
                self.analytics_data.append({"platform": "Instagram", "action": "post", "timestamp": datetime.now()})
        except Exception as e:
            logging.error(f"Error in Instagram login or posting: {e}")

    def login_to_linkedin(self):
        """Log in to LinkedIn and post an update."""
        try:
            self.driver.get("https://www.linkedin.com/login")
            time.sleep(2)

            email = self.driver.find_element_by_id("username")
            email.send_keys(LINKEDIN_EMAIL)

            password = self.driver.find_element_by_id("password")
            password.send_keys(LINKEDIN_PASSWORD)
            password.send_keys(Keys.RETURN)

            time.sleep(5)
            logging.info("Logged in to LinkedIn successfully!")

            # Generate AI content
            prompt = "Write a professional LinkedIn post about AI in marketing."
            post_content = self.generate_ai_content(prompt)

            if post_content:
                self.driver.get("https://www.linkedin.com/feed/")
                time.sleep(2)
                post_box = self.driver.find_element_by_xpath("//*[@aria-label='Start a post']")
                post_box.send_keys(post_content)
                time.sleep(2)
                self.driver.find_element_by_xpath("//*[@data-control-name='share.post']").click()
                logging.info("Post updated on LinkedIn!")
                self.analytics_data.append({"platform": "LinkedIn", "action": "post", "timestamp": datetime.now()})
        except Exception as e:
            logging.error(f"Error in LinkedIn login or posting: {e}")

    def login_to_twitter(self):
        """Log in to Twitter and post a tweet."""
        try:
            self.driver.get("https://twitter.com/login")
            time.sleep(2)

            email = self.driver.find_element_by_name("session[username_or_email]")
            email.send_keys(TWITTER_EMAIL)

            password = self.driver.find_element_by_name("session[password]")
            password.send_keys(TWITTER_PASSWORD)
            password.send_keys(Keys.RETURN)

            time.sleep(5)
            logging.info("Logged in to Twitter successfully!")

            # Generate AI content
            prompt = "Write a short and engaging tweet about AI in digital marketing."
            tweet_content = self.generate_ai_content(prompt)

            if tweet_content:
                tweet_box = self.driver.find_element_by_xpath("//*[@aria-label='Tweet text']")
                tweet_box.send_keys(tweet_content)
                time.sleep(2)
                self.driver.find_element_by_xpath("//*[@data-testid='tweetButton']").click()
                logging.info("Tweet posted on Twitter!")
                self.analytics_data.append({"platform": "Twitter", "action": "post", "timestamp": datetime.now()})
        except Exception as e:
            logging.error(f"Error in Twitter login or posting: {e}")

    def generate_analytics_report(self):
        """Generate an analytics report from collected data."""
        try:
            df = pd.DataFrame(self.analytics_data)
            df.to_csv("analytics_report.csv", index=False)
            logging.info("Analytics report generated successfully!")
        except Exception as e:
            logging.error(f"Error generating analytics report: {e}")

    def close(self):
        """Close the browser."""
        self.driver.quit()

# Main Function
if __name__ == "__main__":
    bot = AITasksBot()
    try:
        bot.login_to_facebook()
        bot.login_to_instagram()
        bot.login_to_linkedin()
        bot.login_to_twitter()
        bot.generate_analytics_report()
    except Exception as e:
        logging.error(f"Error in main execution: {e}")
    finally:
        bot.close()
