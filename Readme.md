ctrl + alt + delete = terminal shortcut

date = to check date and time. (Date will not work - case sensitive)

cal =  calender

cal -y = calender of the present year (sudo apt install ncal)

cal (year) 2019 = calender of the year specific year

cal month (1) year (2021) = calender with specific month and year

cal -3 = calender of previous, present and next month together

clear = clear the terminal

exit = close the terminal


-------------Navigating the file system----------

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
   

cd .. = takes you one directory back

Now lets say if you want to go back in you previous working directory foreg: krishna@krishna:~/Desktop/f1/f2/f3$

cd - = directly takes you to your previous current path.
