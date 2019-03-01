     # getting docker working
     sudo apt install docker.io
     sudo apt install docker-compose
     sudo usermod -a -G docker ubuntu
     # needed to add the extra private ip addr
     ip addr add 172.30.0.187/24 dev eth0  

     # installing acmetool https://github.com/hlandau/acme
     # and creating certs
     sudo apt-get install acmetool
     sudo acmetool quickstart
     sudo acmetool want fullcert.tinisles.com
     sudo acmetool want nochain.tinisles.com

     # docker command that launches everything
     docker container run -it --rm -v $(pwd)/data/conf.d:/etc/nginx/conf.d -v $(pwd)/certs:/certs -v $(pwd)/html:/html --network=host nginx:1.15-alpine
