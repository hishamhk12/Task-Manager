## first we create our app.js and package.json

## secound we create our router folder in file task.js
### to able to navigate our url link
```js
const express = require('express');
const router = express.Router();
const {getAlltaks, createtaks, gettaks, updatetaks, deletetaks} = require('../controllers/tasks')

router.route('/').get(getAlltaks).post(createtaks)

router.route('/:id').get(gettaks).patch(updatetaks).delete(deletetaks)

module.exports = router;
```

## third we connect our app to the router

```js
const taks = require('./routes/task')
app.use('/api/v1/taks',taks)
```

## fourth  we setup our controllers

```js
const Task = require('../moodel/task')

const getAlltaks = (req,res)=>{
    res.send('all items')
}

const createtaks = async(req,res)=>{
    const task = await Task.create(req.body);
    res.status(201).json({task})

}

const gettaks =(req,res)=>{
    res.json({id:req.params.id})
}

const updatetaks =(req,res)=>{
    res.send('all 3items')
}

const deletetaks =(req,res)=>{
    res.send('all4 items')
}
```
## fifth we create our database and connect to the app

```js
 const mongoose = require('mongoose');
 
 const mydb =
  'mongodb+srv://hishamhk12:mlSKT99eYIKqgr73@cluster0.knstigg.mongodb.net/shop?retryWrites=true&w=majority'

  const connectDB = (url)=>{
    return mongoose.
    connect(mydb,{ useNewUrlParser: true , useUnifiedTopology: true})
    .then(()=>{console.log('connet')})
    .catch((err)=>{console.log(err)})
  }
  module.exports = connectDB;
 // app.js file

 const  connectDB = require('./db/connect')
const port = 3000;

const star = async()=>{
    try {
             await connectDB();
             app.listen(port, console.log(port));
    }catch (error){
           console.log(error)
    }
}
star()
```
## sixth we create model file task.js
### schema make the shape of our document
### schema give our document the structer we want
```js
const  mongoose  = require("mongoose");
const taskSchema = new mongoose.Schema({
  name: String,
  complated:Boolean
})
module.exports = mongoose.model('Task',taskSchema)
```