## MongoDb schema types
[MongoDb schema types](http://mongoosejs.com/docs/2.7.x/docs/schematypes.html)

## Workflow using mongoose
```JavaScript
var mongoose = require('mongoose');
	conn_str = 'mongodb://localhost:27017/test',
	mongoose.Promise = require('q').Promise;
  
mongoose.connect(conn_str);

var db = mongoose.connection;
// new schema
var emp_schema = mongoose.Schema({
	name: String,  
	id: Number,  
  active: Boolean,  
  date: Date,  
  meta: {
  },
  comments: [Comments] // Comments is pre-defined schema
});
// new model, model is treated as table in mongodb
var emp_model = mongoose.model(emp_schema);

db.on("error", function() {

})

db.on("open"m function() {
	// new record based on module and off course schema. then save record

	emp_model({

	}).save();
})

// fetch data
emp_model.find({"name"})
```

## High level of using shema
[High level of using shema](http://mongoosejs.com/docs/2.7.x/docs/embedded-documents.html)
