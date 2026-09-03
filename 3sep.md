## Reflection

ASCII tree 
why it is important??

Text-based interfaces are more robust and universal because text can work almost everywhere. A GUI depends on a graphical environment, display, window system, and other resources, while a CLI mainly needs a terminal.

Text is also very useful when working with remote computers or servers. For example, if we want to connect to a remote server, we can use a command-line interface and give commands to that machine and receive the output without needing a GUI.

This is especially useful for servers, cloud machines, and systems where a graphical interface may not be available.

So, text/CLI is preferred when we want simplicity, reliability, remote access, and low resource usage, whereas GUI is preferred when we want a more visual and user-friendly experience.



# how to draw it ?

we have a limited amount of characters currently being displayed in the window 
so putting them continuously with one indentation would make it not clearly visible 

For example,
aa  aa  aa      aa ...                        aaa...                                          ...    aa


after that we won't be able to put a new character because visually it won't be able to explain itself


so vertical is the solution

------ root 
|
|    ---- child 1
|    ---- child 2


and so on,
so we have entire next set of Characters dedicated to the name


