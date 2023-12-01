# Remove All
sudo docker rm -vf $(sudo docker ps -a -q)
sudo docker rmi -f $(sudo docker images -a -q)
sudo docker system prune -f
sudo docker volume prune -f


# Remove # Remove volumens and images
docker-compose -f production.yml down --volumes --rmi all


version: "3.8"

services:
  app:
    image: platziapp
    environment:
      MONGO_URL: "mongodb://db:27017/test"
    depends_on:
      - db
    ports:
      - "3000-3001:3000"
    deploy:
      resources:
        limits:
          memory: 20m
  db:
    image: mongo
    deploy:
      resources:
        limits:
          memory: 70m
