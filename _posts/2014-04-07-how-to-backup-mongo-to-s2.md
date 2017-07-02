---
layout: post
title:  "How to backup my MongoDB to Amazon S3?"
date:   2014-04-07 13:36:32 +0300
categories: placeholder
permalink: "how-to-backup-my-mongodb-to-amazon-s3/"
---

I searched a lot for an easy script that would give me an option to easily make a daily backup of my [MongoDB][link1] database and then upload the backup to [Amazon S3][link2].

I found a few solutions, but they did not did exactly what I wanted.

I found one that did exactly what I wanted, but it was for MySQL, So… I converted that script to do the same with MongoDB and now it is [available for you to use on Github][link3].

You can make daily, weekly and monthly backups. it can be automated through CRON. The only dependency is ‘[s3cmd][link4]‘ which is a really recommended for everyone who uses Amazon S3.

The code is really simple, and I’ll put it here, but if you want the latest version – download it from the project [Github repository][link3].

{% highlight javascript %}
#!/bin/sh

# Updates etc at: https://github.com/gmadar/MongoDB-backup-to-Amazon-S3
# Under a MIT license

# change these variables to what you need
S3BUCKET=bucketName
FILENAME=mongo.backup
COLLECTION=''
# the following line prefixes the backups with the defined directory. it must be blank or end with a /
S3PATH=mongodb_backup/
# when running via cron, the PATHs MIGHT be different. If you have a custom/manual MYSQL install, you should set this manually like MONGODUMPPATH=/usr/local/mongo/bin/
MONGODUMPPATH=/temp/mongo/dump/
#tmp path.
TMP_PATH=~/

DATESTAMP=$(date +".%m.%d.%Y")
DAY=$(date +"%d")
DAYOFWEEK=$(date +"%A")

PERIOD=${1-day}
if [ ${PERIOD} = "auto" ]; then
	if [ ${DAY} = "01" ]; then
        	PERIOD=month
	elif [ ${DAYOFWEEK} = "Sunday" ]; then
        	PERIOD=week
	else
       		PERIOD=day
	fi	
fi

echo "Selected period: $PERIOD."

echo "Starting backing up the database to a '${MONGODUMPPATH}' folder..."

# actual-dump:
mongodump -o ${MONGODUMPPATH}

echo "Done dumping the Mongo database"
echo "Starting compression..."

tar czf ${TMP_PATH}${FILENAME}${DATESTAMP}.tar.gz ${MONGODUMPPATH}

echo "Done compressing the dump folder."

# we want at least two backups, two months, two weeks, and two days
echo "Removing old backup (2 ${PERIOD}s ago)..."
s3cmd del --recursive s3://${S3BUCKET}/${S3PATH}previous_${PERIOD}/
echo "Old backup removed."

echo "Moving the backup from past $PERIOD to another folder..."
s3cmd mv --recursive s3://${S3BUCKET}/${S3PATH}${PERIOD}/ s3://${S3BUCKET}/${S3PATH}previous_${PERIOD}/
echo "Past backup moved."

# upload all databases
echo "Uploading the new backup..."
s3cmd put -f ${TMP_PATH}${FILENAME}${DATESTAMP}.tar.gz s3://${S3BUCKET}/${S3PATH}${PERIOD}/
echo "New backup uploaded."

echo "Removing the dump + compressed files..."
# remove databases dump
rm -rf ${MONGODUMPPATH}
rm ${TMP_PATH}${FILENAME}${DATESTAMP}.tar.gz
echo "Files removed."
echo "All done."
{% endhighlight %}

[link1]: https://www.mongodb.com/
[link2]: https://aws.amazon.com/s3/
[link3]: https://github.com/gmadar/MongoDB-backup-to-Amazon-S3
[link4]: http://s3tools.org/s3cmd
