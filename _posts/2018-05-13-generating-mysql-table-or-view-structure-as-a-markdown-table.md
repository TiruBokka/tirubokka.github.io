---
layout: post
title:  "Generating MySQL Table or View Structure as a Markdown Table"
date:   2018-05-12 18:45:00 +0530
categories: mysql script documentation markdown
---
The following script snippet prints the structure of a MySQL table (or view) as a [Markdown](https://daringfireball.net/projects/markdown/) table:

```bash
echo "|Field | Type | Null | Key | Default | Extra|"
echo "|-|-|-|-|-|-|"
mysql -u$DB_USER -p$DB_PASSWORD $DB_NAME -e "DESCRIBE $OBJECT_NAME" 2> /dev/null |\
tail -n +2 | sed -e 's/	/ | /g' -e 's/^/| /' -e 's/$/ |/'
```

The script's output can then be pasted into a document such that it produces:

|Field | Type | Null | Key | Default | Extra|
|-|-|-|-|-|-|
| cust_id | char(10) | NO | PRI | NULL |  |
| cust_name | char(50) | NO |  | NULL |  |
| cust_address | char(50) | YES |  | NULL |  |
| cust_city | char(50) | YES |  | NULL |  |
| cust_state | char(5) | YES |  | NULL |  |
| cust_zip | char(10) | YES |  | NULL |  |
| cust_country | char(50) | YES |  | NULL |  |
| cust_contact | char(50) | YES |  | NULL |  |
| cust_email | char(255) | YES |  | NULL |  |

rather than pasting the the output of DESCRIBE command as pre-formatted text:

```
+--------------+-----------+------+-----+---------+-------+
| Field        | Type      | Null | Key | Default | Extra |
+--------------+-----------+------+-----+---------+-------+
| cust_id      | char(10)  | NO   | PRI | NULL    |       |
| cust_name    | char(50)  | NO   |     | NULL    |       |
| cust_address | char(50)  | YES  |     | NULL    |       |
| cust_city    | char(50)  | YES  |     | NULL    |       |
| cust_state   | char(5)   | YES  |     | NULL    |       |
| cust_zip     | char(10)  | YES  |     | NULL    |       |
| cust_country | char(50)  | YES  |     | NULL    |       |
| cust_contact | char(50)  | YES  |     | NULL    |       |
| cust_email   | char(255) | YES  |     | NULL    |       |
+--------------+-----------+------+-----+---------+-------+
```

The complete script can be downloaded from my [GitHub repo](https://raw.githubusercontent.com/TiruBokka/ShellScripts/master/mysql2markdown).

The Customers table shown above is from the example database from the book [*Sams Teach Yourself SQL in 10 Minutes* by *Ben Forta*](http://a.co/h9Ku6CE).
