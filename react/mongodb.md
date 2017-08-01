MongoDb
=======

Mongoose
========
create document
---------------
create() function used to insert one document to db

Model.create(document, function(err, documents) {
	
})



update document
---------------
Model.update() function will only return status instead of updated document
if you want to return updated document use findOneAndUpdate()
```
app.put('/books/:_id', function(req, res) {
  var book = req.body;
  var query = req.params._id;

  var update = {
    '$set': {
      title: book.title,
        description: book.description,
        images: book.images,
        price: book.price
    }
  };
  // when true return updated record other than original one
  var options = {new: true}; 

  Books.findOneAndUpdate(query, update, options, function(err, book) {
    if (err) {
      throw err;
    }
    res.json(book);
  })
})
```
