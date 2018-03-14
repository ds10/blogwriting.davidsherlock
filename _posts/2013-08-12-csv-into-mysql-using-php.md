---
ID: 225
post_title: CSV into MySQL using PHP
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/csv-into-mysql-using-php/
published: true
post_date: 2013-08-12 14:50:14
---
I wanted to get various fields from a CSV into a MySQL table, it was a two second job. Here is is for anybody that needs it:

&nbsp;

[codesyntax lang="php"]
<pre>&lt;?php

//error reporting

error_reporting(E_ALL);

ini_set('display_errors', 1);

//1) connect to mysql

$db = new PDO('mysql:host=localhost;dbname=database;charset=utf8', 'username','password');

//2)

$row = 1;

if (($handle = fopen("tweets.csv", "r")) !== FALSE) {

    while (($data = fgetcsv($handle, 1000, ",")) !== FALSE) {

    print_r($data);

        $num = count($data);

        echo "&lt;p&gt; $num fields in line $row: &lt;br /&gt;&lt;/p&gt;n";

        $row++;

          $query = "INSERT INTO store(store, site, date) VALUES('$data[7]', 'twitter','$data[5]')";

          print $query;

          $result = $db-&gt;exec($query);

  print $result;

          print  $db-&gt;lastInsertId();

    }

    fclose($handle);

}

?&gt;</pre>
[/codesyntax]

&nbsp;