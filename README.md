## pre-requisites

Docker && Docker-Compose

Bash functions manager:
https://github.com/rcmorano/baids
> do not forget to link baids folder to ~/.baids and execute baids-reload)


## How-to

* Start the cluster

```
dev-mysql-ha-start
```

* Show cluster info

```
dev-mysql-ha-info
```
* Connect to mysql_server

```
dev-mysql-ha-client
```

* Another useful baids

```
dev-mysql-ha-shell
dev-mysql-ha-destroy
```

#### Snippets

```
mysql -h 172.31.0.10 -P 4006 -u maxscale -pmaxscalepass
```

```
docker run -it --net=infrastructure_backend --rm mysql sh -c "exec mysql -h mysqld -P 3306 -u root -p1234"
```


```
docker exec -i mysqld mysql -u root -p1234 <<< "create user 'maxscale'@'%' identified by 'maxscalepass';
                                                GRANT SELECT ON mysql.db TO 'maxscale'@'%'; GRANT SELECT ON mysql.db TO 'maxscale'@'%';
                                                GRANT SELECT ON mysql.tables_priv TO 'maxscale'@'%';
                                                grant REPLICATION SLAVE on *.* to 'maxscale'@'%';
                                                grant REPLICATION CLIENT on *.* to 'maxscale'@'%';
                                                grant ALL PRIVILEGES on *.* to 'maxscale'@'%';"
```

```
mysql -h 172.31.0.10 -P 4006 -u maxscale -pmaxscalepass
```

## TODO

* check how-to reload maxscale config in runtime (consul-template or similar)

https://mariadb.com/kb/en/mariadb-enterprise/mariadb-maxscale-21-readwritesplit/+comments/2824

## Resources

### Cluster

##### Official

https://hub.docker.com/r/mysql/mysql-cluster/

https://downloads.mysql.com/docs/mysql-cluster-excerpt-5.6-en.pdf

##### Related

https://hub.docker.com/r/labbsr0x/mysql-cluster-programs/

https://github.com/RafaMunoz/Cluster-MySQL-HAProxy

https://github.com/fordodone/getting_started_mysql_cluster

### Load balancer / Proxy

##### MaxScale

https://github.com/mariadb-corporation/MaxScale
https://mariadb.com/kb/en/mariadb-enterprise/maxscale-troubleshooting/

##### HAproxy

https://maauso.com/category/entrada/haproxy-con-consul-template/
https://engineeringblog.yelp.com/2015/04/true-zero-downtime-haproxy-reloads.html
