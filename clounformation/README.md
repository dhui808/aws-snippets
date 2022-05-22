### Sample LAMP Stack
    EC2 -> Key Pair -> mykp.pem
    
    CloudFormation
    
    DBName:MyDatabase
    DBPassword: Mysql2022
    DBRootPassword: Mysql2022
    DBUser: danny
    
    chmod 400 mykp.pem
    ssh ec2-user@172.31.85.52 -i mykp.pem
    
    curl localhost/index.php
    mysql --version
    mysql -h localhost -u root -p MyDatabase
    
