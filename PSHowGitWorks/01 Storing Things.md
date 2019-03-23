So we have seen that Git is a map where the keys are SHA1s, and the values are pieces of content, but I also said that Git is not just a 
map, it's a persistent map. Where does persistence come from? Let's go back to the git hash-object command we used a few minutes ago. If I 
want the Apple Pie content to be persistent, I can add a -w argument to this command, -w stands for rights. 


$ echo "Apple Pie" | git hash-object --stdin -w

(make sure this is done in a git initialized proj.. else it will complain)


$ls -a


we can see a new hidden subdirectory called. git. This is where your Git repository goes. So, now Git has a place to save stuff, and if 
we run the hash-object command again with -w, we get the hash, and we also save the content. Let's see where exactly. Let's peek inside 
the. git directory. There are a few files and folders here, but for now just look at this directory here, objects. This is called the 
object database. It's the place where Git saves all its objects like the string Apple Pie we just saved. Let's peek inside. 

 Ignore these two, the info and pack subdirectories for now, they're not important. Instead, look at this subdirectory here. Its name is 
 23, and these are the first two hexadecimal digits of the SHA1 of the content we just saved. And if we look inside 23, there is a file 
 in  here, and the name of this file is the remaining digits of the SHA1!
 
 
Git uses this scheme to organize content and spread it over multiple directories. It's just a trick to avoid piling up all the content 
into a single huge cluttered directory. Our original string, Apple Pie, is inside this file. This is what Git calls a blob of data, a blog 
is a generic piece of content. However, the original string has been mangled a bit inside the file. Git added a small header and 
compressed the content to save space. 


So we cannot just open the file and read it, but we can use another low-level plumbing command to 
look at the content. It's called $git cat-file. Once again, don't worry if you don't remember this command. It's rarely used. I'm using 
it now just because I want to show you how Git saves content. Git cat-file takes the SHA1 of an object and an argument. If we run it 
with the -t argument, it stands for type, Git tells us what this piece of content is, it's a blob. 

$git cat-file 23991897e13e47ed0adb91a0082c31c82fe0cbe5 -t




$git cat-file 23991897e13e47ed0adb91a0082c31c82fe0cbe5 -p

And if we run it again with -p, for pretty 
printing, then Git unzips the object, removes the header, and it prints out the actual content of the blob. And here it is, the string 
Apple Pie, there. So far, we have seen that Git is able to take any piece of content, generate a key for it, a SHA1, and then persist the content into the repository as a blob, a persistent map. This is the very basic of the Git model. Let's build on this, and move on to the next layer of the onion.
