# redis-geo-ip
Redis geoip load all maxmind geoip values into redis. 
To load the data place the file in the maxmind directory or change the path

First ask your decimal IP

zrangebyscore  ip [IP] +inf limit 0 1

then use the result to get the country

zrevrangebyscore  country [RESULT] 0  withscores limit 0 1

if you find this software useful please let me know
