# Docker-Projeqtor

This docker image provides a [Projeqtor](https://www.projeqtor.org) container with LDAP support.

This image is based on `php:7.4-apache`

Version of Projeqtor in this image is currently **9.2.2**

## Exposed ports :

- 80 : Projeqtor Webpanel

## Volumes

They are two volume mounted on this image :

- /mnt/documents
- /mnt/logs

Both need to have rw access

## Environment

Current used environments vars :

### PHP ENV

| Environment variable          | Default | Recommended                                                  |
| ----------------------------- | ------- | ------------------------------------------------------------ |
| PHP_MAX_INPUT_VARS            | 4000    | Must be > 2000 for real work allocation screen               |
| PHP_REQUEST_TERMINATE_TIMEOUT | 0       | Must not end requests on timeout to let cron run without ending |
| PHP_MAX_EXECUTION_TIME        | 30      | 30 is minimum advised                                        |
| PHP_MEMORY_LIMIT              | 512M    | 512M is minimum advised for PDF generation                   |

### Projeqtor ENV

| Name                         | Default       | Usage                                                        |
| ---------------------------- | ------------- | ------------------------------------------------------------ |
| PJT_DB_TYPE                  | mysql         | Database type. Can be `mysql` or `pgsql`                     |
| PJT_DB_HOST                  | 127.0.0.1     | Database host (server name)                                  |
| PJT_DB_PORT                  | 3306          | Database port                                                |
| PJT_DB_USER                  | root          | Database user to connect                                     |
| PJT_DB_PASSWORD              | root          | Database password for user                                   |
| PJT_DB_NAME                  | projeqtor     | Database schema name                                         |
| PJT_DB_PREFIX                | ***`empty`*** | Database prefix for table names                              |
| PJT_SSL_KEY                  | ***`empty`*** | SSL Certificate key path                                     |
| PJT_SSL_CERT                 | ***`empty`*** | SSL Certificate path                                         |
| PJT_SSL_CA                   | ***`empty`*** | SSL Certificate CA path                                      |
| PJT_ATTACHMENT_MAX_SIZE_MAIL | 2097152       | Max file size in email                                       |
| PJT_LOG_LEVEL                | 2             | Log level {'4' for script tracing, '3' for debug, '2' for general trace, '1' for error trace, '0' for none} |
| PJT_ENFORCE_UTF8             | 1             |                                                              |



## Installed PHP extensions

| Extension | Usage                                                        |
| --------- | ------------------------------------------------------------ |
| qd        | For reports graphs                                           |
| imap      | To retrieve mails to insert replay as notes                  |
| mbstring  | Mandatory. for UTF-8 compatibility                           |
| mysqli    | For default MySql database                                   |
| pgsql     | If database is PostgreSql                                    |
| pdo       | BDD connector                                                |
| pdo_mysql | For default MySql database                                   |
| pdo_pgsql | If database is PostgreSql                                    |
| openssl   | To send mails if smtp access is authentified (with user / password) |
| ldap      | Directory Access Protocol, and is a protocol used to access "Directory Servers" |
| zip       | ZipArchive class is mandatory to manage plugins and export to Excel format |

