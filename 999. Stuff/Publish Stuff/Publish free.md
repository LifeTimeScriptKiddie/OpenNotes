---
{"dg-publish":true,"permalink":"/publish-stuff/publish-free/","noteIcon":"","created":"2025-04-15T14:11:19.625-04:00"}
---

















I’ve always thought about developing my own website to record my work and share it with the community. Why not? My requirements were simple: Free and simple.

Like many others, I started with GitHub. But then, guess what? I love GitHub, but I wanted a little more than just the typical GitHub setup. While doing some research, I came across Digital Garden Docs. So, here, I want to cover a bit more about how I did it and how easy it can be.
# 1. Requirements
Sign up, Sign up, and Download. 

1. Github account 
	https://github.com/
2. Vercel account
	 https://vercel.com/
1. Obisidian 
	https://obsidian.md/

# 2. Time to Deploy

https://github.com/oleeskild/digitalgarden
Visit this GitHub repository and click the deploy button. You will need to select your scope and give it a name.




![](https://i.imgur.com/ZWUlUSn.png)


Once that’s done, Vercel will handle the deployment.


![](https://i.imgur.com/XxtsjFJ.png)


Hooray! Once it's complete, you can add a domain and make additional customization.


![](https://i.imgur.com/ELIJ1Qv.png)


Under Project tab, Production Deployment will indicate your page. Obviously there is nothing there yet.
![](https://i.imgur.com/YyNWZiR.png)


# 3. Create a personal access token from github. 

Follow link here : https://github.com/settings/personal-access-tokens/new
Adjust Token Expiration date and fill in the following details. 
==Token Name: YYYY-Digital Garden==
==Description: Publishing content to the digital garden.==
==Resource owner: yourself==

![](https://i.imgur.com/swhuzH6.png)


==Select `Only select repositories`.== 

==Only select repositories: Select your garden repo==
==Permissions:  
Contents: Access: Read and write 
Pull requests: Access: Read and write==

You don't wanna generate a Golden key. (Sorry for AD metaphor)

![](https://i.imgur.com/bvRzxza.png)



# 4. Get your Digital Garden Plugin!!

In Obsidian app, click the gear box on the bottom left corner. Then, click `Community Plugins` and search for Digital Garden. 


![](https://i.imgur.com/ZHKshNF.png)

![](https://i.imgur.com/G01Dz2o.png)

Once Digital Garden Plugin is installed, enter your information under the Digital Garden Tab. 

If you upload images a lot, the imgur plugin is a good option.
![](https://i.imgur.com/LRivWkX.png)


# 5.  Let's publish your first note!

Create a page and add  the following at the top of the note. 
`dg-home` indicates the page is the index page. 
`dg-publish `indicates the page will be published. 

==Homepage==


```
---
dg-home: true
dg-publish: true
---
```
This will look like this
![](https://i.imgur.com/1pfRmGc.png)
==For other pages==

```
---
dg-publish: true
---
```
This will look like this
![](https://i.imgur.com/HHIrbBU.png)


Once you do that, press CTRL+P and select the option you want. 

I am a lazy person, hence I normally go for Publish Multiple Notes.



![](https://i.imgur.com/kQek1iC.png)




# 6. If you want obsidian looking theme...

Copy and paste `*.scss` files under /src/site/styles/user. 
You will need to create the user folder. 

![](https://i.imgur.com/VOBEE9r.png)


# 7. Resources
All resources I used are here. [[Digital Garden Resources\|../Digital Garden Resources]]



Huge thanks to #oleeskild and the community for making this so easy!! 

# 8. Overcoming issues
https://github.com/oleeskild/obsidian-digital-garden/issues/320

#Obsidian #Vercel #github #digitalgarden #makeyourownwebsiteforfree

