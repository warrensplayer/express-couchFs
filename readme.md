# express-couchFs

A express module that provides a simple file upload api using couchDb as file storage.

## Usage

``` js
var couchFs = require('express-couchdb-fs');

app.configure(function() {
  app.use(couchFs({couch: 'http://localhost:5984/fs'}));
});
```

### Alternate Configuration

If you would like to dynamically change which database is being used, then use 
the following configuration and set the request parameter given to the name of 
the database to use. The `database_parameter_name` is optional and will default 
to `"COUCH_DB"`. 

``` js
app.use(couchFs({url: 'http://localhost:5984/', database_parameter_name: 'COUCH_DB' }));
```

## API

### POST /api/file

The post statement can be a FORM Post or XHR2 post, the important aspect is that the body contains a file field named: `uploadFile`

On Success, this returns the couchdb generated document response:

```
{
  ok: true,
  id: xxxxx,
  rev: xxxx
}
```

### GET /api/file/:id

Grabs the file and downloads it to the client with a save as dialog.

### DELETE /api/file/:id