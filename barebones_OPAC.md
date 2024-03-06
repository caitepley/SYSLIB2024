## Creating a Bare Bones OPAC
I was able to pretty easily follow the process of logging into MySQL and accessing the opacdb database from last week's notes (install_and_setup_LAMP_stack.md). However, writing the SQL to manipulate the
data in the database is still tripping me up.
### Example of me writing horrible SQL:
![image](https://github.com/caitepley/SYSLIB2024/assets/148588703/9702e95c-178b-4814-9a02-76e2898e6c89)
Writing SQL statements in the terminal is much less forgiving than writing them in database management software.

However, once I got the statement right, it was very rewarding.
![image](https://github.com/caitepley/SYSLIB2024/assets/148588703/15ef86dc-b79a-4342-a6ce-e746c3ecefcf)
The 'Query OK' statement gave me some hope that I might actually kinda know what I'm doing. 

Once I added some more books, I had this:
![image](https://github.com/caitepley/SYSLIB2024/assets/148588703/3eacefdd-5e5a-4223-8d98-d050b4af1aa7)


Navigating to the search.php page in the browser (http://<VM IP address>/search.php), we can search for books in the opacb database:

![image](https://github.com/caitepley/SYSLIB2024/assets/148588703/d6bc25c3-7233-4755-aac7-92c2f20eecc8)

The results look like this:

![image](https://github.com/caitepley/SYSLIB2024/assets/148588703/2b95a284-4a50-425f-b88d-6ad0145a5a3c)


## Final Thoughts
It was pretty fun to be able to easily create, edit, and delete items from a small database in MySQL. However, it did seem very tedious to enter MySQL queries
into the terminal. If you mess up, it is a lot harder to go back and edit what you have already done. I definitely prefer writing SQL statements in something like Postgres 
or even Microsoft Access. I can see how using the terminal to manage databases could be preferable if you know what you are doing; you probably have a lot more freedom to do 
what you want because you don't need to stay within the confines of the DBMS.


