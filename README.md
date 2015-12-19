#GameJam Survival Guide

This document describes my thoughts on the game jam I attended (Ludum Dare 34 to be specific). After reading this text you should know:

- what technologies we used, why we used them, their pros and cons
- how to set up the working environment before the jam even starts
- how to cooperate within a small team of developers
- how to cooperate with a graphic designer 
- how to survive in general

Firstly, I'd like to mention that it was my first game jam ever. We formed a team of 3 developers and 1 graphic designer. The size of the team was quite reasonable - I think 2 developers could have made it as well (with much more effort though) and 4 developers would cause more troubles than actual work.

Thanks to the site location in Europe, the topic was announced at 3AM local time. We decided to begin at 8AM in order to sleep a little. Due to school reasons we finished at 8PM the other day which left us with 36 hours in total (including apx. 7 hours of sleep).

##Technologies
Things we actually employed, why we decided so and how we hacked them.

###Unity
For game development we decided to use [Unity framework](https://unity3d.com/) which is free as [Personal Edition](https://unity3d.com/unity/personal-edition). There was no specific reason for choosing this solution except for the fact that [@gyfis](https://github.com/Gyfis) had already worked with it and had known a lot of tricks. The rest of the team had no clue how Unity worked.

###C# #
Unity supports both JavaScript and C# as scripting languages. We decided to use C# since it is a compiled language (believe it or not it's really great to detect errors ASAP). Don't be afraid of C#! I hadn't written much C# until the event itself and there were no problems with C#. Actually it's a really friendly language very similar to Java (but better).

###Operating Systems
This is the part where it gets funny. Of course we intended to stay completely multiplatform i.e. OSX, Ubuntu 14.10 and Windows7. Unfortunately, the installation of Unity on my Ubuntu froze many times so I switched to Windows10 (still three different OSs!). Anyway, if you manage to install Unity on your linux, the rest of the text applies to you as well (Dropbox, Visual Studio Code and all technologies and practices).

I suggest using virtual desktops as much as possible. OSX and Ubuntu have been featuring them for a long time already while Windows haven't. Fortunately, Windows10 brings virtual desktops as well, so try to hack into them! I recommend one desktop for a browser, one for Unity, one for IDE and one for stuff like system monitor and file manages. Of course this is completely up to you.

###Sharing Code
Originally, we wanted to use git or SVN for the version control. I'm really glad we haven't even tried that! Imagine that you are sitting besides two other developers, typing like crazy, and now all of you commit. Who's going to deal with the conflicts? You (almost) need another person to merge branches and manage the repository itself. Moreover, you need the changes to appear immediately - not after some `commit-pull-merge` cycle every 2 minutes.

We used [Dropbox](http://dropbox.com) instead. I think every other cloud-based storage does the trick as well. On the other hand, Dropbox works on all commonly used operating systems and allows you to sync the devices using LAN which is a huge speedup.

So what was the setup? I created an empty folder within my Dropbox folder and by using web interface I shared it with the guys. They accepted and since that time all files were synced among our laptops.

We still had to communicate in order not to modify each other's working file, however, the workflow was much faster.
- Me: "I need this method fixed, pls"
- Tomas: "ook" *typing wildly and saving the file*
- Me: "thx" *after a sec the file is updated on my laptop*

Such situations happen all the time and you don't want to use version control for that, trust me :) If you wonder how we handled the source code conflicts (yes, even though we used Dropbox, there were some conflicts), keep reading.

So what do you really want to sync with others?
- `Assets/`
- `ProjectSettings/`
- `<ProjectName>.sln`
- `<ProjectName>.userprefs`

The remaining folders are generated automatically, so don't bother to share them among the devices - it only slows down the sync process.

*Remark:* Dropbox displays pop-ups every time files are synced. Even though you can turn this feature off, I recommend you not to do so. It's good to know that someone's changes are successfully synced to your device. Especially with Unity.

###IDE
What IDE would you use when writing C#? [Visual Studio](https://www.visualstudio.com/)? Oh, let me laugh a bit. We started with VS on both Windows7 and Windows10. The same version of VS on different systems couldn't handle the Dropbox sync. Seriously Microsoft, what's wrong with you? Your OSs and your IDE don't work together? VS allows you to use some "team" features which is basically git with neat GUI which isn't what we needed for fast co-op.

Since there is no VS port to OSX or linux, we used [Monodevelop](http://www.monodevelop.com/). As you may imagine, the cooperation between Monodevelop and VS was even worse than between VS and VS. In addition, Monodevelop AFAIK doesn't support "load on change" feature. Hence when somebody changes your files via Dropbox, Monodevelop either ignores them or crashes. Not cool.

So what to do? We didn't want to use some basic code editors such as [Sublime Text](http://www.sublimetext.com/) since the lack of C# auto-completion. Let me remind you that the majority of our team have never worked with Unity and its object structure. Fortunately, we found a pretty impressive tool called [Visual Studio Code](https://www.visualstudio.com).
  
VSC is a very lightweight multi-platform IDE very similar to Sublime Text 3. It features *Intellisense*, extensions and many more cool stuff. It auto-loads the changed files (Dropbox integration for free!) and simply works as you expect it to do. Good job, Microsoft, really!

Actually, you must do a simple trick - exclude `Assembly-CSharp.csproj` from Dropbox sync. This file contains some paths to some dynamically linked libraries which are different among the various OSs (yes, even between Windows7 and Windows10 - *meh*). In order not to sync files (really files, not folders) you must do a [folder-trick](http://superuser.com/a/757498/437870) (really Dropbox? Really?).

Everything works somehow well but I'll give you an exact tutorial on opening a file since sometimes VSC doesn't suggest the Unity methods and classes.

1. Set VSC as a default editor in Unity
2. Open a C# script in Unity (this should launch VSC)
3. In VSC, click `open folder` button and select the root of the projects (where `.sln` project is)
4. Test it! Simply type `UnityEngine.<tab>` somewhere in the script and see whether you get a list of classes/functions.

But what if you're working on a script and somebody saves his version of the same file before you do? In normal IDEs your (or his) progress is lost, right? Not in VSC! When you hit `save` it automatically detects a conflict and splits the screen with both versions of the file and lets you merge as you wish. You may say it's very similar to git or SVN, isn't it? It actually isn't. With good communication you'll see this rarely. Moreover, everything is integrated in the IDE so you simply drag useful blocks of code and preserve the colleague's code. This is a killer feature - it really saves time.

###Unity again (sharing code)
One thing I haven't discussed yet is sharing the changes of Unity Editor. In Unity, lots of things may be set by mouse (you basically don't do anything else but clicking stuff). A team should delegate all Unity work to a single developer in order to prevent conflicts. Such developer is the only one who is working in the editor. However, the others have the editor open as well in order to test their scripts. On the other hand, they do not modify anything in the editor.

The "Unity-master" should save the editor changes often. When he does so, the new setting is distributed into the others' computer via Dropbox automatically. According to my experience on Windows10, one must lose and gain again focus on Unity in order to load the new setting. This sucks little bit, but it's still pretty fast.

Of course there are moments when other developers need to change something in Unity. In that case you have to communicate! Seriously, if you overwrite a half-an-hour unsaved work of the "Unity-master", he'll probably kill you.

###Task Management
We decided to use simple [Google Documents](https://www.google.com/docs/about/) as a TODO-list. We wrote the general things to cover, a bug-list and a separate list for the graphical designer. GDocs are great for multi-user editing and it really worked well.

We originally thought about using some kind of issue tracker but apparently it's overkill for such a small project. Don't waste time.

##Graphics
Another directory was created in Dropbox which we shared also with the graphical designer. We didn't use the original project folder in order to prevent worthless sync with another person which could have led into potential troubles and slowdown.

##Tips&Tricks
- Meet your team a day before the topic is announced and set up your environment in advance. Try to develop a blank project in Unity, observe whether Dropbox works as expected, try to handle artificial conflicts. It really pays off, especially if you attend such an event for the first time.
- Buy enough food and beverages beforehand. It's good to have some chocolate for energy boost and some small snacks. Coffee and Coke contain caffeine which wakes you up in the morning and after lunch. I personally discourage you from drinking much of those in the evening as you won't be able to fall asleep.
- Yes, sleep! We worked from 8AM to midnight and I don't think we could come up with something worthy the last half an hour. Having a shower and sleeping for at least few hours pay off.
- Discuss the game BEFORE you start coding. Is it going to be a RPG? Card game? Make sure the whole team knows what you're going to implement. And BTW, don't aim too high - you won't have much time and it's always better to implement fully functional small game than huge unfinished game without sounds and at least some testing.
- Make a TODO list otherwise you'll forget half of the things you wanted to fix.
- Backup! Even though Dropbox features some kind of changes history it's no harm to completely copy the whole project somewhere every 2 hours.
- Talk! If you have the possibility to sit next to each other, communicate a lot. If you work from distinct locations, use at least [Google Hangouts](https://hangouts.google.com/) or something similar.
- Take regular breaks. Order a pizza and eat it together just to get your eyes off the screen (the eyes will thank you!). Go for a 5min walk to buy some soda or another refreshment.
- Change the air in the room regularly, especially if you attend a site with >10 people. No matter what, more oxygen can prevent headaches etc.
- And don't take it too seriously! It's just for fun so be nice to each other!

##Game
Take a look! We've made a game in less than 36 hours.
- [Ludum Dare Post](http://ludumdare.com/compo/ludum-dare-34/?action=preview&uid=63882)
- [Play in Browser](http://randomgamers.github.io/GMOOvergrowth/)
- [GitHub repository](https://github.com/randomgamers/GMOOvergrowth)
