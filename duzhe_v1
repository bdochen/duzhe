import re
import time
from requests_html import HTMLSession
session = HTMLSession()
r = session.get("http://www.52duzhe.com/")
news = r.html.find('tr > td.time > a')
i=0
for new in news:
    qi_list= ((str(new.absolute_links)).replace("{'",'').replace("'}",''))
    qi_list_html = session.get(qi_list)
    qi_list_article_list = qi_list_html.html.find('tr > td.title > a')
    for qi_list_article in qi_list_article_list:
        title=qi_list_article.text
        title=title.replace('/','-')
        title_url= ((str(qi_list_article.absolute_links)).replace("{'",'').replace("'}",''))
        title_html = session.get(title_url)
        article_contents = title_html.html.find('div.blkContainerSblk.collectionContainer > div.blkContainerSblkCon')
        for article_content in article_contents:
            article_temp=article_content.text
            baidu_ad=re.findall('BAIDU(.*?);', article_temp, re.S)
            baidu_wd="BAIDU"+baidu_ad[0]+";"
            article_next=article_temp.replace(baidu_wd,'')
            filename=title + '.txt'
            fileall='读者文摘' + '.txt'
            try:
                with open('./duzhe/'+filename, 'a+', encoding='utf-8') as f:
                    i=i+1
                    print('第',i,'篇')
                    print(title)
                    print(title_url,'\n')
                    f.write(title+'\n'+article_next+'\n')
                with open('./duzhe/'+fileall, 'a+', encoding='utf-8') as f:
                    f.write('第'+str(i)+'篇'+'\n'+title+article_next+'\n'+'\n'+'\n')
            except:
                pass
                
                
                
