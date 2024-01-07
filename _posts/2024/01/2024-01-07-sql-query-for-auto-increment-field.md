---
layout: post
permalink: sql-query-for-auto-increment-field
title: MySQL query for an id column with an AUTO_INCREMENT field
date: 2024-01-07T12:00:24.116Z
description: A fix for a MySQL query with an AUTO_INCREMENT field
tags: [mysql, php]
---

While working on a project for a “Make a Spotify Clone from Scratch: JavaScript PHP and MySQL” course that I’m learning, I encountered an issue with making a query to the database.

The task was to set user-provided data like username, name, email, etc. into the database table. But the query provided in the course didn’t work for me.

I’ve struggled a bit but managed to find a solution.

**My setup:**

1. MAMP version 6.8
2. PHP version 7.4.33
3. mySQL version 5.7.39

**What I had:**

1. The database was set via the phpMyAdmin tool.
2. There were 8 columns in the database's `users` table.
3. The first column is `id` with a type of `INT` and has an `AUTO_INCREMENT` without any initial value.

<figure class="figure-centered">
  <img class="shadow" loading="lazy" src="/images/misc/users-table.webp" alt="Example of users table">
  <figcaption>Example of users table</figcaption>
</figure>

**Suggested query:**

So when I used the provided query it didn't work for me. The first parameter in the parenthesis is supposed to represent an `id` column.

```php
mysqli_query($this->con, "INSERT INTO users VALUES ('', '$un', '$fn', '$ln', '$em', '$encryptedPw', '$date', '$profilePic')");
```

This query returned `false`. And after debugging as suggested in the course, I received the following error for the given query:

> `#1366 - Incorrect integer value: '' for column 'id' at row 1`

<figure class="figure-centered">
  <img class="shadow" loading="lazy" src="/images/misc/mysql-type-error.webp" alt="MySQL type error">
  <figcaption>MySQL type error</figcaption>
</figure>

So it means that the provided value type was wrong for the `id` column.

**Solution:**

After some of research I've found out that for the `AUTO_INCREMENT` columns, you [can skip this parameter]((https://www.w3schools.com/mysql/mysql_autoincrement.asp){:target="_blank"}) in the query.

So, you would set all columns except the first one (the `id`), and the final query would look like this:

```php
mysqli_query($this->con, "INSERT INTO users (username, firstName, lastName, email, password, signUpDate, profilePic) VALUES ('$un', '$fn', '$ln', '$em', '$encryptedPw', '$date', '$profilePic')");
```
