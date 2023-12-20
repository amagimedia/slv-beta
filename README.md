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

ID (Public Key):  SLV_EPK_6pKu2fWP9sUut7Ux5Ge3Z91ooqqCFX1pwtEafq84Jd7TFiS
Name:             alice
Email:            alice@example.com
Tags:             []

Env Data:  SLV_EDS_2kUTPLXjtGkGZ3Kt9XESJSxB8duee1yoMNry4S7x8u3gg45APFrEDUJJfgzrtdeRuFgRYkS6ZB9z68vs8fjGPu1bUSXy4jvCxTp1KddUhTSTnoNsUYaEEMVTkyzwdC9oRho5uezE498ASWro4zULUU4XTQS5NdgsLAd9a5Km8KBaTFFHgyweWNf2ndfDQh9owDZBVrdDQZE2AZzAAycqfA

Secret Key: SLV_ESK_6o234DMAdSPBfVVBTy1AGTBvRSHPNRiptJ8mAYBhcNfWoon
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
$ export SLV_SECRET_KEY=SLV_ESK_6o234DMAdSPBfVVBTy1AGTBvRSHPNRiptJ8mAYBhcNfWoon
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