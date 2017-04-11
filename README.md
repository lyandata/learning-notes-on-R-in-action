# learning-notes-on-R-in-action  
I learned R by reading and doing the examples on the book R in action ,it helped me a lot.I'd like to share my study notes with all of you,who likes data analysis and R.
#以下为R in Action 学习笔记，特此感谢此书作者及翻译人员。本文内容仅作学习交流之用。
#演示部分part one
library(openxlsx)#加载
setwd("C:")
getwd()
dat=read.xlsx("TEST.xlsx",sheet = 1)
library(openxlsx)#别忘了
dat=read.xlsx("E:/R/TEST.xlsx",sheet = 1)
setwd("E:/R")
dat=read.xlsx("TEST.xlsx",sheet = 1)
da=na.omit(dat)
attach(dat)
summary(ID)#基本的统计量
summary(SCORE)
detach(dat)
attach(da)
summary(ID)
summary(SCORE)
help(plot)
plot(ID,SCORE,type="l",pch=16,col="red",cex=0.5,lwd=2)
cor(ID,SCORE)


#2016年10月R学习笔记
#http://cran.r-project.org   #下载
library(datasets) # R在datasets包中装有多个数据集
data()  #把数据集加载入内存

file.choose()  #手动选择文件

source(file,echo=TRUE)  #执行脚本中的文件
sink()  #结果输出到文件
data("CO2")
sink("co2.txt")

getwd()
demo()
install.packages("stats")
x<-c(1,6,9,12,76,87,43,54,67,40,98,32)
y<-c(4.4,3,45,65,21,80,65,47,87,65,54,32)
demo()
plot(x,y)
help.start()
example("demo")
help.search("demo")
data()
source("filename")
help.start()
install.packages("vcd")
library(vcd)
help(Arthritis)
Arthritis
install.packages("vcd")
library(vcd) #使用包
example("Arthritis")
help("example")

 
#向量c()

x<-c(3,34,56,78)
x
x[c(1:3)]
x[1:3]
#字符charactor   数字numeric    整数 integer 逻辑 logical   复数complex 
pmax()
pmin()   #极值
unique ()    #去掉向量或数据框中相同的行
array(   )    #数列
aperm()     #维度变换

#矩阵matrix()
X<-matrix(rnorm(12),nrow=3,ncol=4)
nrow(X)
ncol(X)
rowSums(X)
colMeans(X)
#行列式 det()
x<-matrix(1:16,4,4)
det(x)

#Apply()对行列进行运算
#apply(X,margin,fun) margin=1/2表示对行或者列进行运算，fun即运算函数
x<-matrix (rnorm(16),nrow=4,ncol=4)
apply(x,1,sum)
apply(x,2,var)#每一列的方差

#计算X'X的逆 包strucchange,solve函数或者solveCrossprod
#solveCrossprod（x,method=c("qr","chol","solve"),qr效率高，chol精度高
install.packages("strucchange")  ????#包没装上
library (strucchange)
A=matrix(rnorm(16),4,4)
solve(A,method="solve")
solve(crossprod(A,A))
上下结果不同，为什么??????

#取矩阵的上下三角部分  lower.tri(),upper.tri()
A=matrix(1:16,4,4)
#A[lower.tri(A)]=0  #=0别忘了
#A
A[upper.tri(A)]=0
A
#或者利用代码
x= matrix(1:16,4,4)
#下三角
x[row(x)<col(x)]=0 #若上三角改为>
x
#row(),col()
x=matrix (1:12,3,4)
row(x) #第i行所有元素均为i
col(x)  #第j列所有元素均为j

#矩阵行列命名    list()
X<-matrix(1:6,nrow=2,ncol=3,byrow=FALSE)
X[2,]
#dimnames(rnames<-c("r1,r2"),cnames<-c("c1,c2"))
rnames<-c("r1","r2")
cnames<-c("c1","c2","C3")
Y<-matrix(1:6,nrow=2,ncol=3,byrow=FALSE,dimnames=list(rnames,cnames))

向量化算子 一列vec(),一行vech()
x=matrix(6,3,2)
vec(x) 


#转置
x<-matrix(rnorm(9),nrow=3,ncol=3)
t(x)
t(t(x))
y<-c(1:6) #默认y为列向量
#t(y)
#x<-class(y)# ????
class((t(y)))#矩阵
#对应元素相加减“+ —”
#数与矩阵相乘“*”
3*x
#矩阵与矩阵AB相乘 “%*%”
A=matrix(1:12,nrow=3,ncol=4)
B=matrix(1:12,nrow=4,ncol = 3)
A%*%B

#A'B  crossprod
A=matrix(1:12,nrow=4,ncol=3)
B=matrix(1:12,nrow=4,ncol = 3)
crossprod(A,B)

#Hadmard积  “*”
A=matrix(1:16,4,4)
B=A
A*B
#diag提取对角元素
x<-matrix(1:6,nrow=3,ncol=2)
diag(x)

#生成对角矩阵
diag(diag(x))
diag(4)

#矩阵求逆 AX=b  b若不指明默认为单位矩阵   “solve"
a=matrix(rnorm(16),4,4)
solve(a)

#A=UBU'特征值，特征向量 eigen
help("args")
A=diag(4)+1
eigen(A)

#矩阵QR分解 x=QR  qr()
x=matrix(1:16,4,4)
x
Q<-qr(x)
qr.Q(qr(x))  #得到Q
qr.R(qr(x))
#正定矩阵分解A=PP'  chol()
x<-c(2,1,1,1,1,2,1,1,1,1,2,1,1,1,1,2)
A=matrix(x,nrow=4,ncol=4)
chol(A)

#矩阵奇异值分解  A=UDV'，其中u'u=I=V'V A为m*n阶，秩为r的矩阵   svd()
x=matrix(1:18,3,6)
svd(x)

#矩阵广义逆(Moore-Penrose) ABA=A,BAB=B,包MASS  ginv()函数
#A%*%ginv(A)%*%a
install.packages("MASS")
library(MASS)
A=matrix(1:16,4,4)
ginv(A)
A%*%ginv(A)%*%A   #验证

#时间序列的滞后值  “fMultivar"包，tslag() 函数
install.packages("fMultivar")
tslag(x,K,trim=F) #k滞后的阶数，trim 为假返回阶数与原阶数相同，但含有NA值.
library(fMultivar)
tslag(1:16,1:4,trim=FALSE)


#数组array()
dim1<-c("r1","r2","r3")
dim2<-c("c1","c2")
x<-pnorm(6)
z<-array(data=x,c(3,2),dimnames=list(dim1,dim2))
help("list")

#数据框data.frame
patientID<-c(1,2,3,4)
age<-c(25,34,28,52)
diabetes<-c("Type1","Type2","Type1","Type1")
status<-c("Poor","Improved","Excellent","Poor")
patientdata<-data.frame(patientID,age,diabetes,status)
patientdata
patientdata[1:2]
patientdata[1,]
sapply(data.frame, is.numeric)   #判断数据框的列是否为数字
merge()    #数据框合并
#列联表table
table(diabetes,status)
attach(mtcars)#添加数据框
plot(mpg,disp)
detach(mtcars)

attach(mtcars)
summary(mpg)
#with
with(mtcars,{x1<<-summary(mpg)})  #<<
x1

#因子factor
diabetes<-factor(diabetes,ordered=TRUE) #ordered
diabetes
status<-factor(status,ordered  =TRUE)
status<-factor(status,ordered=TRUE,levels=c("Poor","Excellent","Improved"))#levels
#数值型levels,labels
sex<-c("1","2")
sex<-factor(sex,levels = c(1:2),labels=c("Male","Female"))
sex

patientID<-c(1,2,3,4)
age<-c(25,34,28,52)
diabetes<-c("Type1","Type2","Type1","Type1")
status<-c("Poor","Improved","Excellent","Poor")
patientdata<-data.frame(patientID,age,diabetes,status)
str(patientdata)#x显示结构

#列表list
#包含多种对象
x<-c(1:4)
y<-c("ab","花")
g<-matrix(rnorm(2))
h<-"my first list"
mylist<-list(h,x,y,g)
mylist

#   数据    的   输入


edit()#弹出界面框

mydata<-data.frame() 
fix(mydata)  #弹出数据编辑框类似excel

#从csv文件中导入数据（可由Excel转换得到）

setwd("E:/R")#别忘了
grades<-read.table("Studentgrades.csv",header = TRUE,sep = ",")
grades
#对每列指定化类，避免都转化为因子 colclasses
grades<-read.table("Studentgrades.csv",header = TRUE,sep = ",",
colclasses=c("character","character","character","numeric","mnueruc","numeric"))
grades
str(grades)
 
#Excel   read.xlsx
#1.转化为csv    2.利用包xlsx
install.packages("xlsx")
library(openxlsx)#改为xlsx为嘛不行？？
A<-c("D:/1.xlsx")
mydataframe<-read.xlsx(A)


#1.XML( )省略   2.网页
install.packages("RCurl")
install.packages("XML")
readLines(con=stdin())???
xtable( )  #用于产生  HTML的原码

#3.导入SPSS  文件后缀为sav
#Hmisc包，函数spss.get(),read.spss()

install.packages("Hmisc")
library("Hmisc")
spss.get("E:/R/2.sav")
#导入SAS,Stata,NetCDF,HDF5,访问数据库系统（未看）P37-40
# 导入数据的软件：Stat/Transfer(www.stattransfer.cm)

#2.4数据集的标注

#变量标签使用names()重命名
names(x[2])<-"Male"
#factor()为类别变量创建值标签 
#如前：
sex<-c("1","2")
s<-factor(sex,levels = c(1:3),labels=c("Male","Female"))
s
#即把"1"指向了“Male"
?factor
#处理数据对象的函数见表2-4（P(41))
#head()列出对象的前一部分，tail()列出对象的后一部分
#数据的导出部分见附录C,F


#     画图

attach(mtcars)
plot(wt,mpg)#散点图
abline(lm(mpg~wt))#最优拟合曲线
title("Regression of MPG on Weight")
detach(mtcars)

# 用代码保存图形？？？
pdf("my-pdf")#还有很多格式，win.metafile()图元文件，png()便携式网络图片，jpeg()压缩位图格式，bmp(),windows下标准图像格式
attach(mtcars)
plot(wt,mpg)
abline(lm(mpg~wt))
title("Regression of MPG on Weight")
detach(mtcars)
dev.off()

#创建多个图形并随时查看每一个
#法1：

dev.new()
 #statements  to   create   graph 1  
x<-c(11,23,43,56,87,65)
y<-c(21 ,22,45,78,90,12)
plot(x,y)#得到图一
dev.new()
 #statements  to   create   graph 2
a<-c(21,21,32,45)
b<-c(11,13,43,23)
plot(a,b) 
#得到图2,但是两个图是分开的
#法2：

#按键式：Export,注意在direction中选择存放位置

#法3：
#使用dev.new(),dev.next(),dev.prev(),dev.set(),dev.off()
dev.new()
x<-c(11,23,43,56,87,65)
y<-c(21 ,22,45,78,90,12)
plot(x,y)#得到图一
dev.next()
a<-c(21,21,32,45)
b<-c(11,13,43,23)
plot(a,b) 

#设置参数等
dose<-c(20,30,40,45,60)
drugA<-c(16,20,27,40,60)
drugB<-c(15,18,25,31,40)
plot(dose,drugA,type = "b")#"b"同时绘制点线
#函数par()改变图形参数
oPar<-par(n.readonly=TRUE) #使默认图形参数可修改
par(lty=2)#改为虚线，取值1~6
par(pch=17)#点为实心三角，取值0~25
plot(dose,drugA,type="b")
par(opar)    #恢复原始参数
#使用一条代码:
plot(dose,drugA,type = "b",lty=2,pch=17)
plot(dose,drugA,type = "b",lty=2,pch=17,lwd=3,cex=2,col="red")
#宽度为默认的3倍，点的大小为默认的2倍,颜色为红色
#col.axis坐标轴刻度文字的颜色，col.lab坐标名称的颜色，col.main标题颜色
#col.sub副标题颜色，fg图形的前景色，bg图形的背景色
plot(dose,drugA,type = "b",lty=2,pch=17,lwd=3,cex=2,col="red",col.lab="green")
#rgb可基于红-绿-蓝三色值生成颜色，hsv基于色相-饱和度-亮度值
#http://research.stowers-institute.org/efg/R/Color/Chart
#创建连续型颜色向量的函数：rainbow(),heat.colors(),terrain.colors(),topo.colors(),cm.colors

rainbow(5)   ???

 # 颜色配对RColorBrewer
install.packages("RColorBrewer")
library('RColorBrewer')
mycolors<-brewer.pal(7,"Set1")
#"从set1中抽取了7种用16进制表示的颜色并返回一个向量"
#调色板brewer.pal(),
library('RColorBrewer')

brewer.pal.info() ???
 #多阶灰色度  grey()
n<-10
mycolors<-rainbow(n)
pie(rep(1,n),labels=mycolors,col=mycolors)
n<-10
mygrays<-gray(0:n/n)   #n/n改成1后结果不一样
pie(rep(1,10),labels=mygrays,col=mygrays)
#     文本属性
#指定字体族，字号，字样的参数
#font 整数，font.axis(坐标轴刻度文字的字体样式)，font.lab(坐标轴名称的样式)
#font.main 标题的~，font.sub（副标题），ps(字体磅值)
#family(绘制文本时使用的字体族)
par(font.lab=3,cex.lab=1.5,font.main=4,cex.main=2)#斜体，1.5倍放大,粗斜体,2倍.
#字体族设置
windowsFonts(A=windowsFont("Arial Black"),B=windowsFont("Bookman Old Style"))
par(family="A")         
#PDF格式 ，PostScript参考PDF
names(pdfFonts())#找出系统的可用字体
pdf(file="myplt.pdf",family="fontname") #生成图形

#图形尺寸与边界大小的参数
#pin()
dose<-c(20,30,40,45,60)
drugA<-c(16,20,27,40,60)
drugB<-c(15,18,25,31,40)
opar<-par(no.readonly = TRUE)
par(pin=c(2,3))
par(lwd=2,cex=1.5)
par(cex.axis=.75,font.axis=3)
plot(dose,drugA,type="b",pch=10,lty=2,col="red")#image1
plot(dose,drugB,type="b",pch=23,lty=6,col="blue",bg="green")


#4.基本的数据管理
#创建新变量
attach(mydata)
mydata$sumx<-x1+x2
detach(mydata)
#法二
mydata<-transform(mydata,sumx=x1+x2)
#变量重编码
#x|y是或，&与，==严格等于，inTRUE(x)测试是否为x
leadership<-within(leadership,{agecat<-NA
agecat[age>75]<-"elder"
agecat[age>=55&age<=75]<-"middle aged"
     gaecat[age<55]<-"young"})
#within与with不同，它允许修改数据框
#car包中有recode()可重编码数值型，字符型向量或因子。doBy包中的recodevar()也可以。R中cut()可将数值型变量按值域切割为多个区间。
#变量重命名
#弹出修改使用 fix()
#编程修改names()
names(leadershi)[2]<-"testDate"
#将若干个重名命名 names(leadership)[6:10]<-c("1","2","3","4","5")
#安装plyr包，使用rename()函数
x<-rename(x,c(manger="mangerID",data="IDdate"))
#缺失值 is.na() 正，负无穷 Inf,-Inf
y<-c(1,2,3,NA)
in.na(y)
x[x==33]<-NA  #重编码为缺失值
#排除部分缺失值
x<-c(1,2,3,NA)
y<-sum(x,na.rm=TRUE)
#删除所有含有缺失值的行 na.omit()

#日期值 常以字符串的形式输入R中，转化为数值形式存储
as.Date(X,"")
# %d数字表示的日期（0-31） %a 缩写的星期名 %A 非缩写的星期名 %m月份（00~12）
#%b 缩写的月份（Jan) %B 非缩写月份（january) %y 两位数的年份 %Y 四位数的年份
#日期值默认输入：yyyy-mm-dd
mydate<-as.Date(C("2007-06-22","2004-02-13"))
#将默认的字符型数据转化为了对应日期。
strDates<-c("01/05/1965","08/16/1975")
dates<-as.Date(strDates,"%m/%d/%Y") #修改为从月开始读起
myformat<-"%m/%d/%y"
x<-as.Date(x,myformat) #用指定格式读取字符型向量，并将其作为一个日期变量替换到数据框中。
Sys.Date() #返回当天的日期
date()  #返回当前的日期和时间
#format（x,format="") #可指定输出格式，并提取日期中的某些值
# Sys.Date()
#[1] "2016-12-22"
today<-Sys.Date()
format(today,format="%B %d %Y")#"十二月 22 2016"
format(today,format="%A") #"星期四"
difftime() #计算时间间隔
today<-Sys.Date()
then<-as.Date("2011-01-22")
difftime(today,then,units="weeks") #Time difference of 308.7143 weeks

strDates<-as.character(dates) #将日期转化为字符型变量

#类型转换，判断使用is.  , 转换用as.
is.numeric()is.character()is.vector()is.matrix() is.data.frame() is.factor() is.logical()
#数据排序 默认是升序，降序用负号
attach(data);newdata<-data[order(gender,-age)]
#数据集的合并
#使用公共因子进行联结 merger()
total<-merge(dataframeA,dataframeB,by="ID")
#或者total<-merge(dataframeA,dataframeB,by=c("ID","country"))
#直接合并，添加行，列 rbind(),cbind()

#数据集取子集
newdata<-leadership[,c(6:10)]
#或者使用变量名充当列的下标
myvars<-c("q1","q2","q3","q4","q5","q6")
newdata<-leadership[myvars]
#或者使用paste()函数
myvars<-paste("q",1:5,sep="")
newdata<-leadership[myvars]
#剔除或丢弃变量 ，先选择，再用非
myvars<-names(leadership)%in%c("q3","q4")
newdata<-leadership[!myvars]
#若已知变量的位置
newdata<-leadership[c(-8,-9)]
#相同变量的删除工作
leadership$q3<-leadership$q4<-NULL
#选入观测
attach(data);newdata<-data[gender=='M'&age>30];detach(data)
#简单方法subset() newdata<-subset(data,age>=35|age<24,select=c(q1,q2,q3,q4)) #其中变量保留了q1到q4
newdata<-subset(data,gender=="M"&age>25,select=gender:q4)

#随机抽样
mysample<-data[sample(1:nrow(data)),3,repalce=FALSE] #个数为3，无放回

#操作sql数据框
library(sqldf)
newdf<-sqldf("select *from mtcars where carb=1 order by mpg",row.names=TRUE)
sqldf("select avg(mpg) as avg-mpg,avg(disp) as avg-disp,gear from mtcars where cy1 in (4,6) group by gear")


#高级数据管理
#数学函数 abs(),sqrt(),ceiling()不小于x 的最小整数，floor()不大于......
#trunc()向0的方向截取的x中的整数部分，round(x,digit=2)将x舍入为指定小数位的数
#signif(x,digits=2)将x舍入为指定的有效位数的数，cos(),sin(),tan()
#反acos(),asin(),atan(),双曲sinh(),cosh(),atanh()
#log(x,base=n)对x取以n为第的对数log(10)=2.3026,log10(10)=1,exp()指数

#统计函数
z<-mean(x,trim=0.05,na.rm=TRUE) #丢弃了最大5%，最小5%和缺失值之后的值。
#mean(),median(),sd(),var(),mad()#绝对中位差
#quantile(x,probs);y<-quantile(x,c(.3,.84)) 分位点
#range(),sum(),diff(x,lag=n) 滞后差分，lag指定滞后的项数，默认为1
#min(),max(),scale(x,center=TRUE,SCALE=TRUE) 按列进行中心化，默认0均值，1方差
newdata<-scale(mydata)*SD+M #任意一列
newdata<-transform(mydata,myvar=scale(myvar)*10+50) #对任意变量进行标准化
#概率函数
#dnorm密度函数（density),pnorm分布函数，qnorm分位数，rnorm生成随机数
#beta,binom,cauchy,chisq(卡方)，exp,f,gamma,geom(几何)，hyper(超几何)，lnorm(对数正态)
#logis,multinom(多项分布)，nbinom(负二项分布)，norm(正态)，pois(泊松)，
#signrank(wilcoxon符号秩和检验)，t,unif(均匀分布)，weibull(weibull分布)，wilcox(wilcox秩和分布)
#在[-3，3]上绘制标准正态曲线
x<-pretty(c(-3,3),30) #pretty(x,n),将x分割为等间距的n个区间
y<-dnorm(x)
plot(x,y,type="l",xlab="Normal Deviate",ylab="Density",yaxs="i")


#设定随机种子 set.seed(1234)
#生成多元数据 MASS包中的mvrnorm(n,mean,sigma)
library(MASS)
options(digits=3)
set.seed(1234)
mean<-c(230.7,146.7,3.6)
sigma<-matrix(c(15360.8,6721.2,-47.1,6721.2,4700.9,-16.5,-47.1,-16.5,0.3),nrow=3,ncol=3)
mydata<-mvrnorm(500,mean,sigma) #sigma为方差-协方差矩阵，相关矩阵
mydata<-as.data.frame(mydata)
names(mydata)<-c("y","x1","x2")
dim(mydata)
head(mydata,n=10) #只显示前面10个

#字符处理函数
nchar() #计算字符数量 
x<-c("ab","cde","fghij");length(x)  #3
nchar(x[3])  #5
substr(x,start,stop) #提取或替换一个字符向量中的子串
x<-"abcdef";substr(x,2,4);  #"bcd"
substr(x,2,4)<-"22222"   ; x  #"a222ef"
grep(pattern,x,ignore.case = FALSE,fixed = FALSE)#在x中搜索某种模式，fixed=FALSE,则pattern为一个正则表达式，否则为文本字符串，返回值为匹配的下标
grep("A",c("b","A","c"),fixed=TRUE)  #2
sub(pattern,replacement,x,ignore.case = FALSE,fixed = FALSE) #在x中搜索pattern,并以文本replacement将其替换
sub("\\s",".","hello there")  #"hello.there"
strsplit(x,split,fixed = TRUE)  #在split 处分割字符向量x中的元素
y<-strsplit("abc","") ;y  #"a" "b" "c"
unlist(y)[2]#或者sapply(y,"[",2) #结果均为“b"

paste(...,sep="") #连接字符串，分割符为sep
paste("x",1:3,sep="") #"x1" "x2" "x3"
paste("x",1:3,sep="m") #"xm1" "xm2" "xm3"
paste("today is",date()) #paste("x",1:3,sep="")
toupper() #大写转换 tolower() #小写转换
toupper("abc") #"ABC"
#正则表达式  ^[hc]?at  #匹配任意以0个或1个h或c开头，后接at的字符串

#其他实用函数
length(x);seq(from,to,by);rep(x,n);
cut(x,n)#将连续型变量x分割为有着n个水平的因子,使用ordered.result=TRUE创建有序因子
pretty(x,n) #将连续型变量x分割为n个区间
cat(...,file = "myfile",append=FALSE) #连接....中的对象，并将其输入到屏幕上或文件中
firstname<-c("Jane")
cat("hello",firstname,"\n") #hello Jane \n新行，\t制表，\'单引号，\b退格
name<-"Bob";cat("hello",name,"\b.\n","isn\'t R","GREAT?\n")
#hello Bob.
#  isn't R GREAT?
name<-"Bob";cat("hello",name,".\n","isn\'t R","GREAT?\n") #不使用\b退格，则.距Bob会很远

#将函数应用与矩阵 apply() 求各行，各列
apply(x,MARGIN,FUN,...)# MARGIN=1表示行，2表示列
mydata<-matrix((rnorm(30),nrow=6))
apply(mydata,1,mean);apply(mydata,2,mean,trim=0.2)


#将学生的各科成绩组合为单一的成绩衡量指标，基于名次给出从A到F的评分，根据学生姓氏和名字首字母对花名册进行排序
options(digits = 2)
student<-c("john davis","angela williams","bullwinkle moose","david jones","janice markhammer","cheryl cushing",
           "reuven ytzrhak","greg knox","joel england","mary rayburn")
math<-c(502,600,412,358,495,512,410,625,573,522)
science<-c(95,99,80,82,75,85,80,95,89,86)
english<-c(25,22,18,15,20,28,15,30,27,18)
roster<-data.frame(student,math,science,english,stringsAsFactors = FALSE)#花名册，执勤表
Z<-scale(roster[,2:4])
score<-apply(z,1,mean)
roster<-rbind(roster,score)
y<-quantile(score,c(.8,.6,.4,.2))#综合得分的百分位数
roster$grade[score>=y[1]]<-"A"
roster$grade[score<y[1]&score>y[2]]<-"B"
roster$grade[score<y[2]&score>y[3]]<-"C"
roster$grade[score<y[3]&score>y[4]]<-"D"
roster$grade[score<y[4]]<-"F"
name<=strsplit((roster$student)," ")  #以姓名为界，拆分姓和名
lastname<sapply(name,"[",2)  #姓
firstname<-sapply(name,"[",1) #名
roster<-rbind(firstname,lastname,roster[,-1]) #把姓，名变量合并添加到roster中，并删除student变量
roster<-roster[order(lastname,firstname), ] #按照姓氏和名字排序

#控制流
#语句（statement)是一条单独的语句或一组复合语句（包含在花括号中的一组语句，使用；h号隔开
#条件（cond)是一条最终被解析为真，假的表达式
#表达式（expr)是一条数值或字符串的求值语句
#序列（seq)是一个数值或字符串序列

#for循环
for  (var in seq ) statement
for(i in 1:10) print ("hello")  #单词hello被输出10次
#while 循环
while(cond ) statement
i<-10
while(i>0) {print ("hello");i<-i-1} 
#条件执行
#if-else 结构
if(cond) statement
if(cond) statement1 else statement2
#ifelse结构
ifelse(cond ,statement1,statement2)
#switch结构
switch(expr,...) #根据一个表达式的值选择语句执行

#用户自编函数
myfunction<-function (arg1,arg2,...)
  {statements
  return(object)}

#整合（aggregate)与重构(reshape)
#转置 t() #可作用于矩阵或数据框，后者行名将变为列名
#整合 aggregate(x,by,FUN) #X是待折叠的对象，by 是变量名组成的列表(一个变量也要列表形式），FUN为函数
options(digits=3)
attach(mtcars)
aggdata<-aggregate(mtcars,by=list(cyl,gear),FUN=mean,na.rm=TRUE)
aggdata
Group.1 Group.2  mpg cyl disp  hp drat   wt qsec  vs   am gear carb
1       4       3 21.5   4  120  97 3.70 2.46 20.0 1.0 0.00    3 1.00
2       6       3 19.8   6  242 108 2.92 3.34 19.8 1.0 0.00    3 1.00
3       8       3 15.1   8  358 194 3.12 4.10 17.1 0.0 0.00    3 3.08
4       4       4 26.9   4  103  76 4.11 2.38 19.6 1.0 0.75    4 1.50
5       6       4 19.8   6  164 116 3.91 3.09 17.7 0.5 0.50    4 4.00
6       4       5 28.2   4  108 102 4.10 1.83 16.8 0.5 1.00    5 2.00
7       6       5 19.7   6  145 175 3.62 2.77 15.5 0.0 1.00    5 6.00
8       8       5 15.4   8  326 300 3.88 3.37 14.6 0.0 1.00    5 6.00
#前3列是新生成的，比如4个汽缸，3个档位行驶英里数均值为21.5

#reshape2包 #先让数据融合melt(),s使每一行都是唯一的标识符-变量组合，再重铸(dcast())为你想要的形状
install.packages("reshape2")
library(reshape2)
md<-melt(mydata,id=c("ID,"Time" ))
#必须唯一确定每个测量所需的变量，而表示测量变量名的变量由程序自动创建
#重铸 dcast()
newdata<-dcast(md,formula,fun.aggregate)
#md为已融合的数据，formula为最终想要的结果，fun.aggregate为数据整合函数










#论文中用到的
gc(rm(list=ls())) #清除之前的变量空间
library(openxlsx)
 X=read.xlsx("C:/Users/123/Desktop/1.xlsx",sheet=1)
plot(t,y)
attach(X)
fit<-lm(log(Y)~t,data=X) #对数线性
summary(fit)
#fit<-lm(Y~X1+X2+X3,data=X)
summary(fit)
plot(t,y)
#y<-c(4,1,0,0,0,7,4.571)
#z<-c(18,1,0,0,0,60,1.727)


require(stats)
x <- matrix(1:10,ncol=2)
x

centered.x <- scale(x, scale = FALSE)
centered.x
install.packages("car")  #对应分析的包

llibrary(openxlsx)
X=read.xlsx("E:/R/mydata.xlsx",sheet = 1)

fit<-lm(mysample$P2~mysample$EL+I(mysample$EL^2),data=mysample) #多项式回归
#summary(fit)
plot(X$EL,X$P2,xlab="EL",ylab = "P2")
abline(fit)

library(openxlsx)
X=read.xlsx("C:/Users/123/Desktop/1.xlsx",sheet=1)
summary(X$x1)
t.test(X$x1,mu=4) #t检验
summary(X$x2)
t.test(X$x2,mu=50)
summary(X$x3)
t.test(X$x3,mu=10)



library(openxlsx)
X=read.xlsx("C:/Users/123/Desktop/1.xlsx",sheet=1)
lm.lg<-lm(Y~log(t))
summary(lm.lg)

#options(digits=3)
Z<-log(Y)
#Z
fit<-lm(Z~t)
#plot(fit)
summary(fit)
#cor(X)
#install.packages("car" )
#library(car)
#scatter.smooth(X,spread=FALSE,smoother.args=list(lty=2),main="Scatter Plot  Matrix")
#fit<-lm(Y~X1+X2+X3,data=X)
#summary(fit)
#par(mfrow=c(2,2))
#plot(fit)
#attach(X)
#points(X$year==2012)
newdata<-X(year==2012)
predict(lm(Y~X1+X2+X3),point,interval="prediction", level=0.95)  #预测
#predict(fit)

library(openxlsx)
X=read.xlsx("C:/Users/123/Desktop/2.xlsx", sheet=1)
library(MASS)
digit(options=3)
ld<-lda(Type~x1+x2+x3+x4+x5+x6+x7,X) #判别
ld
attach(X)
table(Type,predict(ld)$class)
X=read.xlsx("C:/Users/123/Desktop/2.xlsx", sheet=1)
Y=read.xlsx("C:/Users/123/Desktop/4.xlsx", sheet=2)
library(MASS)
ldax<-lda(Type~x1+x2+x3+x4+x5+x6+x7,X)
predict(ldax,Y)


gc(rm(list=ls()))

library(openxlsx)
X=read.xlsx("E:/R/mydata.xlsx", sheet = 1)
plot(X$EL,X$P2)
#set.seed(1234)
mysample<-X[sample(1:nrow(X),10,replace=FALSE),]
p<-scale(X$P2)
p
plot(X$EL,p)
fit<-lm(scale(X$P2)~X$EL) #标准化，线性回归
summary(fit)
plot(X$EL,P,xlab="EL", ylab = "P")
abline(fit)
fit<-lm(scale(X$P2)~X$EL+I(X$EL^2),data=X)
summary(fit)
set.seed(1234)
mysample<-X[sample(1:nrow(X),10,replace=FALSE),]
plot(mysample$EL,scale(mysample$P2),xlab="EL", ylab = "P2")
abline(fit)

fit<-lm(X$P2~X$EL+I(X$EL^2),data=X)
par(mfrow=c(2,2))
plot(fit)

fit<-lm(scale(X$P2)~X$EL+I(X$EL^2),data=X)
par(mfrow=c(2,2))
plot(fit)

gc(rm(list=ls()))
ydata<-read.table("E:/R/mydata.csv",header=TRUE)
mydata
#myvars<-c("EL","P2","P1","Time")
attach(mydata)
#X<-data.frame(myvars)
#X<-matrix(mydata,nrow=201,ncol=6)


library(openxlsx)
X=read.xlsx("E:/R/mydata.xlsx", sheet = 1)
fit<-lm(scale(X$P2)~X$EL+I(X$EL^2),data=X)
par(mfrow=c(2,2))
plot(fit)
install.packages("Hmisc")
library(Hmisc)
spss.get("E:/R/mydata.sav", use.value.labels = TRUE)

聚类

gc(rm(list=ls()))
library(openxlsx)   
X=read.xlsx("C:/Users/123/Desktop/ju1.xlsx",sheet=1)
hc<-hclust(dist(X),"complete")
cbind(hc$merge,hc$height)
plot(hc)
Y<-X[-1]
library(NbClust)
devAskNewPage(ask=TRUE)
nc<-NbClust(Y,min.nc=2,max.nc=15,method="kmeans")
table(nc$Best.n[1,])
barplot(table(nc$Best.n[1,]),xlab="Number of Clusters", ylab="Number of Clusters chosen by 26 criteria")
fit.km<-kmeans(Y,5)
fit.km$size
fit.km$centers

#第二部分：基本方法
     #基本图形
barplot(height) #条形图，height为矩阵或向量，加参数horiz=TRUE可绘制水平条形图
install.packages("vcd")
library(vcd)
x<-Arthritis$Improved #此处x为因子（None,Some,Marked),可以直接用，否则可用table()列表化。
#若height为矩阵，beside的默认值为FALSE,则矩阵中的每一列都将生成图形中的一个条形，将生成堆砌条形图。
#若beside=TRUE,则矩阵的每一列都表示一个分组，生成分组条形图。
#若height为矩阵，可用参数legend.text为图例提供各条形的标签，一般legend=rownames(height)
   #均值，中位数，标准差等的条形图
states<data.frame(state.region,state.x77)
means<-aggregate(states$Illiteracy,by=list(state.region),FUN=mean)
means<-means[order(means$x),] #将均值排序，注意此处的均值为矩阵形式，有两列，Group.1和x
barplot(means$x,names.arg=means$Group.1,main="Mean Illiteracy Rate")#means$x是包含各条形高度的向量，第二处是添加标签。
   #条形图的微调
#使用参数cex.name来减小字号，names.arg允许指定一个字符向量作为条形的标签名。
library(vcd)
par(mar=c(5,8,4,2))#表示绘图区与整个图表区之间的“下，左，上，右”的距离
par(las=2)#las=2即标签垂直于坐标轴
counts<-table(Arthritis$Improved)
barplot(counts,main="Treatment Outcome",horiz=TRUE,cex.name=0.8,names.arg=c("No Improved","Some Improved","Marked Improved"))
    #棘状图（对堆砌条形图进行缩放，每个条形总高度为1，每一段即比例）
library(vcd)
attach(Arthritis)
counts<-table(Treatment,Improved)
spine(counts,main="Spinogram Example  ")
detach(Arthritis)
    #饼图
pie(x, labels = names(x), edges = 200, radius = 0.8, 
clockwise = FALSE, init.angle = if(clockwise) 90 
else 0,    density = NULL, angle = 45, col = NULL, border = NULL, 
lty = NULL, main = NULL)
                     1、x为一个数组，是必输项；
                     
                     2、labels表示为数组添加标签；
                     
                     3、edges为边线数，如果取值太小就是绘制出的图形为多边形，默认值为200，此时较为平滑；
                     
                     4、 radius表示半径大小，默认值为0.8.一般取0.5-1.5之间，太小可能变成一个点，太大则画布显示不完；
                     
                     5、clockwise表示数组数据绘图是是否按照顺时针方向排列；clockwise=TRUE为顺时针，否则逆时针，默认=FALSE；
                     
                     6、 init.angle 表示初始角度大小，顺时针是为90度，否则为0；
                     
                     7、density表示阴影线密度，默认值为NULL，表示没有阴影线；
                     
                     8、angle表示阴影线的倾斜角度，默认值45。
                     
                     9、col表示填充颜色，一般以rainbow(n)来设置不同颜色，n表示颜色数量。
                     
                     10、border表示划分饼的切割线的颜色。
                     
                     11、lty表示划分饼的切割线的线形，lty=0无线条，lty=1为实线，lty取2及以上的值则为虚线。
                     
                     12、main为整个图的标题。
pie(x,labels) #x为非负数值向量，表示每个扇形的面积，而labels表示各扇形标签的字符型向量

par(mfrow=c(2,2))
slices<-c(10,12,4,16,8)
lbls<-c("US","UK","Australia","Germany","France")
pie(slices,labels=lbls,main="Simple Pie Chart")

pct<-round(slices/sum(slices)*100) #添加比例数值
lbls2<-paste(lbls,"",pct,"%",sep="") #百分之的形式，paste用于连接字符
pie(slices,labels=lbls2,col=rainbow(length(lbls2)),main="Pie Chart with Percentages")
#rainbow为各个图形都添加了颜色。

#install.packages("plotrix")  #安装包
library(plotrix)
pie3D(slices,labels=lbls,explode=0.1,radius=2) #直接使用labels=lbls,标签字体太大，radius是半径
text(slices,labels=lbls,pos=1,cex=0.6) ？？？
title(" 3D pie Chart")

mytable<-table(state.region)  #从表格中创建饼图
lbls3<-paste(names(mytable)"\n",mytable,sep=" ”)
pie(mytable,labels=lbls3,main="Pie Chart from a Table\n (with sample sizes)")

 #扇形图  fan.plot()
library(plotrix)
slices<-c(10,12,4,16,8)
lbls<-c("US","UK","Australia","Germany","France")
fan.plot(slices,labels=lbls,main="Fan Plot")  #各个扇形相互叠加，并对半径做了修改，默认的区域颜色就不同。

  #直方图  （连续型变量的分布）
par(mfrow=c(2,2) )
hist(mtcars$mpg)  #简单直方图,有默认的标题

hist(mtcars$mpg,breaks=12,col="red",xlab="Miles Per Gallon",main="Colored histogram with 12 bins") #breaks控制组的数量

hist(mtcars$mpg,freq=FALSE,breaks=12,col="red",xlab="Miles Per Gallon",main="Histogram,rug plot ,density curve") 
#freq=FALSE表示纵轴为概率密度
rug(jitter(mtcars$mpg))  #添加轴须图，若出现结，可以使用参数amount=+-0.01,为每个点添加一个小的随机值
lines(density(mtcars$mpg),col="blue",lwd=2)  #添加了核密度估计曲线

h<-hist(x,breaks=12,col = "red",xlab="Miles Per Gallon",main="Histogram with normal curve and box")
xfit<-seq(min(x),max(x),length=40) #产生了介于最值之间的40个随机数
yfit<-dnorm(xfit,mean = mean(x),sd=sd(x))  #将这40个数进行正态化,dnorm()正态密度函数，此处yfit值较小，绘图不成线
yfit<-yfit*diff(h$mids[1:2])*length(x)  #diff为差分函数.对之前的yfit进行了放大，方法来自于R-help.
lines(xfit,yfit,col="blue",lwd=2)  #叠加正态密度曲线
box()  #利用盒子将整个图形包 起来

#核密度图(估计随机变量概率密度函数的非参数方法)
plot(density(x))   #x为数值型向量

par(mfrow=c(2,1))
d<-density(mtcars$mpg)
plot(d)   #默认设置下的简单图形

d<-density(mtcars$mpg)
plot(d,main="Kernel Density of Miles Per Gallon")
polygon(d,col="red",border="blue")  #polygon根据顶点的x,y坐标绘制多边形
rug(mtcars$mpg,col="brown") #棕色轴须图

#可比较的核密度图 sm.density.compare(x,factor),x为数值型向量，factor为分组向量 ,在sm包中。

install.packages("sm")
library(sm)
attach(mtcars)
cyl.f<-factor(cyl,levels=c(4,6,8),labels=c("4 cylinder","6 cylinder","8 cylinder")) 
#cy1即以4，6，8编码的数值型向量
#为了向图形提供值的标签，所以转换为因子
sm.density.compare(mpg,cy1,xlab="Miles Per Gallon")
title(main="MPG Distribution by Car Cylinders")
colfill<-c(2:(1+length(levels(cyl.f))))
legend(loocator(1),levels(cyl.f),fill=colfill)
detach(mtcars)

 #箱线图 boxplot()
boxplot(formula,data=dataframe) #formula为公式，y~A,将为类别型变量A的每个值并列地生成数值型变量y的箱线图。
#y~A*B,将为类别型变量A，B所有水平的两两组合生成数值型向量y的箱线图
#参数varwidth=TRUE将箱线图的宽度与其样本大小的平方根成正比，参数horizontal=TRUE可以反转坐标轴的方向

attach(mtcars)
boxplot(mpg~cyl,main="Car Mileage Data",xlab="Number of Cylinders",ylab="Miles per Gallon")
#添加参数notch=TRUE,可以得到含凹槽的箱线图
boxplot(mpg~cyl,data=mtcars,notch=TRUE,varwidth=TRUE,col="red",main="Car Mileage Data",xlab="Number of Cylinders",ylab="Miles per Gallon")
#为多个分组因子绘制箱线图
mtcars$cyl.f<-factor(mtcars$cyl,levels=c(4,6,8),labels=c("4","6","8"))
mtcars$am.f<-factor(mtcars$am,levels=c(0,1),labels=c("auto","standard"))
boxplot(mpg~am.f*cyl.f,data=mtcars,varwidth=TRUE,col=c("gold","darkgreen"),main="MPG Distribution by Auto Type",xlab="Auto Type",ylab="Miles Per Gallon")

#小提琴图 为箱线图与核密度图的结合，vioplot包中的vioplot()函数
#图中白点为中位数，黑色盒型的范围是下四分位点到上四分位点，西黑线表示须。
vioplot(x1,x2,...,names=,col=)  #x为数值型向量，names标签的字符向量，
install.packages("vioplot")
library(vioplot)
library(sm)
x1<-mtcars$mpg[mtcars$cyl==4]
x2<-mtcars$mpg[mtcars$cyl==6]
x3<-mtcars$mpg[mtcars$cyl==8]
vioplot(x1,x2,x3,names=c("4 cyl","6 cyl","8 cyl"),col="gold")
title("violin plots of miles per gallon",ylab="miles per gallon",xlab="number of cylinders")

#点图 dotchart(x,labels=),x为数值向量，labels为每个点的标签组成的向量
#可以添加参数 groups来选定因子，用以指定x中元素的分组方式，gcolor控制颜色，cex控制标签大小。

dotchart(mtcars$mpg,labels=row.names(mtcars),cex=.3,main="Gas Mileage for Car Models",xlab="Miles per gallon")

#分组，排序，着色后的点图
x<-mtcars[order(mtcars$mpg),]
x$cyl<-factor(x$cyl)
x$color[x$cyl==4]<-"red"
x$color[x$cyl==6]<-"blue"
x$color[x$cyl==8]<-"darkgreen"
dotchart(x$mpg,labels=row.names(x),cex=.3,groups=x$cyl,gcolor="black",color=x$color,pch=19,main="Gas Mileage",xlab="Miles Per Gallon")


   #第7章 基本统计分析
summary()   #提供极值，四分位数和数值型变量的均值，以及因子向量和逻辑向量的频数统计。
apply() supply() #可指定统计量，supply(x,fun,options),x为数据框或矩阵，若指定了options，它将传递给fun.
#常用的有mean(),sd(),var(),median(),length(),range(),quantitle(),fivenum()可返回图基五数，偏度skew,峰度kurt可自己定义。
#通过sapply()计算描述性统计量
mystats<-function(x,na.omit=FALSE){
         if(na.omit)
         x<-x[!is.na(x)]
         m<-mean(x)
         n<-length(x)
         s<-sd(x)
        skew<-sum((x-m)^3/s^3)/n
        kurt<-sum((x-m)^4/s^4)/n-3
return(c(n=n,mean=m,stdev=s,skew=skew,kurtosis=kurt))
}
myvars<-c("mpg","hp","wt" )
sapply(mtcars[myvars],mystats)

#其他需要安装包的可使用函数
#Hmisc，pastecs,psych.Hmisc包中的describe()函数有之前介绍的函数没有的功能：可返回变量和观测变量的数量、缺失值和唯一值的数目、平均值、分位数以及5个最值。
#pastecs包中的stat.desc()函数，stat.desc(x,basic=TRUE,norm=FALSE,P=0.95)
#其中x为数据框或时间序列。若basic=TRUE为默认情况，若norm=TRUE(非默认)，则返回正态分布统计量，包括峰度，偏度和Shapiro-Wilk正态检验结果。此处使用p值计算均值的置信区间。
#psych包中的describe()函数，可计算非缺失值的数量，平均数，标准差，中位数，截尾平均，绝对中位差，最值，值域，偏度，峰度和均值的标准误。
 install.packages("Hmisc" )
library(Hmisc )
myvars<-c("mpg","hp","wt" )
describe(mtcars[myvars] )  #需要R3.3.2
 install.packages("pastecs" )
library(pastecs )
myvars<-c("mpg","hp","wt" )
stat.desc(mtcars[myvars] ) ##需要R3.3.2
 install.packages("psych" )
library(psych )
myvars<-c("mpg","hp","wt" )
decribe(mtcars[myvars])  #需要R3.3.2

  #分组计算描述性统计量
#1.aggregate(),2.by(),3.doBy包中的summaryBy() 4.psych包中的describeBy()
myvars<-c("mpg","hp","wt" )
aggregate(mtcars[myvars],by=list(am=mtcars$am),mean)
aggregate(mtcars[myvars],by=list(am=mtcars$am),sd)
#aggregate(),是单返回值函数，by可以弥补
#2.by(data,INDICES,FUN) data是数据框或矩阵，INDICES是因子或因子组成的列表，定义了分组，FUN是任意函数。
dstats<-function(x)sapply(x,mystats )
myvars<-c("mpg","hp","wt")
by(mtcars[myvars],mtcars$am,dstats )

#3.分组计算的扩展
summaryBy(formula,data=dataframe,FUN=function )
#formula可接受一下格式：var1+var2+var3+...+varN ~ groupvar1+...+groupvarN,~左侧是数值型变量，右边类别型分组变量。function可为任何内建或自编的R函数。
install.packages("doBy")
library(doBy)
summaryBy(mpg+hp+wt~am,data=mtcars,FUN=mystats)
#3.2 describeBy不允许指定任意函数
library(psych)
myvars<-c("mpg","hp","wt")
describeBy(mtcars[myvars],list(am=mtcars$am))

 #频数表和列联表
library(vcd)
head(Arthritis)
table(var1,var2,..),#使用n个类别型变量（因子）创建n维列联表
xtabs(formula,data),#根据一个公式和一个矩阵或数据框创建一个n维列联表
prop.table(table,margins)#依margins定义的边际表格将表中条目表示为分数形式
margin.table(table,margins)#依margins定义的边际表格计算表中条目的和
addmargins(table,margins)#将概述边（默认求和）放入表中
ftable(table) #创建一个紧凑的“平铺式”列联表
mytable<-with(Arthritis,table(Improved))
prop.table(mytable)  #将频数转化为比例值,有结果，但有警告
prop.table(mytable)*100

 #二维列联表
#1.table(A,B)， 2.xtabs()可使用公式风格的输入创建列联表，mytable<-xtabs(~A+B,data=mydata),~右侧为要进行交叉分类的变量，mydata为矩阵或数据框
#2.使用margin.table()和prop.table()分别生成边际频数和比例
margin.table(mytable,1)
prop.table(mytable,1)   #行，下标1指代table()语句中的第一个变量

margin.table(mytable,2)
prop.table(mytable,2)   #列，下标2指代table()语句中的第二个变量
#各单元格所占比例
prop.table(mytable)
#为表格添加边际和 addmargins(mytable),默认对象是所有变量
addmargins(prop.table(mytable,1),2)  #行和
addmargins(prop.table(mytable,2),1)  #列和
#注意：table()函数默认忽略缺失值，若要将na视为有效类别，需添加参数，useNA="ifany".
#3.使用gmodels包中的CrossTable（）函数
install.packages("gmodels")
library(gmodels)
CrossTable(Arthritis$Treatment,Arthritis$Improved)

#多维列联表
#1.table(),xtabs(),margin.table(),prop.table(),addmargins()都可以推广到高维
#2.ftable()
mytable<-xtabs(~Treament+Sex+Improved,data=Arthritis)
ftable(mytable)
margin.table(mytable,1)
margin.table(mytable,2)
margin.table(mytable,3)
margin.table(mytable,c(1,3))
ftable(prop.table(mytable,c(1,2)))
ftable(addmargins(prop.table(mytable,c(1,2)),3))

#独立性检验 1.卡方独立性检验，2.Fisher精确检验  3.Cochran-Mantel-Haenszel
#1.chisq.test(),对二维表的行，列变量进行卡方独立检验
library(vcd)
mytable<-xtabs(~Treament+Improved,data=Arthritis)
chisq.test(mytable)

mytable<-xtabs(~Improved+Sex,data=Arthritis)
chisq.test(mytable)

#2.Fisher精确检验,fisher.test(),此检验原假设为边界固定的列联表中行，列相互独立
fisher.test(mytable) #注：fisher.test只能用于行，列数大于2的列联表上

3.Cochran-Mantel-Haenszel检验,mantelhaen.test(mytable)

#相关性的度量，vcd包中的assocstats()函数可计算二维列联表的phi系数，列联系数，Cramer's V系数
#vcd包中的kappa()函数，可以计算混淆矩阵的Cohen's kappa值以及加权的kappa值

#结果的可视化，vcd包绘制马赛克图和关联图,ca包中的对应分析函数

 #7.3 多种相关系数和相关性的检验，Pearson,Spearman,Kendall,偏相关系数，多分格相关系数（polychoric),多系列相关系数（polyserial),本节数据集为state.x77
#Pearson定量变量之间,Spearman定序变量之间,Kendall's Tau等级相关系数，cor()可以计算这三种，cov()协方差
#cov(x,use= ,method= ),默认use="everything",method="pearson"
#注：对于cor()函数，可以计算非方形的相关矩阵，cov(x,y)
attach(states.x77) #未找到
#7.3.2偏相关，在控制一个或多个定量变量时，另外两个定量变量之间的相互关系。ggm包中的pcor()函数
#pcor(u,s) u为数值向量，前两个数值表示要计算相关系数的变量下标，其余的数值为条件变量的下标，s为变量的协方差阵
install.packages("ggm")
library(ggm)
colnames(states)
pcor(c(1,5,2,3,6),cov(states))

#7.3.3 其他类型的相关 polycor包中的hetcor()函数可计算一种混合的相关矩阵，
#二、相关性的显著性检验
cor.test(x,y,alternative = ,method= ) #一次只能检验一种相关关系
#psych包中的corr.test()一次可以做更多事情
#在多元正态的假设下，psych包中的pcor.test()可以检验在控制一个或多个额外变量时两个变量之间的条件独立性，pcor.test(r,q,n),r即偏相关系数，q为要控制的变量数
#psych包中的r.test()提供了很多方法：检验某种相关系数的显著性，两个独立相关系数的差异是否显著，两个基于一个共享变量得到的非独立相关系数的差异是否显著，两个基于完全不同的变量得到的非独立相关系数的差异是否显著。

 #相关关系的可视化一般通过散点图和散点图矩阵，还有相关图。

#7.4  t检验
#7.4.1 独立样本的t检验--检验两个总体的均值相等。假设为：两组数据独立，为正态总体。
t.test(y~x,data) #y为数值向量，x是二分变量，调用格式为：t.test(y1,y2),y1,y2为数值向量，data为矩阵或数据框
#注意：此处默认方差不相等，并使用Welsh修正自由度，可以添加参数var.equal=TRUE来假定方差相等，并使用合并方差估计。
library(MASS)
t.test(Prob~So,data=UScrime)#由于结果变量是一个比例值，可以在t检验时对其进行正态化变换，如本例中(Y/1-Y，log(Y/1-Y),arcsin(Y),arcsin(sqrt(Y))

#7.4.2非独立样本的t检验，假定组间的差异呈正态分布，调用格式为：t.test(y1,y2,paired=TRUE),y1,y2为两个非独立的数值向量
library(MASS)
sapply(UScrime[c("U1","U2")],function(x)(c(mean=mean(x),sd=sd(x))))
with(UScrime,t.test(U1,U2,paired=TRUE))

 #7.4.3多于两组的情况
#对于多于两组的之间进行比较，若数据是从正态总体中独立抽样而得，那么可用方差分析。

 #7.5 组间差异的非参数检验，一般是数据无法满足t检验或方差分析的参数假设（变量有可能本质上就严重偏倚或呈现有序关系）
 #7.5.1 两组的比较，Wilcoxon秩和检验（Mann-Whitney U 检验）(两组成对数据，且不满足正态性），调用格式： wilcox.test(y~x,data)，默认双侧，可添加参数exact进行精确检验
with(UScrime,by(Prob,So,median))
wilcox.test(Prob~So,data=UScrime)
#Wilcoxon符号检验是非独立样本t检验的一种非参数替代方法。它适用于两组成对数据和无法保证正态性假设的情况。

 #7.5.2 多于两组的比较
#在不满足方差分析时，若各组独立，用Kruskal-Wallis检验；若各组不独立（如重复测量设计或随机区组设计），Friedman检验。
 # kruskal.test(y~A,data),其中的y为数值型结果变量，A是一个拥有两个或更多水平的分组变量。（若有两个水平，则与Mann-Whitney U检验等价）
 #friedman.test(y~A|B,data),其中的y为数值型结果变量，A是一个分组变量，B是一个用以认定匹配观测的区组变量。
#以上data均为可选参数，它指定了包含这些变量的矩阵或数据框
states<-data.frame(state.region,state.x77)
kruskal.test(Illiteracy~state.region,data=states)

#同步进行多组比较，直接完成所有组之间的成对比较。
 #wmc(y~A,data,method),method指定限制I类误差的方法。
#wmc函数首先会给出样本量，样本中位数，每组的绝对中位差，然后生成各组比较，最后可以观测P值。
source("http://www.statmethods.net/RiA/wmc.txt")  #下载并执行了定义wmc函数的R脚本
states<-data.frame(state.region,state.x77)
wmc(Illiteracy~state.region,data=states,method="holm")


#####
####参考文献：R语言实战（第2版）Robert I.kabacoff著，王小宁 刘撷芯 黄俊文等译   人民邮电出版社 中国工信出版集团





