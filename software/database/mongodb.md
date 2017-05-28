pymongo tutorial :
	https://docs.mongodb.com/getting-started/python/query/	
	http://api.mongodb.org/python/current/tutorial.html
	

备份数据库：
	mongodump -d teachers

mkdri -p ~/db
apt-get install mongodb

python驱动
	sudo easy_install pymongo


例子：
frank@G470:~$ mongo
MongoDB shell version: 2.4.9
connecting to: test
> show dbs
local	0.078125GB
teacher_db	0.203125GB
test	0.203125GB
> use teacher_db
switched to db teacher_db
> show collections
sdust_teachers
system.indexes
> db.sdust_teachers.findOne()
{
	"_id" : ObjectId("572ca8d34089a4166879c7b7"),
	"网页信息" : {
		"description" : "山东科技大学 山东科技大学",
		"title" : "山东科技大学",
		"url" : "http://www.sdust.edu.cn/index__8B60D2DD6EB07375973DBB2BAE30BA3D.htm",
		"html" : "body",
		"time" : "Fri, 06 May 2016 15:21:49 GMT",
		"parent_url" : "parent_url"
	}
}
> 


$ mongo
>show dbs 显示所有数据库
>help
>db      显示正在使用的数据库
>use test		选择'test'数据库
>post = { "_id" : ObjectId("566688e6d49d9d45a435c994"), "title" : "my blog post", "content" : "here is my blog post." }
>db.blog.insert(post)　　定义文档
>db.blog.find()			显示'db'中'blog'集合的所有文档
>db.blog.findOne()　　　
>post.comments=[]		
>db.blog.update({title: "my blog post"}, post)
>db.blog.remove({title: "my blog post"}, post)

> db.sdust_teachers.drop()
true
> db.sdust_teachers.find()

null
true false
3.14 3
"x"
new Date()
["a", "b", "c"]
ObjectId()

$mongo some-host:30000/myDB
$mongo --nodb
>conn = new Mongo("some-host:30000")
>db = conn.getDB("myDB")

>help
>db.foo.batchInsert([{"_id" : 0}, {"_id" : 1}, {"_id" : 2}])
>db.foo.remove()
>db.foo.remove("opt-out" : true)
>db.foo.drop()

>var joe = db.users.findOne({"name" : "joe"})
>joe.relationships = { "friends" : joe.friends, "enemies" : joe.enemies};
>joe.username = joe.name;
>delete joe.friends;
>delete joe.enemies;
>delete joe.name;
>db.users.update({"name" : "joe"}, joe)

>db.people.update({"_id" : ObjectId("123456")}, joe)

修改器
>db.foo.update({"url" : "www.f.com"},
	{"$inc" : {"pageviews" : 1}})
>db.foo.update({"_id" : ObjectId()},
	{"$set" : {"favorite book" : "war and peace"}})
>db.foo.update({},
	{"$unset" : {"favorite book" : 1}})
>db.blog.posts.update({"author.name" : "joe"},
	{"$set" : {"author.name" : "joe schmoe"}})
>db.foo.update({},
	{"$push" : {"comments":
		{"name : "joe", "email" : "joe@x.com", "content" : "..."}}})
>db.stock.ticker.update({},
	{"$push" : {"hourly" : {"$each" : [1, 2, 3]}}})
>db.stock.ticker.find({},
	{"$push" : {"hourly" : 
		{"$each" : [1, 2, 3], "$slice" : -10}}})
>db.foo.find({},
	{"$push" : {"top10" : {
		"$each" : [{"name" : ""}, {"name" : }],
		"$slice" : -10,
		"$sort" : {"rating" : -1}}}})
>db.foo.update({"author cited" : {"$ne" : "Richie"}},
	{"$push" : {"author cited" : "Richie"}})
>db.foo.update({},
	{"$addToSet" : {"email" : "joe@gmail.com"}})
>db.foo.update({},
	{"$addToSet" : {"email" : {
			"$each" : ["joe@php.net", "joe@python.org"]}}})
删除数组元素
>db.lists.update({}, {"$pull" : {"todo" : "laundry"} })
也可以用{"$pop" : {"key" : 1}} {"$pop" : {"key" : -1}}

>db.blog.update({},
	{"$inc" : {"comments.0.votes" : 1}})
>db.blog.update({"comments.author" : "John"},
	{"$set" : {"comments.$.author" : "Jim"}})
>db.foo.upsert({"url" : "/blog"},{"$inc": {"pageviews" : 1}}, true)
>db.foo.update({},
	{"$setOnInsert" : {"createdAt" : new Date()}},true)
>db.foo.update({},
	{"$set" : {"gift" : "Happy Birthday!"}},false, true)
>db.runCommand({getLastError : 1})
>ps = db.runCommand({"findAndModify" : "process",
	"query" : {"status" : READY},
	"sort" : {"priority" : -1},
	"update" : {"$set" : {"status" : "RUNNING"}}})
查询
>db.foo.find()
>db.users.find({"username" : "joe", "age" : 27})
>db.users.find({}, {"username" : 1, "age" : 1})
>db.users.find({}, {"username" : 1, "fatal_weakness" : 0})
>db.foo.find({"age" : {"$gte" : 18, "$lte" : 30}})
>start = new Date("01/01/2007")
>db.foo.find({"registered" : {"$lt" : start}})
>db.user.find({"username" : {"$ne" : "joe"}})
>db.foo.find({"ticket_no" : {"$in" : [1, 2, 3]}}
>db.foo.find({"ticket_no" : {"$nin" : [1, 2, 3]}}
>db.foo.find({"$or" : [{"ticket_no" : 75}, {"winner" : true}]}
>db.foo.find({"id_num" : {"$mod" : [5, 1]}})
>db.foo.find({"id_num" : {"not" : {"$mod" : [5, 1]}}})
>db.foo.find({"z" : {"$in" : [null], "$exists" : true}})
>db.users.find({"name" : /joe/i});
>db.users.find({"name" : /joey?/i})//pcre
>db.food.find({fruit : {$all : ["apple", "banana"]}})
>db.food.find({"fruit.2" : "peach"})
>db.food.find({"fruit" : {"$size" : 3}})
>db.blog.posts.findOne(criteria, {"comments" : {"$slice" : 10}})
>db.people.find({"name.first“ : "joe", "name.last" : "schmoe"})
>db.blog.find({"comments" : {
	"$elemMatch" : {"author" : "joe", "score" : {"$gte" : 5}}})
>for(i=0; i<100; i++) {
	db.collection.insert({x : i});
}
> var cursor = db.collection.find();
>while(cursor.hasNext()){
	obj = cursor.next();
	//do stuff
}
>cursor.forEach(function(x) {
	print(x.name)
});
>var cursor = db.foo.find().sort({"x" : 1}).limit(1).skip(10);
>cursor.hasNext();
>db.c.find().limit(3)
>db.c.find().skip(3)
>db.c.find().sort({username : 1, age : -1})




