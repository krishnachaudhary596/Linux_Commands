{
    ctrl + alt + delete = terminal shortcut

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
 { tell prakash to run this command
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

 }