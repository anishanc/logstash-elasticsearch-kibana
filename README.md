# logstash-elasticsearch-kibana

Sample Log 

20160927-210452.110|I|cpeg-001.anc.com|test_app-1.5-0||~|f324dfsdf23sd23||org.springframework.orm.hibernate3.LocalSessionFactoryBean:777|Building new Hibernate SessionFactory

Create a file for custom pattern --> ./custom_patterns/my_pattern.txt

CUST_DATETIME [0-9.-]+
SEPARATOR \|
MULTI_SEPARATOR \|\|\~\|


Updated the same in logstash config file:

filter {
  grok{
    patterns_dir => "./custom_patterns"

    match => [ "message", "%{CUST_DATETIME:orb_date}%{SEPARATOR}%{WORD:method}%{SEPARATOR}%{USERNAME:host_name}%{SEPARATOR}%{USERNAME:app_name_version}%{MULTI_SEPARATOR}%{USERNAME:session}%{SEPARATOR}%{DATA:class_name}%{SEPARATOR}%{GREEDYDATA:log_message}" ]

   }
}


