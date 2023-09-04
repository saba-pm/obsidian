we create this file to write all env if you like you can add  ==aws_access_key = "" , aws_secret_key = ""==

```
variable "key_name" {

  description = "Key to access the EC2 instance"

  type = string

  default = "terraform"

}
```