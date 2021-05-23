# Minimal SQLite3 Container with pcre Plugin

sqlite3-pcre is a minimal Alpine container with SQLite3 and sqlite3-pcre plugin installed

## Build Instruction
```bash
docker image build --tag wstein/sqlite3-pcre $PWD
```

## Usage Example

this example uses the chinook.db sample database from https://www.sqlitetutorial.net/sqlite-sample-database

```bash
docker container run -it --rm -v sqlite3_data:/data --entrypoint /bin/ash wstein/sqlite3-pcre -c "wget https://www.sqlitetutorial.net/wp-content/uploads/2018/03/chinook.zip && unzip chinook.zip"

# entering interactive mode using box output mode:
docker container run -it --rm -v sqlite3_data:/data wstein/sqlite3-pcre -box chinook.db

# view all tables available in the sample database:
docker container run -it --rm -v sqlite3_data:/data wstein/sqlite3-pcre chinook.db ".tables"

# show album titles and their artist names using csv output mode with header:
docker container run -it --rm -v sqlite3_data:/data wstein/sqlite3-pcre -csv -header chinook.db "
    SELECT Title, Name
    FROM albums
    INNER JOIN artists ON artists.ArtistId = albums.ArtistId;
" | sed -e "/^--/d"
```
