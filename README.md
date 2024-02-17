# Air-poluution-System


# coding: utf-8

# In[33]:


import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
get_ipython().magic('matplotlib inline')
import seaborn as sns
import datetime 
import matplotlib.dates as md


# In[71]:


df=pd.read_csv('pollution.csv')
df.head()


# In[72]:


df.drop("entry_id",axis=1,inplace=True)
df.head()


# In[73]:


#finding out the time when max. pollution occurs at Chadni Chowk
df[df['Chadni Chowk']==3.0235897439999997].drop(['Gariahat','Dharmatala'],axis=1)


# In[74]:


#finding out the time when max. pollution occurs at Gariahat
df[df['Gariahat']==3.0235897439999997].drop(['Chadni Chowk','Dharmatala'],axis=1)


# In[75]:


#finding out the time when max. pollution occurs at Dharmatala
df[df['Dharmatala']==3.0235897439999997].drop(['Chadni Chowk','Gariahat'],axis=1)


# In[96]:


#finding out pollution level at Chadni Chowk by hourly update
plt.figure(figsize=(12,8))
plt.rcParams.update({'font.size':15})
x =pd.to_datetime(df['created_at'])
y=df['Chadni Chowk']
plt.plot_date(x, y)
plt.xlabel("Data & Hour")
plt.ylabel("Pollution Level")
plt.title("Hourly Pollution Level at Chadni Chowk")


# In[97]:


#finding out pollution level at Gariahat by hourly update
plt.figure(figsize=(12,8))
plt.rcParams.update({'font.size':15})
x =pd.to_datetime(df['created_at'])
y=df['Gariahat']
plt.plot_date(x, y,color='green')
plt.xlabel("Data & Hour")
plt.ylabel("Pollution Level")
plt.title("Hourly Pollution Level at Gariahat")


# In[98]:


#finding out pollution level at Dharmatala by hourly update
plt.figure(figsize=(12,8))
plt.rcParams.update({'font.size':15})
x =pd.to_datetime(df['created_at'])
y=df['Dharmatala']
plt.plot_date(x, y,color='red')
plt.xlabel("Data & Hour")
plt.ylabel("Pollution Level")
plt.title("Hourly Pollution Level at Dharmatala")


# In[95]:


#pairplotting
sns.set(font_scale=1.5)
g=sns.pairplot(df,hue="Chadni Chowk")
g.fig.set_size_inches(15,15)


# In[108]:


sns.jointplot(x="Chadni Chowk",y="Gariahat",data=df,color='green')


# In[109]:


sns.jointplot(x="Chadni Chowk",y="Dharmatala",data=df,color='red')


# In[113]:


sns.jointplot(x="Dharmatala",y="Gariahat",data=df,color='k')
#include <ESP8266WiFi.h>  
 #include <WiFiClient.h>  
 #include <ThingSpeak.h>
 #include<Servo.h>
 Servo servo_test;
 int gas = A0; 
 int angle=0;   
 const char* ssid = "Red Devil";  
 const char* password = "pqrs123456";  
 WiFiClient client;  
 unsigned long myChannelNumber = 318444;  
 const char * myWriteAPIKey = "T4WKJK0X7FLAV3BL";    
 void setup()  
 {
  pinMode(D0,OUTPUT); 
  pinMode(D1,OUTPUT); 
  pinMode(gas,INPUT);  
  servo_test.attach(D2);
  Serial.begin(115200);  
  delay(10);  
  // Connect to WiFi network  
  Serial.println();  
  Serial.println();
  Serial.print("Connecting to ");  
  Serial.println(ssid);  
  WiFi.begin(ssid, password);  
  while (WiFi.status() != WL_CONNECTED)  
  {  
   delay(500);  
   Serial.print(".");  
  }  
  Serial.println("");  
  Serial.println("WiFi connected");  
  // Print the IP address  
  Serial.println(WiFi.localIP());  
  ThingSpeak.begin(client);
 }  
 void loop()   
 {  
  static boolean data_state = true;  
  int sensorValue = analogRead(gas);
 float a = sensorValue*(5.0/1023.0);
  if(a>1)
  {
       ThingSpeak.writeField(myChannelNumber,  2,a , myWriteAPIKey);
      Serial.println("uploaded");
      digitalWrite(D1,LOW);
          digitalWrite(D0,HIGH);
    for(angle = 0; angle < 180; angle += 1)    // command to move from 0 degrees to 180 degrees 
  {                                  
    servo_test.write(angle);                 //command to rotate the servo to the specified angle
    delay(15);                       
  }  
  }
  else
  {
        digitalWrite(D0,LOW);
        digitalWrite(D1,HIGH);
       ThingSpeak.writeField(myChannelNumber,  2,a , myWriteAPIKey);
      Serial.println("uploaded");
  }
  Serial.println(a);
  delay(1000);

  // Write to ThingSpeak. There are up to 8 fields in a channel, allowing you to store up to 8 different  
  // pieces of information in a channel. Here, we write to field 1. 
  delay(1000); // ThingSpeak will only accept updates every 1 second.  
 }
