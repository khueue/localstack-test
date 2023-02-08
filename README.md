# localstack-test

A simple setup to showcase the following:

- Run localstack (in docker compose).
- Run a separate "shell" container attached to the same network, providing:
  - `terraform`, to provision infrastructure within localstack.
  - `awslocal`, an awscli wrapper to work with localstack.

# Usage

**Requirements:**

- Docker (and Compose).
- POSIX tools: Bash, Make.

## 1. Clone the repo

## 2. In one terminal

Launch localstack:

```
$ cd localstack
$ docker compose up
```

## 3. In another terminal

```
$ cd shell
$ make shell
```

Continue within the container:

```
$ cd /terraform/test-project
$ terraform init
$ terraform apply

...
aws_s3_bucket.my_bucket: Creating...
aws_s3_bucket.my_bucket: Creation complete after 1s [id=my-test-bucket]

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
```

Still in the same container:

```
$ awslocal s3 ls
2023-02-08 14:31:20 my-test-bucket
```

Voila! You have now set up localstack and tools to manage its infrastructure.
Add more services to docker-compose.yml as you see fit.
