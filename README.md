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
    author: {
        $regex: /Thilanka/
    }
})

- Greater than 5

db.posts.find({
    objectId: {
        $gt: 5
    }
})

-Greater than april 1 2022

db.posts.find({
    createdAt: {
        $gt: new Date("2022/04/01")
    }
})

part 2-------------------------

finding blogs where lastModified not existing

db.posts.find({
    lastModified: {
        $exists: false
    }
})

createdAt type = date

db.posts.find({
    createdAt: {
        $type: "date"
    }
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