# gRPC-Service
dans ce projet, vous verrez comment créer un service API simple et un client qui récupère les prix en temps réel des crypto-monnaies
Utilisez les commandes suivantes pour installer les dépendances sur votre machine Linux :
#Créer un répertoire pour le projet:
mkdir crypto-service
cd crypto-service
#Créer un environnement virtuel
virtualenv crypto
source crypto/bin/activate 
pip3 install grpcio grpcio-tools
touch crypto_service.proto
#protocol buffer
syntax = "proto3";

// requetes des clients
message cryptocurrency{
   optional string name = 1;
}

// les reponses de API service
message market_price{
   optional float max_price = 1;
   optional float min_price = 2;
   optional float avg_price = 3;
}

// difinition du service de GExchange
service GExchange {

   // get_price method definition
   rpc get_price (cryptocurrency) returns (market_price) {};

}
#utiliser le compilateur de protocole pour compiler le fichier crypto_service.proto
python3 -m grpc_tools.protoc -I. --python_out=. --grpc_python_out=. crypto_service.proto
#cree le fichier python du serveur
touch crypto_server.py
