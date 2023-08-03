+++
author = "Collin"
title = "Using Breach Data to Find a Lost Number"
description = "Gaining extra information from an email address"
date = 2023-08-03
+++

I wanted to text an old friend but only had their email. Here is how I found their number.

## Step 1: Email

Most people only use one email address for everything. This means that their email has probably been in a lot of data breaches. I used [have I been pwned](https://haveibeenpwned.com/) to check. I decided to use a breach that included their email, name, and phone number. This would give me enough info to confirm later that this is the correct person. [dehashed](https://dehashed.com/) and [intelligence x](https://intelx.io/) can also be used to find breaches if the ones on have I been pwned are not useful.

## Step 2: Follow the breach

Now it's time to find out where it can be accessed or downloaded from. I like to first go to [intelligence x](https://intelx.io/) as this will give the file name of the breach. This is important for google dorking the file itself. Sometimes if the file is a text file, intelligence will leave the part you need unobfuscated which would mean skipping downloading the breach. However, this time we are not so lucky.

Using the file name of the breach in a google dork gives us a link to a torrent on btdigg. btdigg is a site that hosts torrent files and I have found a lot of breaches on here. The torrent file is called MyCloud and is a collection of breaches which includes the one we are following.

## Step 3: Download the breach

Now that we have the torrent file for MyCloud, it's time to download what we want. I use [qBittorrent](https://www.qbittorrent.org/). I don't want to download the whole torrent file as we only want our one breach so I only select the file we need. Make sure to seed for a while after it's downloaded!

## Step 4: Access the breach

The breach is in a MySQL dump. We will need to load it into a database to access

```sudo mysql dbname < dump.sql```

inside MySQL run these commands

```use database_name;``` (this will switch to the database we loaded) 

```show tables;``` (shows all the tables in the database)

now run ```SELECT * FROM table WHERE email="email@test.com"``` but replace with the real table and email to find the phone number.

you could also do a grep on the dump file as it isn't a binary, but depending on how big the dump is, it will take a long time to complete. The loading into the database will also be slow if the dump is big too.

## Step 5: Success!

After finding the number and checking that it belongs to my friend using people search websites, I texted them and got a response!
