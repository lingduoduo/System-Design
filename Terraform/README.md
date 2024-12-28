https://developer.hashicorp.com/terraform/docs

# IaC Core Principal

| **Concept**                  | **Description**                                                                 |
|------------------------------|---------------------------------------------------------------------------------|
| **Versioned infrastructure** | Multiple versions of code that should be under source control.                 |
| **Idempotence**              | Consistency, no matter how many times it is run.                               |
| **Self-describing infrastructure** | The infrastructure is the code and can be understood by people easily.         |

* Use `terraform` commands: `init`, `fmt`, `validate`, `plan`, `apply`, `destroy`

| **Step**  | **Description**                                                                                 |
|-----------|-------------------------------------------------------------------------------------------------|
| **Write** | Code your Terraform configuration file in its own working directory. Initialize the directory.  |
| **Plan**  | Verify that the configuration is valid and review the Terraform plan.                           |
| **Apply** | Build the infrastructure based on the Terraform configuration.                                  |

---


# Installing Terraform

## Install Terraform from the Hashicorp Terraform installation web page:

Link: https://developer.hashicorp.com/terraform/downloads 

Link #2: https://learn.hashicorp.com/tutorials/terraform/install-cli 

You can install Terraform manually or from a package manager. For now, I recommend using a package manager because it is the easiest way for beginners. 

For example:

- Linux (apt, dnf, or other package manager)
- macOS: Homebrew - install it at https://brew.sh
- Windows: Chocolatey - install it at https://chocolatey.org

Locate your operating system and install Terraform following the step-by-step directions at the HashiCorp website.

> Note: You might also opt to install the latest binary. To do so, go to https://releases.hashicorp.com/terraform. Locate the latest version for your platform, download it, verify the checksum, unzip it, and copy it to your binaries directory (for example, /usr/local/bin).
> For a video demonstration of the binary version install of Terraform, go to my website: https://prowse.tech/terraform-binary-install-linux.  


## Verify that Terraform is installed and view the version.
`terraform version` 

or

`terraform -v`

---

# Install Terraform Autocomplete

While the Bash shell can perform auto-completion of commands, such as the `terraform` command, it will not be able to auto complete terraform subcommands such as `terraform version`. 

Terraform autocomplete takes care of that second part for you. 

- First, if you are using the Bash shell, make sure that you have an existing .bashrc file.
  
  If not, create a blank one, for example: 
    
    `touch ~/.bashrc`

- Install autocomplete: 

  `terraform -install-autocomplete`

- Restart the shell

- Test this with by typing only the first three letters of a terraform subcommand. ("ver" instead of "version"). Make sure it works!
  For example, type:

`terraform ver` 

and then press the tab key. It should complete the word "version" for you. There it is, tab completion is great.

**USE AUTO-COMPLETION!** Over time it can save you millions of keystrokes - literally. 

`terraform -h`

> Note: This is very helpful for Bash, but not quite as necessary for other shells such as Fish or ZSH. 

---

```
<block type> "<block label>" "<block label name>" {
  <identifier> = <expression> 
}
```
> "block label name" is the Terraform name, or Terraform ID. 
> The identifier = expression argument might also be referred to as a key-value pair or simply attributes.

A real example of this would be:

```hcl
resource "aws_instance" "app_server" {
  ami = "ami-0c7df786sdf3ghf0f"
}
```

```
terraform fmt
terraform init
terraform validate
terraform plan -out=plan-output
terraform apply
terrafrom destroy
```
