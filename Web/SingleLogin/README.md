![image](https://github.com/petriQore/Capture-The-Love/assets/123587287/a77c7ad2-20dc-4ec7-b60e-4c7e147cf933)

 upon opening the website, we're met with this login page:

![image](https://github.com/petriQore/Capture-The-Love/assets/123587287/1acd22ae-f7f8-4626-b3c8-79ace9d59567)

 let's check the attached file to get an idea

![image](https://github.com/petriQore/Capture-The-Love/assets/123587287/283bb662-b964-41f7-8265-27cd31cf0d3b)

 ok so it seems like we can try an sql injection but let's check the ```/ilookinteresting``` endpoint:


![image](https://github.com/petriQore/Capture-The-Love/assets/123587287/e6ad58ee-cb28-4d25-b9a8-ed2ad712d640)


 so it's telling us to check robots.txt, if you're not familiar with that, it's basically a file that tells web crawlers where they're not allowed to search, here's the definition according to wikipedia

```robots.txt is the filename used for implementing the Robots Exclusion Protocol, a standard used by websites to indicate to visiting web crawlers and other web robots which portions of the website they are allowed to visit. This relies on voluntary compliance.```


![image](https://github.com/petriQore/Capture-The-Love/assets/123587287/e25d08e3-9625-476f-ad3f-6b5059720c7a)


 upon checking the ```/message_for_singles.eml``` endpoint, a file with the same name is downloaded:


![image](https://github.com/petriQore/Capture-The-Love/assets/123587287/eb863333-b06d-47c1-9a4f-c8c83ce5c6cd)


 so this basically confirms that we have to perform an sql injection, it also leaves a clue that sadsingle is the user who can access the website, but we could have found that out from the code directly.<br> in other words, this file is a nice hint for beginners to guide them to the right answer!

finally, we can input:

```username: sadsingle```
```password: ' OR 1=1;--```


![image](https://github.com/petriQore/Capture-The-Love/assets/123587287/46d99981-9edb-4bbf-a7c5-25a367cf262b)

flag: ```SecuriNets{b31ng_51ngl3_15_c00l8bc96fdeedd7d0f536b2a287dce4e4b7}```


