# SMTP example 1

Download <a href="https://raw.githubusercontent.com/ChristofSchwarz/qs_log4net_appender/master/smtp1/LocalLogConfig.xml">here</a>
and save it into folder C:\ProgramData\Qlik\Sense\Scheduler of your Sense Server node.

After download fix the following params in each <appender> block:
 * smtpHost, port, EnableSsl, Authentication, username, password ... is for your SMTP server
 * from ... email to show as the sender (a generic email usually)
 * to ... a comma-separated list of recipients
 * subject ... email subject, I recommend to mention the sense server name here
 * maybe adapt the conversionPattern if you want a different email body

This SMTP appender config assume that you have **multiple groups of recipients for different apps**. For this reason
there are two (or more) appenders blocks defined, called like SendMail1, SendMail2 ... This is defined on the top 
of the file and also included in the <appender-ref> tag at the bottom.

To accomplish different recipients for different apps, there are 1 to N sections with "whitelists" of filter settings, 
and - if you want all other reload failures to go to a default recipient list - one "blacklist" with the rest. 

You can base a filter on every column from the corresponding log file, in this case the one in
C:\ProgramData\Qlik\Sense\Log\Scheduler\Trace\<computername>_System_Scheduler.txt

## A whitelist looks like this:
```
	<filter type="log4net.Filter.PropertyFilter">
		<param name="key" value="AppName" />
		<param name="stringToMatch" value="Operations Monitor" />
	</filter>
	<filter type="log4net.Filter.PropertyFilter"> 
		<param name="key" value="AppId" /> 
		<param name="stringToMatch" value="68221483-9ee9-4633-ab8e-e3a9a9879249" /> 
	</filter> 
	<filter type="log4net.Filter.DenyAllFilter" />  
```
Note that it uses multiple PropertyFilter-stringToMatch combinations and will end with a
DenyAllFilter row. This means, "if none of the previous filters found something, then
the search is negative".

## A blacklist looks like this:
```
	<filter type="log4net.Filter.PropertyFilter">
		<param name="key" value="AppName" />
		<param name="stringToMatch" value="Operations Monitor" />
		<param name="acceptOnMatch" value="false" />
	</filter>
	<filter type="log4net.Filter.PropertyFilter">
		<param name="key" value="AppId" />
		<param name="stringToMatch" value="68221483-9ee9-4633-ab8e-e3a9a9879249" />
		<param name="acceptOnMatch" value="false" />
	</filter>
```
Note that each filter is reversed with acceptOnMatch=false to turn it into a meaning
AppName NOT equal to Operations Monitor. In case of a black list, do NOT add the 
line DenyAllFilters 
