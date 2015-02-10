# Building with the MyDrive docker deb-builder image

    docker run --rm -i -v `pwd`:/usr/src/myapp -w /usr/src/myapp mydrive/precise-deb-builder make deb

# Uploading the built package to an s3 repo using [deb-s3](https://github.com/krobertson/deb-s3)

    deb-s3 upload --bucket <your bucket> --arch amd64 <path-to-newly-build-deb-file>

# apt-s3
additional "s3" protocol for apt so you can host your giant apt repository in s3 on the cheap!

Author: Kyle Shank

We use this for pressflip.com to deploy and distribute all of our software.  apt is a great packaging system and s3 is a great place to backup/store static files.  apt-s3 is especially useful and fast if you are hosting your servers within EC2.

THIS NEEDS MORE DOCUMENTATION OBVIOUSLY

TODO
----
This has to be compiled with the source version of apt.

Once compiled, the resulting s3 binary must be placed in /usr/lib/apt/methods/ along with the other protocol binaries.

Finally, this is how you add it to the /etc/apt/sources.list file:

deb s3://AWS_ACCESS_ID:[AWS_SECRET_KEY_IN_BRACKETS]@s3.amazonaws.com/BUCKETNAME prod main

Simply upload all of your .deb packages and Packages.gz file into the s3 bucket you chose with the file key mapping that matches the file system layout.
