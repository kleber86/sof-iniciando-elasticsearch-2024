# Instalar ElasticSearch usando Docker

Criar uma rede elastic:
```
docker network create elastic
```

Baixar a imagem do container do ElasticSearch:
```
docker pull docker.elastic.co/elasticsearch/elasticsearch:8.13.0
```

Criar o container do ElasticSearch:
```
docker run --name es01 --net elastic -p 9200:9200 -it -m 1GB docker.elastic.co/elasticsearch/elasticsearch:8.13.0
```

Nos logs da execução acima irá aparecer algumas informações importantes, como usuário e senha do Elasticsearch e o token que será necessário para a próxima etapa.
```
✅ Elasticsearch security features have been automatically configured!
✅ Authentication is enabled and cluster connections are encrypted.

ℹ️  Password for the elastic user (reset with `bin/elasticsearch-reset-password -u elastic`):
  laxxWJLuxG1dcR-0cr2R

ℹ️  HTTP CA certificate SHA-256 fingerprint:
  6649ac3a3660699df302da30e4f51bb96546e73d625c54660ead11a6e81671

ℹ️  Configure Kibana to use this cluster:
• Run Kibana and click the configuration link in the terminal when Kibana starts.
• Copy the following enrollment token and paste it into Kibana in your browser (valid for the next 30 minutes):
  eyJ2ZXIiOiIgdfgdf53CJhZHIiOlgfdgdfgsiMTcyLjE4LjAuMjo5MjAwIl0sImZnciI6IjY2NDlhYzNhMTAxZjA2OTlkZjMwgdgdfgdMmRhMzBlNGY1MWJiOTg5YTJlNzNkNjI1Y2RiYmY2MGVhZDzEiLCJrZXkiOiJScmtzZlk0QjZBY29JNkxiUUVYdTpOZjRZeUxyZ1JXYUsxSWxoV3pDaVRRIn0=
```

# Instalar o Kibana usando Docker

Baixar a imagem do container:
```
docker pull docker.elastic.co/kibana/kibana:8.13.0
```

Criar o container do Kibana:
```
docker run --name kib01 --net elastic -p 5601:5601 docker.elastic.co/kibana/kibana:8.13.0
```

Quando finalizar os logs mostrará um endereço web com um codigo é só acessar: 
```
Go to http://0.0.0.0:5601/?code=328193 to get started.
ou
Go to http://localhost:5601/?code=328193 to get started.
```

Ao acessar a página no campo Enrollment token, coloque o token gerado na etapa da instalação do ElasticSearch.

Depois da configuração é só logar com o usuário `elastic` e senha que foi gerada durante a primeira inicialização do ElasticSearch.

Obs: É possivel que durante a configuração ou após o container do ElasticSearch seja encerrado, é só iniciar novamente e continuar a configuração ou a inicialização.

