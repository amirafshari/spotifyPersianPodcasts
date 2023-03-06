

# Libs


```python
# Recieving Data from Spotify
import spotipy
from spotipy.oauth2 import SpotifyClientCredentials
import pandas as pd
import matplotlib.pyplot as plt
```

# API


```python
sp = spotipy.Spotify(auth_manager=SpotifyClientCredentials(client_id="",
                                                           client_secret=""))
```

# Explore


```python
show = sp.search(q='پادکست', type='show', market='US', offset=0, limit=50)
#show['shows']['items'][0]
```

# Prepare


```python
names = []
description = []
publisher = []
total_episodes = []
external_urls = []
for i in range(20):
    show = sp.search(q='پادکست', type='show', market='US', offset=i*50, limit=50)
    show = show['shows']['items']
    for e in show:
        names.append(e['name'])
        description.append(e['description'])
        publisher.append(e['publisher'])
        total_episodes.append(e['total_episodes'])
        external_urls.append(e['external_urls']['spotify'])
```


```python
names = pd.Series(names)
description = pd.Series(description)
publisher = pd.Series(publisher)
total_episodes = pd.Series(total_episodes)
external_urls = pd.Series(external_urls)
```


```python
df = pd.DataFrame(
{
    'Name': names,
    'Publisher': publisher,
    'Description': description,
    'Total Episodes': total_episodes,
    'URL': external_urls,
    
})

df.index += 1
```

# Finally!


```python
df
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Publisher</th>
      <th>Description</th>
      <th>Total Episodes</th>
      <th>URL</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>ChannelB پادکست فارسی</td>
      <td>Ali Bandari</td>
      <td>در هر اپیزود پادکست فارسی چنل‌بی گزارش یک ماجر...</td>
      <td>83</td>
      <td>https://open.spotify.com/show/2PmMxFZ4OIW5DoUY...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Masty o Rasty | پادکست فارسی مستی و راستی</td>
      <td>King Raam</td>
      <td>Welcome to Masty o Rasty "The Drunken Truth" p...</td>
      <td>142</td>
      <td>https://open.spotify.com/show/35RtCrgybsUG3dos...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>پادکست رخ</td>
      <td>Rokh Podcast</td>
      <td>داستان زندگی کسانی که قسمتی از تاریخ را رقم زدند</td>
      <td>22</td>
      <td>https://open.spotify.com/show/0hDXe6EN56UZsPBr...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Radio Deev / پادکست رادیو دیو</td>
      <td>RadioDeev</td>
      <td>پادکست فارسی رادیو دیو مجله ی شنیداری فرهنگی ه...</td>
      <td>32</td>
      <td>https://open.spotify.com/show/1KZXcjPkHVeaziGY...</td>
    </tr>
    <tr>
      <th>5</th>
      <td>پادکست کتاب کست - KetabCast</td>
      <td>کتاب کست - KetabCast</td>
      <td>📚کتاب کست - Ketab Cast ، پادکست کتاب های صوتی ...</td>
      <td>534</td>
      <td>https://open.spotify.com/show/1eoeo5t8CfjoucLo...</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>996</th>
      <td>سگ مست | Sagmast</td>
      <td>matinus</td>
      <td>sagmast by Matinus alkohol lovers سگ مست پادکس...</td>
      <td>11</td>
      <td>https://open.spotify.com/show/3nEp3Tpo8QLnhVZs...</td>
    </tr>
    <tr>
      <th>997</th>
      <td>داستان های کوتاه</td>
      <td>Farzad Bayan</td>
      <td>توی این پادکست</td>
      <td>1</td>
      <td>https://open.spotify.com/show/5WRbEroh1Wzb5bvW...</td>
    </tr>
    <tr>
      <th>998</th>
      <td>NightPods - نایت پادز</td>
      <td>NoN Residential</td>
      <td>نایت‌پادز یک پادکست سرگرمی است که در آن دور هم...</td>
      <td>5</td>
      <td>https://open.spotify.com/show/1o2Kvl0Q0rrOCVEZ...</td>
    </tr>
    <tr>
      <th>999</th>
      <td>🔺ایلومیناتی: فرقه‌ای که زمین را بلعید</td>
      <td>1343</td>
      <td>در این پادکست درباره‌ی فرقه‌ای خواهید شنید که ...</td>
      <td>2</td>
      <td>https://open.spotify.com/show/5ZAb7t3FF1A7eKrD...</td>
    </tr>
    <tr>
      <th>1000</th>
      <td>سولاریس 💫</td>
      <td>Hesam Bokazadeh</td>
      <td>اگه شما هم با شنیدن اسم آسیموف نیشتون باز میشه...</td>
      <td>9</td>
      <td>https://open.spotify.com/show/0IOjqr6qtaaFw9B4...</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 5 columns</p>
</div>



## Top 20


```python
df[:20]
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Publisher</th>
      <th>Description</th>
      <th>Total Episodes</th>
      <th>URL</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>ChannelB پادکست فارسی</td>
      <td>Ali Bandari</td>
      <td>در هر اپیزود پادکست فارسی چنل‌بی گزارش یک ماجر...</td>
      <td>83</td>
      <td>https://open.spotify.com/show/2PmMxFZ4OIW5DoUY...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Masty o Rasty | پادکست فارسی مستی و راستی</td>
      <td>King Raam</td>
      <td>Welcome to Masty o Rasty "The Drunken Truth" p...</td>
      <td>142</td>
      <td>https://open.spotify.com/show/35RtCrgybsUG3dos...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>پادکست رخ</td>
      <td>Rokh Podcast</td>
      <td>داستان زندگی کسانی که قسمتی از تاریخ را رقم زدند</td>
      <td>22</td>
      <td>https://open.spotify.com/show/0hDXe6EN56UZsPBr...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Radio Deev / پادکست رادیو دیو</td>
      <td>RadioDeev</td>
      <td>پادکست فارسی رادیو دیو مجله ی شنیداری فرهنگی ه...</td>
      <td>32</td>
      <td>https://open.spotify.com/show/1KZXcjPkHVeaziGY...</td>
    </tr>
    <tr>
      <th>5</th>
      <td>پادکست کتاب کست - KetabCast</td>
      <td>کتاب کست - KetabCast</td>
      <td>📚کتاب کست - Ketab Cast ، پادکست کتاب های صوتی ...</td>
      <td>534</td>
      <td>https://open.spotify.com/show/1eoeo5t8CfjoucLo...</td>
    </tr>
    <tr>
      <th>6</th>
      <td>پادکست آرامش</td>
      <td>arameshpodcast.com</td>
      <td>هدف پادکست آرامش، هدیه کردن دقایقی آرامش و احس...</td>
      <td>29</td>
      <td>https://open.spotify.com/show/7cr35mqkp0UbVPCn...</td>
    </tr>
    <tr>
      <th>7</th>
      <td>‌BPLUS بی‌پلاس پادکست فارسی خلاصه کتاب</td>
      <td>Ali Bandari</td>
      <td>خلاصه‌ی فارسی کتابهای غیرداستانی</td>
      <td>63</td>
      <td>https://open.spotify.com/show/5HqY5kOdUaGvmQsW...</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Digesttt/ پادکست دایجست</td>
      <td>فرشاد محمودی</td>
      <td>پادکست دایجست مسائل نسبتاً پیچیده دنیای اطراف ...</td>
      <td>41</td>
      <td>https://open.spotify.com/show/0APHFnyp6hB6de0s...</td>
    </tr>
    <tr>
      <th>9</th>
      <td>پادکست جنایی آخرین شاهد</td>
      <td>Mahdi Pourbaqi</td>
      <td>این یک پادکست قصه گو نیست پرونده های جنایی واق...</td>
      <td>79</td>
      <td>https://open.spotify.com/show/5oJxOMLttosMDiPu...</td>
    </tr>
    <tr>
      <th>10</th>
      <td>پادکست مختصر و مفید</td>
      <td>Ardeshir Tayebi</td>
      <td>کنج‌کاوی در تاریخ، سیاست و علم با اردشیر طیبی</td>
      <td>50</td>
      <td>https://open.spotify.com/show/7bCiopnv1MlEl2UE...</td>
    </tr>
    <tr>
      <th>11</th>
      <td>meditation podcast | مدیتیشن پادکست</td>
      <td>meditation podcast</td>
      <td>در هر اپیزود مدیتیشن پادکست، مدیتیشنی برای کمک...</td>
      <td>58</td>
      <td>https://open.spotify.com/show/2KqzlJNguHFSjx73...</td>
    </tr>
    <tr>
      <th>12</th>
      <td>On podcast پادکست آن</td>
      <td>mersen</td>
      <td>در هر اپیزود پادکست آن، داستان واقعی آدمها رو ...</td>
      <td>20</td>
      <td>https://open.spotify.com/show/18dEbxRMhmCOSBLB...</td>
    </tr>
    <tr>
      <th>13</th>
      <td>owrsi | پادکست اورسی</td>
      <td>Saman Karampour</td>
      <td>غیر سطحی ببینیم و بشنویم</td>
      <td>11</td>
      <td>https://open.spotify.com/show/5G5S9nV9WaMVbsJh...</td>
    </tr>
    <tr>
      <th>14</th>
      <td>پادکست فارسی ناوکست / Navcast/ترجمهٔ مستقل کتا...</td>
      <td>Roshan Abady</td>
      <td>قسمتهای این فصل از ناوکست به صورت پیوسته به تر...</td>
      <td>74</td>
      <td>https://open.spotify.com/show/2r3S4hgcs0ksj5V9...</td>
    </tr>
    <tr>
      <th>15</th>
      <td>پادکست بوم</td>
      <td>Mehdi Abbasi</td>
      <td>پادکست فارسی تاریخ فلسفه</td>
      <td>34</td>
      <td>https://open.spotify.com/show/3a6TjdLquDQvSXtV...</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Moniaz Podcast | پادکست فارسی منیاز</td>
      <td>moniaz</td>
      <td>پادکست منیاز با هدف آگاهی بخشی در جهت ایجاد زن...</td>
      <td>47</td>
      <td>https://open.spotify.com/show/2pCF0JIZOagq3OJS...</td>
    </tr>
    <tr>
      <th>17</th>
      <td>R.O.Tik | پادکست اروتیک</td>
      <td>R.O.✔</td>
      <td>🔞تنها پادکست اروتیک ایرونی!🍑🍆نود یا صداس سکستو...</td>
      <td>7</td>
      <td>https://open.spotify.com/show/7gFfKTEEE0ILmTLP...</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Saate Sefr | پادکست فارسی ساعت صفر</td>
      <td>Amin Matin | امین متین</td>
      <td>ساعت صفر روایتی است از معمای زمان | *توجه : شا...</td>
      <td>39</td>
      <td>https://open.spotify.com/show/6ZbOqYS6h8Q4e2h2...</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Ravi | پادکست فارسی راوی</td>
      <td>arash kaviani</td>
      <td>ما روایت گر قصه زندگی افرادی هستیم که یک چالشی...</td>
      <td>23</td>
      <td>https://open.spotify.com/show/6YpWbAA0PL9A3jEF...</td>
    </tr>
    <tr>
      <th>20</th>
      <td>پادکست – جادی دات نت | کیبرد آزاد</td>
      <td>Jadi</td>
      <td>در دفاع از آزادی کیبرد</td>
      <td>20</td>
      <td>https://open.spotify.com/show/2la9aW3sYTNjxVaa...</td>
    </tr>
  </tbody>
</table>
</div>



## Shows containing word 'مدیتیشن'


```python
slice = df[df['Description'].str.contains('مدیتیشن')]
slice
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Publisher</th>
      <th>Description</th>
      <th>Total Episodes</th>
      <th>URL</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>6</th>
      <td>پادکست آرامش</td>
      <td>arameshpodcast.com</td>
      <td>هدف پادکست آرامش، هدیه کردن دقایقی آرامش و احس...</td>
      <td>29</td>
      <td>https://open.spotify.com/show/7cr35mqkp0UbVPCn...</td>
    </tr>
    <tr>
      <th>11</th>
      <td>meditation podcast | مدیتیشن پادکست</td>
      <td>meditation podcast</td>
      <td>در هر اپیزود مدیتیشن پادکست، مدیتیشنی برای کمک...</td>
      <td>58</td>
      <td>https://open.spotify.com/show/2KqzlJNguHFSjx73...</td>
    </tr>
    <tr>
      <th>38</th>
      <td>پادکست مدیتیشن فارسی دارما | Dharma Meditation...</td>
      <td>Ali Delshad</td>
      <td>مراقبه یا مدیتیشن از طریق ورود به بخش نیمه خود...</td>
      <td>100</td>
      <td>https://open.spotify.com/show/0VcAShPf0PhYeE1w...</td>
    </tr>
    <tr>
      <th>108</th>
      <td>پادکست مدیتیشن فارسی دارما | Dharma Meditation...</td>
      <td>Ali Delshad</td>
      <td>من علی هستم و پادکست دارما رو با کمک هلیا برات...</td>
      <td>14</td>
      <td>https://open.spotify.com/show/5mLXV3uB5GX6ZHct...</td>
    </tr>
    <tr>
      <th>165</th>
      <td>پادکست انگیزشی و ژرف‌اندیشی دارما موتیویشن | D...</td>
      <td>Ali Delshad</td>
      <td>در پادکست دارما موتیویشن، سعی می کنیم با کارآف...</td>
      <td>6</td>
      <td>https://open.spotify.com/show/0aslEbqmSj69VDRE...</td>
    </tr>
    <tr>
      <th>192</th>
      <td>آرام پادکست</td>
      <td>محمد مقامیان زاده</td>
      <td>آرام پادکست کانالی با محتوای انگیزشی واجتماعی ...</td>
      <td>7</td>
      <td>https://open.spotify.com/show/6ZKqF9FLQyo4ZurD...</td>
    </tr>
    <tr>
      <th>339</th>
      <td>پادکست روانشناسی و پزشکی دارما کلینیک | Dharma...</td>
      <td>Ali Delshad</td>
      <td>دارما‌ کلینیک پادکستیه که در مورد مسائل روانشن...</td>
      <td>19</td>
      <td>https://open.spotify.com/show/2ptVB562q1m0hBo4...</td>
    </tr>
    <tr>
      <th>783</th>
      <td>YogaLifeRomane یوگا و زندگی با رمانه</td>
      <td>Romaneh Khalili Pour</td>
      <td>سلام من رمانه خلیلی پور هستم مربی یوگا  در هر ...</td>
      <td>14</td>
      <td>https://open.spotify.com/show/0fu00jdnh2Cn3pS8...</td>
    </tr>
    <tr>
      <th>870</th>
      <td>Asoothe | آسوده</td>
      <td>Araz Pourvatan</td>
      <td>Life is an experiment. Here the experience is ...</td>
      <td>3</td>
      <td>https://open.spotify.com/show/2HGdWKcdo6Sj32wn...</td>
    </tr>
    <tr>
      <th>947</th>
      <td>RAZPAD</td>
      <td>راضیه رضایی</td>
      <td>سلام. من اینجا هستم با هدف قرار دادن مهربانی و...</td>
      <td>9</td>
      <td>https://open.spotify.com/show/6HiN7mGLCz7D1A8c...</td>
    </tr>
  </tbody>
</table>
</div>



## Statistics


```python
df.describe()
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Episodes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>1000.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>27.484000</td>
    </tr>
    <tr>
      <th>std</th>
      <td>75.644338</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>4.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>10.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>25.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>1283.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['Total Episodes'].value_counts()
```




    1      105
    2       69
    4       57
    3       55
    5       52
          ... 
    114      1
    115      1
    116      1
    136      1
    0        1
    Name: Total Episodes, Length: 126, dtype: int64



## With more than 400 Episodes


```python
df[df['Total Episodes'] > 400]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Publisher</th>
      <th>Description</th>
      <th>Total Episodes</th>
      <th>URL</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>5</th>
      <td>پادکست کتاب کست - KetabCast</td>
      <td>کتاب کست - KetabCast</td>
      <td>📚کتاب کست - Ketab Cast ، پادکست کتاب های صوتی ...</td>
      <td>534</td>
      <td>https://open.spotify.com/show/1eoeo5t8CfjoucLo...</td>
    </tr>
    <tr>
      <th>54</th>
      <td>Radio Padio | پادکست خبری پادیو</td>
      <td>RadioPadio | پادکست خبری پادیو</td>
      <td>نمیذاریم بی‌خبر بمونین! پادکست خبری رادیو پادی...</td>
      <td>529</td>
      <td>https://open.spotify.com/show/47ITpNV6wVBmF0Hw...</td>
    </tr>
    <tr>
      <th>469</th>
      <td>روانشناسی شخصیت</td>
      <td>اساتید روانشناسی دانشگاه‌ها</td>
      <td>دکتر فرهنگ هلاکویی دکتر محمدرضا سرگلزایی دکتر ...</td>
      <td>833</td>
      <td>https://open.spotify.com/show/7FiQjYyDfZtZHFbU...</td>
    </tr>
    <tr>
      <th>493</th>
      <td>روانشناسی شخصیت‌ و خوشبختی</td>
      <td>Plato</td>
      <td>همه مکالمات دکتر هلاکویی در فصل 1 قرار دارند. ...</td>
      <td>1073</td>
      <td>https://open.spotify.com/show/5r5dc2JA7Y56ZYFd...</td>
    </tr>
    <tr>
      <th>550</th>
      <td>تلویزیون میهن | mihantv</td>
      <td>mihantv1</td>
      <td>با ما از پشت پرده ی سیاست با خبر شوید و از بهت...</td>
      <td>1283</td>
      <td>https://open.spotify.com/show/7cPVgVgTb2PAnysU...</td>
    </tr>
    <tr>
      <th>939</th>
      <td>داستانک</td>
      <td>سعید امینیان</td>
      <td>در اپیزودهای جدید، من برداشت خودم را از داستان...</td>
      <td>430</td>
      <td>https://open.spotify.com/show/3BjE3M4G87Yri4Ot...</td>
    </tr>
  </tbody>
</table>
</div>




```python
df[df['Total Episodes'] < 10]
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Publisher</th>
      <th>Description</th>
      <th>Total Episodes</th>
      <th>URL</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>17</th>
      <td>R.O.Tik | پادکست اروتیک</td>
      <td>R.O.✔</td>
      <td>🔞تنها پادکست اروتیک ایرونی!🍑🍆نود یا صداس *س***ک**ستو...</td>
      <td>7</td>
      <td>https://open.spotify.com/show/7gFfKTEEE0ILmTLP...</td>
    </tr>
    <tr>
      <th>42</th>
      <td>وقت خواب | پادکستی برای رفع بی خوابی</td>
      <td>لویی و دوستان</td>
      <td>وقت خواب ، یک پادکست فارسی زبانه که برای مواقع...</td>
      <td>5</td>
      <td>https://open.spotify.com/show/5c27xgMZdXaSzAxb...</td>
    </tr>
    <tr>
      <th>59</th>
      <td>پادکست هُشْتَکْ | Hoshtak</td>
      <td>MohammadSalar</td>
      <td>پادکست هشتک رو می شنوید من، محمد سالار نعمتی ه...</td>
      <td>8</td>
      <td>https://open.spotify.com/show/4Fhy3dfYAlkB5Nth...</td>
    </tr>
    <tr>
      <th>61</th>
      <td>Mind Master پادکست</td>
      <td>Sara</td>
      <td>مایند مستر یه پادکست فارسیه که توش جنبه‌های مخ...</td>
      <td>8</td>
      <td>https://open.spotify.com/show/5G2T1M7mSbcvY3d1...</td>
    </tr>
    <tr>
      <th>68</th>
      <td>salam podcast | پادکست فارسی سلام</td>
      <td>basalam</td>
      <td>قصه‌ی محصولات و دست‌ساخته‌ها از زبان سازندگان</td>
      <td>8</td>
      <td>https://open.spotify.com/show/7c7QY4VEU3MjDT9Q...</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>995</th>
      <td>سبکتو | Sabketo (فارسی)</td>
      <td>Sabketo</td>
      <td>در پادکست‌های سبکتو در کنار شنونده‌ها...</td>
      <td>0</td>
      <td>https://open.spotify.com/show/7wMHG6jwpMg4OWxF...</td>
    </tr>
    <tr>
      <th>997</th>
      <td>داستان های کوتاه</td>
      <td>Farzad Bayan</td>
      <td>توی این پادکست</td>
      <td>1</td>
      <td>https://open.spotify.com/show/5WRbEroh1Wzb5bvW...</td>
    </tr>
    <tr>
      <th>998</th>
      <td>NightPods - نایت پادز</td>
      <td>NoN Residential</td>
      <td>نایت‌پادز یک پادکست سرگرمی است که در آن دور هم...</td>
      <td>5</td>
      <td>https://open.spotify.com/show/1o2Kvl0Q0rrOCVEZ...</td>
    </tr>
    <tr>
      <th>999</th>
      <td>🔺ایلومیناتی: فرقه‌ای که زمین را بلعید</td>
      <td>1343</td>
      <td>در این پادکست درباره‌ی فرقه‌ای خواهید شنید که ...</td>
      <td>2</td>
      <td>https://open.spotify.com/show/5ZAb7t3FF1A7eKrD...</td>
    </tr>
    <tr>
      <th>1000</th>
      <td>سولاریس 💫</td>
      <td>Hesam Bokazadeh</td>
      <td>اگه شما هم با شنیدن اسم آسیموف نیشتون باز میشه...</td>
      <td>9</td>
      <td>https://open.spotify.com/show/0IOjqr6qtaaFw9B4...</td>
    </tr>
  </tbody>
</table>
<p>486 rows × 5 columns</p>
</div>
