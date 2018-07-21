#coding=utf-8
import re
import requests
import MySQLdb

respose=requests.get('https://movie.douban.com/subject/26611804/comments?status=P')
# print(respose.status_code)# 响应的状态码
# print(respose.content)  #返回字节信息
# print(respose.text)  #返回文本内容
duanpin=re.findall(r'class="short">(.*?)</span>',respose.text,re.S)
#初始化一个数据库
cxn = MySQLdb.connect(user='root',passwd='xlndxwh',host='127.0.0.1')
cur = cxn.cursor()
sql="""drop DATABASE if exists burndouban"""
cur.execute(sql)
sql = """CREATE DATABASE burndouban DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci"""
cur.execute(sql)
cxn.commit()
cur.close()
cxn.close()
#连接数据库创建表格导入数据
conn=MySQLdb.connect(host='127.0.0.1',port=3306,user='root',passwd='xlndxwh',db='burndouban',charset='utf8')
cur=conn.cursor()
sql=""" create table if not exists dbcomment(
	num int NOT NULL auto_increment,
	comment varchar(1000) not null,
	primary key (num)
	)"""
cur.execute(sql)
for i in range(len(duanpin)):
	sql=""" insert into dbcomment(comment) values('%s') """ %(duanpin[i])
	cur.execute(sql)
conn.commit()
cur.close()
conn.close()

