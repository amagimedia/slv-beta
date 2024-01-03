# SLV - Secure Local Vault
Secure Local Vault - SLV (a.k.a Secrets Launch Vehicle 🔐🚀) is a tool to manage secrets locally in a secure manner. It is designed to be used by developers to manage secrets along with their code so that they can be shared with other developers and services in a secure manner.

SLV is designed based on the following **key principles**
 - Anyone can add or update secrets, however will not be able to read them unless they have access to the vault
 - An environment should have a single identity that will give access to all necessary secrets from any vault shared with it

 ## Installation
Download the latest SLV binary from the [releases](https://github.com/amagimedia/slv-beta/releases/latest) page and add it to your path.

SLV can also be installed with brew using the following command
```zsh
brew install amagimedia/tap/slv
```

## Usage

#### Create a new profile
```sh
$ slv profile new -n amagi

Created profile:  amagi
```

#### Create a new environment
```sh
$ slv env new -n alice -e alice@example.com --add

ID (Public Key):  SLV_EPK_AEAUL5MX7UWLB27DGCPMTBJ7EOFKN54W6LAWEAO3TEKWJH4DTRBSWBRDAC4I2UDWENT32TPYL5CCODACNKFC4KI
Name:             alice
Email:            alice@example.com
Tags:             []

Env Data:  SLV_EDS_AF4JYNGKJVV4EMA4QDY674R7S4OWVOSCJ3FZXGZGUZA5GZJ3JFLIGBESFAK4XSWYO4PWK6D4PB7D6YHOL4UQ4MWMQDQ2BXUPYLECGENEK7G65I7NTWRHLS27THMVTOTNIW3ZNOSB5ZMRCJ2IW6ZEFOXNDPRHMTYPR3XDSYLIKP35YCLNK62TLH5KMGWOHBDJXFTEQ3VAALWXGAAMH3CSCQAFEL5ZQHX5CK7H3PVG6A2FZ4XSZJSOP25CN5QZZ7V56XTRXYDSJ6UQEM26UZ4AUI4N4UKMWGJQYDXV6AAAAD7773YTH5MA

Secret Key: SLV_ESK_AEAELQO7YIQWBLSCPTGYUC3CZLBPCWFEGK45RDFCYJ3MRL22ZB4T7WS4
```

#### Create a vault
```sh
$ slv vault new -v test.slv -s alice

Created vault: test.slv
```

#### Add secrets to the vault
```sh
$ slv secret put -v test.slv -n db_password -s "super_secret_pwd"

Added secret: db_password to vault: test.slv
```

#### Get secrets from the vault
Set the environment variable `SLV_SECRET_KEY` to the secret key generated in the previous step
```sh
$ export SLV_SECRET_KEY=SLV_ESK_AEAELQO7YIQWBLSCPTGYUC3CZLBPCWFEGK45RDFCYJ3MRL22ZB4T7WS4
$ slv secret get -v test.slv -n db_password

super_secret_pwd
```

#### Share the vault with other environments
Ensure that the current environment has access to the vault in order to share it with other environments
```sh
$ slv vault share -v test.slv -s bob

Shared vault: test.slv
```
Once shared, the other environments can access the vault using their respective secret keys