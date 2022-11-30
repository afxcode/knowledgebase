Prerequisites Install the Microsoft ODBC driver for SQL Server

```bash
if ! [[ "18.04 20.04 22.04" == *"$(lsb_release -rs)"* ]];
then
    echo "Ubuntu $(lsb_release -rs) is not currently supported.";
    exit;
fi

sudo su
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -

curl https://packages.microsoft.com/config/ubuntu/$(lsb_release -rs)/prod.list > /etc/apt/sources.list.d/mssql-release.list

exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install -y msodbcsql18

# optional: for bcp and sqlcmd
echo 'export PATH="$PATH:/opt/mssql-tools18/bin"' >> ~/.zshrc

sudo apt-get install -y unixodbc-dev
```

Install the PHP drivers for Microsoft SQL Server
```bash
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
printf "; priority=20\nextension=sqlsrv.so\n" > /etc/php/7.4/mods-available/sqlsrv.ini
printf "; priority=30\nextension=pdo_sqlsrv.so\n" > /etc/php/7.4/mods-available/pdo_sqlsrv.ini
exit
sudo phpenmod -v 7.4 sqlsrv pdo_sqlsrv
```

Install Apache and configure driver loading
```bash
sudo su
apt-get install libapache2-mod-php8.1 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.4
exit
```
