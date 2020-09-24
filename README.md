# Log4Net Appender Settings

Qlik Sense Enterprise for Windows uses <a href="https://logging.apache.org/log4net">Apache Log4Net library</a>. This logging library also has a concept of appenders (plug-ins) 
that are triggered at the very moment when also a log line is created. This allows, for example with the smtpAppender, to instantly send an
email. This is what I am focussing on in this git.

Resource Links, key work is from Levi Turner
 - https://github.com/levi-turner/getting_notified_from_qliksense
 - https://community.qlik.com/t5/Qlik-Architecture-Deep-Dive-Blog/Getting-Notified-from-Qlik-Sense/ba-p/1582429
 - https://youtu.be/dnDqzN8pj70
 - https://help.qlik.com/en-US/sense-admin/September2020/Subsystems/DeployAdministerQSE/Content/Sense_DeployAdminister/QSEoW/Deploy_QSEoW/Server-Logging-Using-Appenders-QSRollingFileAppender-Built-in-Appenders.htm
 
I share the following configuration examples:

| Example | Description | 
| ------- | ----------- | 
| <a href="smtp0">0</a> | Simpliest case, one list of recipients for all app reload failures |
| <a href="smtp1">1</a> | Complex case, differnet list of recipients for different app's reload failures |

Enjoy
