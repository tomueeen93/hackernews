# Example for GraphQL with golang

See the following site

https://www.howtographql.com/graphql-go/0-introduction/

### How to check it

Clone

```console
% go version
go version go1.17.6 darwin/amd64
% git clone git@github.com:tomueeen93/hackernews.git
```

Setup Database

```console
% docker run -p 3306:3306 --name mysql -e MYSQL_ROOT_PASSWORD=dbpass -e MYSQL_DATABASE=hackernews -d mysql:latest
% docker exec -it mysql mysql -u root -pdbpass
mysql> CREATE DATABASE hackernews;
mysql> exit;
```

Create tables
```
% go get -u github.com/go-sql-driver/mysql
% go build -tags 'mysql' -ldflags="-X main.Version=1.0.0" -o $GOPATH/bin/migrate github.com/golang-migrate/migrate/v4/cmd/migrate/
% cd internal/pkg/db/migrations/
% migrate create -ext sql -dir mysql -seq create_users_table
% migrate create -ext sql -dir mysql -seq create_links_table
```

Run application
```
% cd hackernews
% go mod tidy
% go run server.go
```
