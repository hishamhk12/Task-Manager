## we want to get one task from our database collection
### we set up our route router.route('/:id').get(getTaks)
```js
const Task = require('../moodel/task')

const getTaks =async(req,res)=>{
    try {                     //we take the id from                               
           const {id:taskID} = req.params // url  http://localhost:3000/api/v1/taks/6493f0be005045171ce438e8
                            //Task is our database name
           const task = await Task.findOne({_id:taskID}); // we will use finOne methods to look for 
           //  6493f0be005045171ce438e8 this id from our database
           if(!task){ // if we did not found our id 
            return res.status(404).json({msg:`No task with id ${taskID}`})
           }
    res.status(200).json({task}) // if we found or id we will show it as json file
} catch (err){
    res.status(500).json({msg:err})}}
```