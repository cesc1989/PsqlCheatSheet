# Multiple AWS Accounts

Place this code in `~/.profile` or in `~/.bash_profile`:

```bash
# Useful for changing between several AWS accounts configured in `~/.aws/credentials`.
#
# Examples:
#
#    $ setaws staging
#    $ setaws uat
setaws() {
  if [ $# -eq 0 ]
  then
    echo "No arguments supplied"
    echo "Example: setaws staging"
  else
    echo "Exporting aws profiles to: $1"
    export AWS_PROFILE=$1
    echo "export AWS_PROFILE=$1"
    export AWS_DEFAULT_PROFILE=$1
    echo "export AWS_DEFAULT_PROFILE=$1"
    export AWS_SDK_LOAD_CONFIG=1
  fi
}
```

And configure `~/.aws/config`:

```
$ cat ~/.aws/config 
[profile staging]
region = us-west-2
output = json

[profile uat]
region = us-west-2
output = json

[profile production]
region = us-east-1
output = json
```

finally, configure `~/.aws/credentials`:

```
$ cat ~/.aws/credentials 
[staging]
aws_access_key_id = [ACCESS_KEY_ID]
aws_secret_access_key = [SECRET_KEY_ID]

[uat]
aws_access_key_id = [ACCESS_KEY_ID]
aws_secret_access_key = [SECRET_KEY_ID]

[production]
aws_access_key_id = [ACCESS_KEY_ID]
aws_secret_access_key = [SECRET_KEY_ID]
```
