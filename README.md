# ELogging-Framework
Logging Framework created by extending JUL Framework . Extending  FileHandler by providing Mulitple FileHandling Manager with Level restrictions. Introducing Extended Logging Bifurcation  .Introducing DB Logging . 
Internally ELogger handles prefix to match the Log entries do by your application. Other Global Logging done by external Jars/Classes will not be captured.
# Usage:
Include Jar in ClassPath

# Create Property File
# Sample : 
# Global
handlers=com.ejohn.logger.ERootFileHandler,com.ejohn.logger.EJdbcHandler
.level=ALL

# RootFileHandler Manager Props
# FileHandler Count
com.ejohn.logger.ERootFileHandler.handler_count=2
# FileHandler Names   . Note: names>count . If 2 names are configured and count is 1 then count is updated to 2
com.ejohn.logger.ERootFileHandler.handler_names=system.severe,system

# Level Bifurcation is done by Prefic 'A-' : Inclusive Above  , 'B-' : Inclusive Below or 'INFO' : Only INFO Logging
# system.severe Props
system.severe.pattern=log_S_%u_%g.log
system.severe.limit=50000
system.severe.count=1
system.severe.append=false
# Only SEVERE Logging will go to this File
system.severe.level=SEVERE   
system.severe.formatter=com.ejohn.logger.EFormatter
system.severe.formatter.format_id=3
system.severe.output_service=com.ejohn.logger.E_LoggingTest

# system Props
system.pattern=log_Below_Severe_%u_%g.log
system.limit=50000
system.count=1
system.append=false
# All Logging Below SEVERE (Including SEVERE) will go to this File
system.level=B-SEVERE
system.formatter=com.ejohn.logger.EFormatter
system.formatter.format_id=3

# DB Handler Props
com.ejohn.logger.EJdbcHandler.dbType=org.postgresql.Driver
com.ejohn.logger.EJdbcHandler.dbURL=jdbc:postgresql://localhost:5432/test112233
com.ejohn.logger.EJdbcHandler.dbUser=postgre
com.ejohn.logger.EJdbcHandler.dbPassword=112233
# below is the default Format User by EFormatter for SQL
#INSERT INTO #table_name ( time_stamp, source, name, level, message, thread_id, error_msg, error_trace) VALUES ( \'%1$tF %1$tT\',\'%2$s\',\'%3$s\',\'%4$-7s\',\'%5$s\',\'%6$s\',\'%7$s\',\'%8$s\')
com.ejohn.logger.EJdbcHandler.sqlTable=table_log
com.ejohn.logger.EJdbcHandler.level=SEVERE
com.ejohn.logger.EJdbcHandler.formatter=com.ejohn.logger.EFormatter

