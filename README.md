# ELK-on-RHEL

Hosting ELK stack on RHEL server

# Getting ElasticSearch up and running

1) Create a folder ELK where you intend to keep the ELK Stack(make sure sufficient space is there to download ELK, 
  you can use df -h to check the file partition)
 
        mkdir ELK
    
        cd ELK

2) Download and unzip Elastic Search from official site https://www.elastic.co/downloads/elasticsearch

        sudo wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-6.6.1.tar.gz
    
        tar -zxvf elasticsearch-6.6.1.tar.gz

3) Changing config file to get the elasticsearch reachable to the outside world than server

        cd elasticsearch/config and change the below entry in elasticsearch.yml

        #network.host: 192.168.0.1 to network.host : 0.0.0.0

    0.0.0.0 : Anyone from outside the server can access this

4) Change the permissions

    Change the ownership of elasticsearch folder to the current user and the usergroup

        whoami : to get the username
        groups username : To get the user group

        sudo chown -R currentUsername:Usergroup elasticsearchFolder

5) Start elasticsearch

          bin/elasticsearch
 
    In the same machine :

        Point your browser to http://localhost:9200 
        
            or 
        
        curl http://localhost:9200/ in command line, you should get a similar response.

          {
          "name" : "8OZ-zhg",

          "cluster_name" : "elasticsearch",

          "cluster_uuid" : "WyBWEwfMRDC7uf49Gy9MMA",

          "version" : {

          "number" : "6.1.0",

           "build_hash" : "c0c1ba0",

          "build_date" : "2017-12-12T12:32:54.550Z",

          "build_snapshot" : false,

           "lucene_version" : "7.1.0",

           "minimum_wire_compatibility_version" : "5.6.0",

          "minimum_index_compatibility_version" : "5.0.0"

          },

          "tagline" : "You Know, for Search"

           }

    Outside the server

     Get the ip of the server using ifconfig 

           http://<IP of the server where elastic Search is running>:9200
           
           You should a similar response as above

Now ElasticSearch is running on port 9200.



# Getting Kibana up and running.

1.  Download and unzip kibana from official site https://www.elastic.co/downloads/kibana .

2.  Open config/kibana.yml in editor and set elasticsearch.url to point to your Elastic search instance.

    #to do the above uncomment the line in kibana.yml;

        elasticsearch.url: http://localhost:9200 (If your elasticsearch is running in the same machine) 
        
        elasticsearch.url: http://<IP of the server where elastic Search is running>:9200 (If your elasticsearch is running in the different machine) 

3.  Changing config file to get the Kibana reachable to the outside world than server
    
          cd kibana/config and Open config/kibana.yml in editor, uncomment and change
    
           #server.host: 0.0.0.0 to server.host: 0.0.0.0

4. Change the permissions

    Change the ownership of kibana folder to the current user and the usergroup

        whoami : to get the username
      
        groups username : To get the user group

        sudo chown -R currentUsername:Usergroup kibanafolder
    
5.  Start kibana
  
          bin/kibana 

6.  Point your browser to     
    
      On the same machine : 
      
          http://localhost:5601  .You should see Kibana Welcome page UI.
    
      Outside the server  :
      
      Get the ip of the server where kibana is running using ifconfig
      
          http://<IP of the server where kibana is running>:5601   

Now Kibana is running on port 5601.







