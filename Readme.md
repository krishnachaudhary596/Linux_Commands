{
    ctrl + alt + delete = terminal shortcut

    ctrl + c = To kill any running process.

    fn + alt + f2 then press r and hit enter = This will refresh linux window.

    date = to check date and time. (Date will not work - case sensitive)

    cal =  calender

    cal -y = calender of the present year (sudo apt install ncal)

    cal (year) 2019 = calender of the year specific year

    cal month (1) year (2021) = calender with specific month and year

    cal -3 = calender of previous, present and next month together

    clear = clear the terminal

    exit = close the terminal
}


<b>-------------Navigating the file system----------</b>

{
    root directory = From "home" to "Other Location" to inside "computer"

    root dir also known as "/"

    root/bin = here you have your binary files

    root/home = usually we spend most of our time here

    root/lib = contains libraries

    pwd = print working directory

    ls = list files and folders of current directory

    cd = change directory

    cd ~ = jump to home directory

    There are two ways of traversing throught directories
        1. Absolute (You know full path already)
        2. Relative (You don't know path so you will start it from home or root (usually))

        Absolute
        {
            krishna@krishna:~$ cd /home/krishna/Desktop/f1/f2/f3

            krishna@krishna:~/Desktop/f1/f2/f3$
        }

        Relative
        {
            krishna@krishna:~$ cd ~

            krishna@krishna:~$ pwd
                /home/krishna

            krishna@krishna:~$ cd Desktop

            krishna@krishna:~/Desktop$ ls
                f1
            krishna@krishna:~/Desktop$ cd f1

            krishna@krishna:~/Desktop/f1$ ls
                f2
            krishna@krishna:~/Desktop/f1$ cd f2

            krishna@krishna:~/Desktop/f1/f2$ ls
                f3
            krishna@krishna:~/Desktop/f1/f2$ cd f3

            krishna@krishna:~/Desktop/f1/f2/f3$ ls

            krishna@krishna:~/Desktop/f1/f2/f3$ 
    }
   

    cd .. or cd = takes you one directory back

    Now lets say if you want to go back in you previous working directory foreg: krishna@krishna:~/Desktop/f1/f2/f3$

    cd - = directly takes you to your previous current path.
}

<b>-------------Hard Link VS Soft Link---------</b>
{
    For linux links you need to remember iNode, which means index node.

        1. Every file and directory has an inode.
        2. It contains all the information except the file contents & name.
            foreg:➢	inode number
                    ➢	File size
                    ➢	Owner information
                    ➢	Permissions
                    ➢	File type
                    ➢	Number of link etc.

    <b>-------Types of Links--------</b>
        1. Soft Link:
            ✔	Just like a shortcut in Window
            ✔	It is a pointer to the original file
            ✔	Different iNode number
            ✔	Smaller file size
            
            Note :- If we delete the original file then softlink will become useless!
        2. Hard Link:
            ✔	Different name of the same file (like we wo do copy & paste and then change the name)
            ✔	Same file size
            ✔	Same iNode number

            Note :- If the original File is deleted, the Hard link will still contain the data that were in the original file.
    ls -i = list the files with their index node.

    ln old_file_name new_file_name = this will create hard link of the given file. (Now if you do ls -i then you will find hardlink of original and copy are same, there will be no issue if we delete original. Hard links are not allowed for directory.)

    ln -s old_file_name new_file_name = this will create soft link of the given file.(Here the inode gets changed. Now if you do delete original file then you will find there will be issue. Soft links are allowed for directory(inode gets changed).))
    
}

{
    <b>--------A Directory Loop-------</b>
    What is it? 
        folder inside folder.
    lets say we have a and inside it we have b and we want to make shortcut of a as c inside b.

    There are two way's of doing it.

    Using abolute path method:
        ln -s path_of_dir new_name_of_dir = this will create a shortcut of directory.

            -> First navigate to the end directory means a/b.
            -> then type this command (ln -s path_of_dir new_name_of_dir), in my case it is ln -s /home/krishna/Desktop/a c.
            -> Done. your loop directory for a(folder) inside b(folder) has been created.
            -> Now if you go inside a/b you will c and if you will open c then you get into loop 
            foreg: /home/krishna/Desktop/a/b/c/b. 
            Refer absolute_directory_loop.png image for better unerstanding.

        Using relative path method:
        ln -s path_of_dir new_nam_of_dir = same comand as earlier.

            -> You have to manually go the directory (I have already explained about how you can use relative path)
            -> Once you reached type this command: ln -s ~/Desktop/a c. 
            Refer relative_directory_loop.png image for better unerstanding.

        Now if you want to make directory loop of parent folder only then:
            -> Navigate to the parent folder.
            -> Type this command : ls -s .. f4(this is name of shortcut).
            Refer parent_directory_loop.png image for better unerstanding.           
}

 <b>--------ls Command options - Part 1-------</b>
 {
    ls -l = This command is used for long listing. It shows many informations about a file, like permission, no. of links, owner, group, file size, modification date, file name.
    {
        drwxrwxr-x 3 krishna krishna 4096 Aug 26 17:32  a

        -> d: this in the beginning represents directory.
        -> rwxrwxr-x: this represents permissions related to it.
        -> 3: this represents no. of hardlinks.
        -> krishna: This represents user.
        -> krishna: This represents Group.
        -> 4096: This represents size.
        -> Aug 26: Aug 26 last modification date.
        -> 17:32: This represents last modified time.
        -> a: This represents file/directory name.
    }

    ls ­-a = This is a list all command. This will list all the files in your current working directories including hidden files that start with . Press ctrl + h unhide the file.
    {
        . = this represents current directory.
        .. = This represents parent directory.
    }

    ls -t = This will list the files sorted by modification date. Newest first

    ls -r = This will list the files in reversed fashion.

    ls -i = This will list the index node number of each file in the current working directory.


 <b>The recusrive option !</b>
 {
    When a function call itself is known is recursive method.

    ls ­-R = if you want to list the contents of a directory and all it's subdirectories then use this command.
        
        ● For example, Imagine if you have a directory named dir1 on your desktop, and inside dir1 you have a subdirectory named dir2.
        Now, if you type ls -­R dir1, Then this will list the contents of dir1 and dir2.
        
        ● Here comes the interesting part, if you executed ls ­R /, then this will list all the files (non hidden) on your system.  (ctrl + c = To kill any running process.)
 }
 <b>Merging</b>
 {
    We can merge different commands to get some summarize output.

    foreg: ls -i -l, ls -il here both the form will work. Also we can add more commands in it. Like ls -ilrt etc.

    NOTE: Here order doesn't matter for writing commands. System has pre-built order.
 }

{
    <b>--------Working with Files in Linux-------</b>
    {
        <b>Touch Command</b>
        {
           The touch command is the easiest way to create new, empty files.
           If you want to create an empty file (not a directory) then you just type touch yourfilename
           You can also create multiple files at the same time.
                For example: touch file1 file2 file3 will create 3 new empty files named file1,file2 and file3 respectively.

        <b>Another use for the touch command</b>
            Touch is also used to update the timestamp (Modification date) for an existing file.          For example: if you already have a file named oldfile then touch oldfile will change the timestamp of oldfile to the current time.
            <b>Similarily</b>
            touch oldfile1 oldfile2 oldfile3 will change the timestamp of oldfile1,oldfile2 and oldfile3 to the current time.
        }
        <b>Make and Remove Directory</b>
        {
            mkdir = This command is used to create new directory. You can also create multiple direcotry at the same time.
            For example: mkdir dir1 dir2 dir3 will create 3 new empty directory named dir1 dir2 and dir3 respectively.
            
            rm dir or file = This command is used to remove empty directory. You can also remove multiple directory (but only empty one )at the same time.
            For example: rmdir dir1 dir2 dir3 will remove 3 new empty directory named dir1 dir2 and dir3 respectively.
            NOTE: It will remove only empty directory.

            rm -R/r dir/file =  This command will remove non-empty directory and file. You can also remove multiple directory at the same time.

            rm -iR/r dir = (i is for interactive) this command will delete non-empty directory with confirmation message displaying. Same can be used for files. 

            rm -f file/dir =  Force remove wheater the files exist or not.

            v = verbose (summary)

            rm -r/Rv dir = Removes the directory with giving summary.
        }
    }
    {
        <b>Copy file to any location</b>
        {
            cp file1 file2 = This will copy content of file1 into file2 if you have file2 already exist else if you don't have file2 then it will create file2 and copy the content of file1 into it. Overwrite will happen here.

            cp file1 file2 dir = This command will copy file1 & file2 in specific directory. Overwrite will happen here.

            cp -i file1 file2 dir = This will work same as above command but now it's interactive so you can choose whether you want to overwrite or not.

            cp -R dir1 dir2 = This command will copy entire dir1 to dir2, -R is used for recursive.

            cp -Rv dir1 dir2 = This command will copy entire dir1 to dir2, -v is used for verbose.
        }
        <b>Rename and move file</b>
        {
            mv old_file_name new_file_name = This command wil change the file name.

            mv old_file_name old_file_name = This command wil change the file name but it will overwrite the content of previous file.

            You can also rename any hidden file in the same way vise versa.

            mv old_dir_name new_dir_name = This command wil change the directory name.

            mv file_name dir_name = This command will cut and paste the file into dir. Same can be applied to multiple files. Overwrite will happen for existing file.

            mv -i file1 dir2 = This command will make it interactive whether we want to overwrite our content or not.

            In the same way we can integrate other commands also.
        }
        <b>Change extension and use of "file" command</b>
        {
            Changing the file extension will not affect actuall file.
            foreg: mv logo.png logo
            Above I have removed the extension of file but it will still work as usual.

            file filename = This file command is helpful to check the type of file.   
        }
        <b>How to add space in filename</b>
        {
            mkdir 'file with space' = You can use single quotes or double quotes to add space while creating file or directory.

            mkdir my\ cat = Work as above 
            \ = escape character, \\, \\\\
        }
        <b>Add special character in filename</b>
        {
            mkdir \$file or mkdir \"file\" = Both the commands will create file with special characters.
        }
        <b>Autocompletion and Keyboard Shortcuts</b>
        {
            tab key can be used for autocompletion in terminal.

            Ctrl + A	Move your	cursor to the beginning of the line.
		
            Ctrl + E	Move your cursor to the End of the line (E ­­ > end).

            Ctrl + D	Delete the character at the cursor location.

            Ctrl + F	Move your cursor Forward one character. Same as your right arrow key.
                    
            Ctrl + B	Move your cursor Backward one character. Same as your left arrow key.
                    
            Alt + F	Move your cursor Forward one word (Jump to the next word).

            Alt + B	Move your cursor Backward one word (Jump to the previous word).

            Alt + L	Convert all the characters beginning from the cursor location to end of the word to Lowercase.
                
            Alt + U	Convert all the characters beginning from the cursor location to end of the word to Uppercase.
                
            Ctrl + K	Cut the text from the cursor location to the end of the line. In Linux, we say Kill text Just like Cut text)
                
            Ctrl + U	Cut the text from the cursor location to the beginning of the line.

            Ctrl + Y	Paste the text that you did cut. Pasting in Linux is Yanking.

            Ctrl + L	Clear the screen just like the clear command.

        }
    }
}
{
    <b>Viewing and Editing files in Linux</b>
    {
        <b>Graphical Text Edit (gedit)</b>
        {
            
        }
    }
}