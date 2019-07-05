ansible_role_goofys
=========

Goofys allows you to mount an S3 bucket as a filey system.

Requirements
------------

Amazon AWS account, S3 bucket and EC2 virtual server(s) with RedHat.

Aws Credentials (aws_access_key_id, aws_secret_access_key)

[golang] (https://golang.org/)
[fuse] (https://github.com/s3fs-fuse/s3fs-fuse)

Role Variables
--------------

None.

Dependencies
------------

[geerlingguy.repo-epel](https://github.com/geerlingguy/ansible-role-repo-epel)

Or build from source with Go 1.9 or later

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
      - { role: geerlingguy.repo-epel }
      - { role: kaihei777.ansible_role_goofys }

Usage
-------

```ShellSession
$ cat ~/.aws/credentials
[default]
aws_access_key_id = AKID1234567890
aws_secret_access_key = MY-SECRET-KEY
$ $GOPATH/bin/goofys <bucket> <mountpoint>
$ $GOPATH/bin/goofys <bucket:prefix> <mountpoint> # if you only want to mount objects under a prefix
```

Users can also configure credentials via the
[AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html)
or the `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` environment variables.

To mount an S3 bucket on startup, make sure the credential is
configured for `root`, and can add this to `/etc/fstab`:

```
goofys#bucket   /mnt/mountpoint        fuse     _netdev,allow_other,--file-mode=0666,--dir-mode=0777    0       0
```

Got more questions? Check out [questions other people asked](https://github.com/kahing/goofys/issues?utf8=%E2%9C%93&q=is%3Aissue%20label%3Aquestion%20)


License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
