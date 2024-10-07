# seasonal_Practicse-
Now it's time to rock!!!



const express = require('express')
const app=express();
const user= [{
    name:"keshav",
    kidney: [{
        healthy: false
    }]

}];

app.use(express.json())
app.get("/", function(req,res){
    const johnkidney =user[0].kidney;
    const numofkidney =johnkidney.length;
    let numofhealthy =0;
    for(let i=0;i<johnkidney.length;i++){
        if(johnkidney[i].healthy){
            numofhealthy=numofhealthy+1;
        }

    }
   
    const numofunhealthy = numofkidney - numofhealthy;

    res.json({
        numofkidney,
        numofhealthy,
        numofunhealthy
    })
})

app.post("/",function(req,res){
const ishealthy = req.body.ishealthy;
user[0].kidney.push({
    healthy: ishealthy
})

res.json({
    msg:"Done"
});

})

app.put("/",function(req,res){
    for(let i=0;i<user[0].kidney.length;i++){
            user[0].kidney[i].healthy=true;
        }
            res.json({});
})

app.delete("/",function(req,res){
// 
//removing all unhealthy kidney

if(isThereAtleastOneUnhealthyKidney())
 {
    const newkidney =[];
    for(let i=0;i<user[0].kidney.length;i++){
       if(user[0].kidney[i].healthy){
           newkidney.push({
               healthy: true
           })
       }
    }
   user[0].kidney=newkidney;
   
   res.json({
       msg:"done!"
   });
 }
 else{
    res.status(411).json({
        msg: "you have no kidneys"
    })
 }
  

})
function isThereAtleastOneUnhealthyKidney(){
    let atleastOnehealthyKidney= false;
    for (let i = 0; i < user[0].kidney.length; i++) {
        if(!user[0].kidney[i].healthy){
          atleastOnehealthyKidney=true;
        }
        
    }
    return atleastOnehealthyKidney;
}

app.listen(3000);
