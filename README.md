

# HelloGreengrassV2
## Install and Run AWS Greengrass V2

Follow these instructions to install and run AWS Greengrass Core on Debian 10.  This was tested with B&R Automation APC/PPC Industrial PC products and Debian 10 Buster.  

## Installation

Open an ssh session with the IPC
```
ssh <user>@<ip_address_of_device>
```

Update and upgrade (because you always do this):
```
sudo apt update && sudo apt upgrade
```

Add the users and groups:
```
sudo useradd --system ggc_user
sudo groupadd --system ggc_group
```

Add the cool stuff:
```
sudo apt install build-essential zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev wget curl python3-pip -y
```

Install the AWS cli:
```
pip3 install awscli --upgrade
```

Install AWS Coretto 8 openjdk:
```
wget https://corretto.aws/downloads/latest/amazon-corretto-8-x64-linux-jdk.deb
sudo apt-get update && sudo apt-get install java-common
sudo dpkg --install amazon-corretto-8-x64-linux-jdk.deb
java --version
```

Add your environmental variables:
```
export AWS_ACCESS_KEY_ID=<ADDYOURACCESSKEYID>
export AWS_SECRET_ACCESS_KEY=<ADDYOURSECRETACCESSKEY>
export AWS_ACCOUNT_ID=<ADDYOURACCOUNTID>
export AWS_REGION=<ADDYOURREGION>
```

Download the Greengrass Core install files:
```
curl -s https://d2s8p88vqu9w66.cloudfront.net/releases/greengrass-nucleus-latest.zip > greengrass-nucleus-latest.zip && unzip greengrass-nucleus-latest.zip -d GreengrassCore
```

Install the Greengrass Core and create the deployment:
```
sudo -E java -Droot="/greengrass/v2" -Dlog.store=FILE -jar ./GreengrassCore/lib/Greengrass.jar \
--aws-region us-west-2 --thing-name <YOURCORENAME> --thing-group-name <YOURGROUPNAME> --component-default-user \
ggc_user:ggc_group --provision true --setup-system-service true --deploy-dev-tools true
```

## Usage

See the YouTube link for usage.

## License
[MIT](https://choosealicense.com/licenses/mit/)
