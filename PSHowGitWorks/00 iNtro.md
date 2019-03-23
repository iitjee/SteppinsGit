When you think about Git, you probably think about the high-level user commands, the so called __*porcelain commands*__. You're probably 
familiar with the basic ones such as add and commit. And if you worked with a remote repository, then you probably also used push and 
pull, and if you worked with branches, then you used branch, checkout, merge, maybe even rebase. The list goes on. Some people even get a 
little bit deeper than these into the low-level commands, the so called __*plumbing commands*__, such as cat-file, hash-object, and a few 
more. 


These are the basic building bricks that the porcelain commands are built upon. You might never need to use the plumbing commands unless 
you're doing some advanced Git scripting or the like. Now understanding all these commands can be hard, some of them can be confusing; 
however, here is a key point, you could argue that the secret to Git is not about knowing the commands, either porcelain or plumbing. 
Instead, the secret to Git is about knowing the conceptual model behind Git. If you want to use Git safely and unleash all of its power, 
and not get in trouble, then don't look at the commands, look at the model instead. Once you do, the complexity of the Git commands kind 
of fades away. Suddenly Git looks simple, even elegant, I promise. You don't get stuck anymore. So if you really want to become a Git 
master, then you should understand the model, and then you will also understand the commands much more deeply after you understand the 
model. 


I just said that at its core, Git is a map. That means that it's a table with keys and values. What are the keys, and what are the values? 
Well, the values are just sequences of bytes, for example, the content of a text file, or even a binary file. Any sequence of bytes can be 
a value. You can give a value to Git, and it will calculate a key for it, a hash. Git calculates hashes with the SHA1 algorithm, it's 
SHA1, SHA1s are 20 bytes in hexadecimal format, so they are a sequence of 40 hex digits. This will be Git's key to store this content in 
the map. We can also calculate the SHA1 on the commandline. To do this, we need a command that you might never have heard about, because 
it's a low-level plumbing command, git hash-object. So let's pass our piece of content to hash-object. 

$git hash-object "Apple Pie"
//you only wish! you get an error.. it expects a file name


$ echo "Apple Pie" | git hash-object --stdin
// use the echo command to output this content, and then pipe the result into hash-object like this. I also need to tell hash-object to 
get its content from standard input.


by all practical purposes, SHA1s are unique. Not just unique in your project, you can think of them as if they were unique in the 
universe. You could put all of the data you will ever write in your life in the same Git repository, and Git would assign a different SHA1 
to each version of each file and each folder. That's a lot of data, you might get some performance problems, but still no collisions. 
Later in this training, when we talk about distribution, this piece of information will come useful. For now, I'm only mentioning it to 
say, if you have ever worried that two SHA1s might collide in your Git project, then stop worrying now.
