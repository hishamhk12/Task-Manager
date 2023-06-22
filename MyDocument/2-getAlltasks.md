## we create function take all the task from dyabase

```js
const getAlltaks = async(req,res)=>{
    try{
        const task = await Task.find({})
        res.status(200).json({task})
    } catch (err){
        res.status(500).json({msg:err})
    }
}
```
## The const task = await Task.find({}) line retrieves all tasks from the database using the Task.find() method. The Task.find() method takes an empty query document as an argument and returns all tasks in the collection.