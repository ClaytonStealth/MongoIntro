# MongoIntro Queries
const eleven =	{
	 createdAt: new Date(),
	 title: "randomTitle",
	 text: "This is just some random text that will fit in this box to meet the requirements for the assignment...LOL",
	 author: "Thilanka Espinal",
	 lastModified: new Date(),
	 categories: ["rear-end", "backend", "frontend"],
	 id: "4a571289-6d5c-4300-9614-64g8f2137f91",
	 objectId: 11
	}
	db.posts.insertOne(eleven)


- find author 
    db.posts.find({
    author: {$regex: /Thilanka/}
})

- Greater than 5

db.posts.find({
    objectId: {$gt: 5}
})

-Greater than april 1 2022

db.posts.find({
    createdAt: {$gt: new Date("2022/04/01")}
})

part 2-------------------------

finding blogs where lastModified not existing

db.posts.find({
    lastModified: {$exists: false}
})

createdAt type = date

db.posts.find({
    createdAt: {$type: "date"}
})

combined two queries not exists and type date

db.posts.find({
    lastModified: {$exists: false},
    createdAt: {$type: "date"}
})
---------------- stretch--------------------
Stretch blog with specific phrase of vitae using regex

db.posts.find({
    text: {$regex: /vitae/}
})

Stretch blogs with qui in array

db.posts.find({
    categories: {$in: ["qui"]}
})


part 3 ------------------------------------------

finding if lastModified exists and adding it if it doesnt

db.posts.updateMany({
    lastModified: {
        $exists: false
    },{$set:{
        lastModified: new Date()
    }
}})

dates after may 2022, adding lorem to category array AND updating lastModified

db.posts.updateMany({
    createdAt: {$gt: new Date("May 2022")},
    {$addToSet: {categories: "lorem"},
        $set:{lastModified: new Date()}  
}})

finding voluptas $in categories array and $pulling it and updating lastModified time

db.posts.updateMany({
    categories: {$in: ["voluptas"]},
        {$pull: {categories: "voluptas"},
        $set: {lastModified: new Date()}
       }
    })

    looking for corrupti in Categories array and then deleting the blog that contains corrupti

    db.posts.deleteMany({
    categories: {$in: ["corrupti"]},
    })