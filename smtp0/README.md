# SMTP example 0

This SMTP appender config is the simpliest possible. Any app reload fail found on a particular Qlik Sense node 
will go to the same email recipients.

Download <a href="https://raw.githubusercontent.com/ChristofSchwarz/qs_log4net_appender/master/smtp0/LocalLogConfig.xml">here</a>
and save it into folder `C:\ProgramData\Qlik\Sense\Scheduler` of your Sense Server node.

After download fix the following params in the <appender> block:
 * smtpHost, port, EnableSsl, Authentication, username, password ... is for your SMTP server
 * from ... email to show as the sender (a generic email usually)
 * to ... a comma-separated list of recipients
 * subject ... email subject, I recommend to mention the sense server name here
 * maybe adapt the conversionPattern if you want a different email body

Since this example has no further filters than a Logging level of ERROR, there is just an &gt;elevator&lt; tag but no &gt;filter&lt; tags.
