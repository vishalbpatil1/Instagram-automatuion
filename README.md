# Instagram-automatuion
In this repo, we will design a simple fun project “Instagram Bot” using Python and instabot . As beginners want to do some extra and learning small projects so that it will help in building big future projects. Now, this is the time to learn some new projects and a better future.

All you need is your username and password and other parameters - no API signup is needed.

### Like posts of users you want to reach
* Comment on these posts
* Follow users you want to reach
* Unfollow users who don't follow you back within x hours
* Like posts in your news feed - only those you want to
* Build a profile object with all your followers and users you follow

### sample code
```python
from instabot import Bot
import os
import shutil
import time
import pandas as pd
class my_insta_login():
    def __init__(self,my_username,my_password):
        ''''''
        try:      
            self.my_username=my_username
            self.my_password=my_password
            cwd=os.getcwd()  ## Get the current working
            if 'config' in os.listdir():
                shutil.rmtree('config') #deletes a directory and all its contents
                time.sleep(1) 
            self.bot = Bot()
            self.bot.login(username=self.my_username,password=self.my_password)
        except:
             print(". Something went to wrong\n. Restart kernal\n. Please logout your previous login")
        
    def get_all_followers_info(self,userid):
        ''''''
        username=[]
        media_count=[]
        follower_count=[]
        following_count=[]
        following_count=[]
        mutual_followers_count=[]
        followers_pk=[]
        self.userid=userid
        my_followers_pk=self.bot.get_user_followers(self.userid) 
        for pk in my_followers_pk:
            followers_pk.append(pk)
        for pk in followers_pk:
            info=self.bot.get_user_info(pk)
            username.append(info['username'])
            media_count.append(info['media_count'])
            follower_count.append(info['follower_count'])
            following_count.append(info['following_count'])
            mutual_followers_count.append(info['mutual_followers_count'])
            #followers_id.append(info)
        df=pd.DataFrame({'username':username,'media_count':media_count,'follower_count':follower_count,
                         'following_count':following_count,'mutual_followers_count':mutual_followers_count})
        return df
    
    def get_user_info(self,userid):
        ''''''
        user_info=self.bot.get_user_info(user_id=userid)
        return user_info
    
    def logout(self):
        self.bot.logout()
    def post_image(self,img_path,photo_caption=""):
        self.bot.upload_photo(img_path,caption=photo_caption)
    def send_msg_to_id(self,msg,username_list):
        self.bot.send_message(msg,username_list)
    def unfollow_everyone(self):
        print()
        self.bot.unfollow_everyone()
    def follow_user(self,username):
        self.bot.follow(username)
        
```

```
my_insta=my_insta_login(my_username='xxxxx-xxxxx-xxxxx',my_password='xxxx-xxxx-xxx')
followers_info_df=my_insta.get_followers_info('username')
```
followers info data frame
![img1](https://github.com/vishalbpatil1/Instagram-automatuion/blob/main/insta_followers_df.png)

Thanks!
