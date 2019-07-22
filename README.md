# vault-tokenhelper-env
Environment-variable driven vault token helper written in generic python

## purpose
The default vault token helper always uses the presence of the ~/.vault-token file.
This custom token helper empowers you to command token file location by environment variable.
For example you may have development/test/production separate environments all using different vault identities/servers.
This script has been tested for compatibility with os-pythons 2.7 and 3.6

## usage
Set the VAULT_TOKEN_PATH environment variable to the location you want vault to store a token.
Edit ~./.vault init file to contain `token_helper = "/full/path/to/environment-var-tokenhelper.py"`

## recommended installation
Consider the following setup which would install/configure the script to be stored in the /opt tree:
```
sudo mkdir -p /opt/vault-contrib/vault-tokenhelper-env
sudo bash -c "curl -L https://github.com/PeteW/vault-tokenhelper-env/archive/1.0.0.tar.gz > /tmp/vault-tokenhelper-env.tar.gz"
sudo tar -zxvf /tmp/vault-tokenhelper-env.tar.gz -C /opt/vault-contrib/vault-tokenhelper-env --strip=1
sudo chmod uga+x /opt/vault-contrib/vault-tokenhelper-env/vault-tokenhelper-env.py
echo 'token_helper = "/opt/vault-contrib/vault-tokenhelper-env/vault-tokenhelper-env.py"' >> ~/.vault
```
Installation testing:
```
export VAULT_TOKEN_PATH=~/.vault-token
vault token lookup
```
