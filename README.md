# Sentimental-Analysis-for-Mental-Health-Tweets-2017
ibrary(syuzhet)
library(lubridate)
library(scales)
library(reshape2)
library(dplyr)
library(ggplot2)

tweets2<-read.csv(file.choose(),header = T)
tweets2<-iconv(tweets2$tweet,to="utf-8")
d<-get_nrc_sentiment(tweets2)
d
tweets2[9]
get_nrc_sentiment("Awareness")

d %>% mutate(sentiment1=positive-negative,
          sentiment2=(positive-negative)/(positive+negative)) %>% head(10)
head(get_sentiment(tweets2[1],method = "nrc"))
get_sentiment(tweets2[1],method = "syuzhet")
get_sentiment(tweets2[1],method = "bing")

barplot(colSums(d),
        las=2,
        col=rainbow(10),
        ylab ="Count",
        main="Sentiment count for Mental Health Tweets in 2017")

#score
t<-get_sentiment(tweets2,method="syuzhet")
data<-data.frame(Tweet=tweets2,Sentiment_Score=t)
ggplot(data,aes(x=Sentiment_Score))+
  geom_histogram(binwidth = 0.5,fill="skyblue",color="black")+
  labs(title="Distribution of Sentimental Score",x="Sentiment_Score",y="Frequency")


library(sentimentr)
sentimentr::sentiment_by(tweets2[21])

a<-get_sentences(tweets2)
b<-sentimentr::sentiment(a)
c<-sentimentr::sentiment_by(a)
