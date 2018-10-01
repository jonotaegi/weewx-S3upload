# weewx-s3

This repository is a fork of https://github.com/wmadill/weewx-S3upload,
a weeWX extension to sync web files to an AWS S3 bucket.

This is a weeWX extension to sync web files to an AWS S3 bucket.

Rather than serving the web pages generated by weeWX directly from a 
webserver running on the same system as weeWX, I upload those pages 
to an AWS S3 bucket. The bucket is configured to be a static website
and is costing me around USD 0.50/month. This is cheaper than usual 
website hosting and saves me the worry of someone hacking into the
system running weeWX.

This has been tested against weeWX 3.8.2.

## Setup

Before installing this extensions, get an S3 bucket at Amazon
https://aws.amazon.com/. Sign into the management consule, create an
account if necessary, then create an S3 bucket.

Search their help pages for how to set up the bucket as a static
website. You'll need to add a DNS record for the URL you choose for
accessing the bucket.

Install `s3cmd` from http://s3tools.org/s3cmd. It is a Python 2.x
tool so will run fine on the same computer as weeWX. This has been
tested with s3cmd 2.0.2.

## Installation instructions

1. Download the extension

  ```
  wget -O weewx-s3.zip https://github.com/jonotaegi/weewx-s3/archive/master.zip
  ```

2. Install the extension

  ```
  sudo wee_extension --install weewx-s3.zip
  ```

3. Modify the S3 stanza in weewx.conf and set your S3 access code,
secret token, and bucket name. You will get those when you set up
the bucket you want to use.

4. Restart weeWX

  ```
  sudo /etc/init.d/weewx restart
  ```

## Manual installation instructions:

1. Clone this repo

  ```
  git clone git@github.com:jonotaegi/weewx-s3 ~/weewx-s3
  ```

2. Copy files to the weeWX user directory

  ```
  cp -rp ~/weewx-s3skins/S3 /home/weewx/skins
  cp -rp ~/weewx-s3bin/user/s3.py /home/weewx/bin/user
  ```

3. Add the following to weewx.conf

  ```
  [StdReport]
      ...
      [[S3]]
          skin = S3
          access_key = 'REPLACE_WITH_YOUR_S3_ACCESS_KEY'
          secret_token ='REPLACE_WITH_YOUR_SECRET_TOKEN'
          bucket = 'REPLACE_WITH_THE_NAME_OF_YOUR_S3_BUCKET'
  ```

4. Restart weeWX

  ```
  sudo /etc/init.d/weewx restart
  ```
