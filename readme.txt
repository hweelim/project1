1) fetch cdr data from production server
sh exportCdrdata.sh <start epoch time> <end epoch time> <directory>
ie. sh exportCdrdata.sh 1454313600000 1454399940000 20160201
* data files will be created under data/20160201


2) import cdr data to elastic search
sh importCdrdata.sh <directory>
ie. sh importCdrdata.sh 20160201
* data will be prepared in data/20160201/output
* screen display number of document count imported to elastic search
* check logs to see if there is any error

3) check if cdr data is imported
curl 'http://192.84.19.61:9200/_cat/indices?v'
* successful import display something as follows:
green  open   sfcdr-20160201    5   1  12164  0  9.5mb 4.7mb

* uncessful import shows 0 or small number in 6th column
green  open   sfcdr-20160203    5   1   0   0   970b  575b 

OR

check elastic search individual indices:
curl 'http://192.84.19.61:9200/sfcdr-20160201/'

