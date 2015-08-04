```bash
$ sudo yum install git
```

```bash
$ cd "your_directory"
```

```bash
$ git clone https://github.com/user_name/your_repository.git

Cloning into 'your_repository'...
Username for 'https://github.com': user_name
Password for 'https://user_name@github.com':
remote: Counting objects: 129, done.
remote: Compressing objects: 100% (13/13), done.
remote: Total 129 (delta 1), reused 0 (delta 0), pack-reused 115
Receiving objects: 100% (129/129), 24.04 MiB | 2.63 MiB/s, done.
Resolving deltas: 100% (46/46), done.
Checking connectivity... done.
```

```bash
$ git remote show origin

Username for 'https://github.com': user_name
Password for 'https://user_name@github.com':
* remote origin
  Fetch URL: https://github.com/user_name/your_repository.git
  Push  URL: https://github.com/user_name/your_repository.git
  HEAD branch: master
  Remote branches:
    master   tracked
    branch_1 tracked
  Local branch configured for 'git pull':
    master merges with remote master
  Local ref configured for 'git push':
    master pushes to master (up to date)
```


```bash
$ git checkout -b aws origin/aws

Branch aws set up to track remote branch aws from origin.
Switched to a new branch 'aws'
```
