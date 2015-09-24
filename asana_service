/**
 * New node file
 */
// Express is required for creating Node.js based web apps
var express = require('express');

// body-parser is used to parse the Request body and populate the req.
var bodyParser = require('body-parser');

// mongoose is used for interacting with MongoDB
var mongoose = require('mongoose');

var app = express();
//app.set('port', 3300);

// Configuring Express App to make use of BodyParser's JSON parser to parse
// JSON request body
app.use(bodyParser.json());

var dbHost = 'mongodb://admin:w_aXU4nSt_6v@localhost:27017/asana';
mongoose.connect(dbHost);
// Create a schema for Book
var userSchema = mongoose.Schema({
  name: String,
  id : Number,
  email:String,
  photo:String,
  workspaces :String ,
  access_token : String,
  refresh_token : String,
  updated_at : String
	});
//  
//
//  
// //Also creating index on field isbn
// isbn: {type: String, index: true},
// author: String,
// pages: Number


// Create a Model by using the schema defined above
// Optionally one can provide the name of collection where the instances
// of this model get stored. In this case it is "mongoose_demo". Skipping
// this value defaults the name of the collection to plural of model name i.e
// books.
var User = mongoose.model('user', userSchema);

// Connecting to Mongod instance.
mongoose.connection;

// Starting up the server on the port: 3300
app.listen(80, function(){
  console.log("Server up: http://localhost");
});


// Get all the users
app.get('/user', function(req, res){
  // Find all the books in the system.
  User.find({}, function(err, result){
    if ( err ) throw err;
    // Save the result into the response object.
    res.json(result);
  });
 
});


// Get the details of the book with the given isbn
app.get('/user/:id', function(req, res){
  console.log("Fetching details for user with id: " + req.params.id);
  // The parameter in the route is accessed via request.params object.
  User.findOne({id: req.params.id}, function(err, result){
    if ( err ) throw err;
    res.json(result);
  });
});

// Add a new user
app.post("/user", function(req, res){
  console.log("Adding new user: " + req.body.name);
  var users = new User({
    name:req.body.name,
    id: req.body.id,
    email:req.body.email,
    photo:req.body.photo,
    workspaces :req.body.workspaces ,
    access_token : req.body.access_token,
    refresh_token : req.body.refresh_token,
    updated_at :  new Date().toISOString()
    
  });
  
  User.findOne({id: users.id}, function(err, result){
	    if ( err ) throw err;

	    if(!result){
	    	 console.log("no  users: save ");
	    	// res.json({
	     // message:"Book with ISBN: " + req.params.isbn+" not found.",
	      
	     // });
	    	 users.save(function(err, users){
	    		    if ( err ) console.log(err);
	    		    // After successfully saving the book we generate a JSON
	    			// response with the
	    		    // message and the inserted book information.
	    		    res.json({
	    		      message:"Successfully added user",
	    		      issuccess :true,
	    		      user:users
	    		    });
	    		  });
	    }else
	    	{

	    	console.log("  users: update ");
	    	result.name = users.name ;
	    	result.email=users.email;
	    	result.photo=users.photo;
	    	result.workspaces =users.workspaces ;
	    	result.access_token = users.access_token;
	    	result.refresh_token = users.refresh_token;
	    	result.updated_at = users.updated_at;
	   
	    result.save(function(err, result){
	      if ( err ) throw err;
	      res.json({
	        message:"Successfully updated the user",
	        issuccess : true,
	        user: result
	      });
	    });

	    	}
	  });
  // Saving the model instance to the DB  	
});



//Delete an existing book
app.get("/userdel/:id", function(req, res){
  User.findOneAndRemove({id: req.params.id}, function(err, result){
      res.json({
        message: "Successfully deleted  user",
        user: result
      });
  });
});
