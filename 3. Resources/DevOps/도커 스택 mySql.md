```yml
version: "3"
services:
  db:
    image: mysql:8.0
    deploy:
      replicas: 1
    restart: always
    ports:
      - "3306:3306"
    environment:
      MYSQL_ROOT_PASSWORD: password1234
      MYSQL_DATABASE: bibum_db
      TZ: Asia/Seoul
    command:
       - --character-set-server=utf8mb4
       - --collation-server=utf8mb4_unicode_ci
    volumes:
      - db_data:/var/lib/mysql
    networks:
      - dbnetwork

networks:
  dbnetwork:
    driver: overlay

volumes:
  db_data:
```

```bash
docker stack deploy -c db-compose.yml mysql-db
```
