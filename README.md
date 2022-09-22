const getPosts = (searchObject, sortObject, limit, skip) => {
    const posts = db.blogs.find(searchObject).toArray()
    return posts
}

const searchObject = {
    createdAt: {$gt: ISODate('2022-05-01')}
}

const sortObject = {}
const limit = 10
const skip = 0

// Uncomment the following line when you're ready to run getPosts

const posts = getPosts(searchObject, sortObject, limit, skip)



# Create Posts

const createPost = (newPost) => {
    const id = getUUID()
    if (!newPost.title){
        console.log('title is a required field')
        return
    }
    if (!newPost.text){
        console.log('text is a required field')
        return
    }
    if (!newPost.author){
        console.log('author is a required field')
        return
    }
    if (!newPost.categories){
        console.log('categories is a required field')
        return
    }
    const postData = {
        id: id,
        createdAt: new Date(),
        title: newPost.title,
        text: newPost.text,
        author: newPost.author,
        categories: newPost.categories,
        lastModified: new Date()
    }
    db.blogs.insertOne(postData)
    return 
}

const newPost = {
    title: "The Dark Knight Movie Review",
    text: "This movie was amazing because I am Batman.",
    author: "Bruce Wayne",
    categories: ["superhero", "action", "thriller"]
}

// Uncomment the following line when you're ready to run createPosts

createPost(newPost)


# update 

const updatePost = (postId, createdAt, newPostData) => {
    db.blogs.updateOne({
        id: postId
    },{$set:{
        id : postId,
        createdAt: createdAt,
        title: newPostData.title,
        text: newPostData.text,
        author: newPostData.author,
        categories: newPostData.categories,
        lastModified: new Date()
    }})

}

const updatedPost = {
    title: "The Dark Knight Movie Review",
    text: "This movie was amazing because I am Batman, and totally not Bruce Wayne. I don't even know who that is.",
    author: "Batman",
    categories: ["superhero", "action", "thriller"]
}

let found = db.blogs.find({
    title : updatedPost.title
}).toArray()
const postId = found[0].id
const createdAt = found[0].createdAt


// Uncomment the following line when you're ready to run updatePost
updatePost(postId, createdAt, updatedPost)


# Delete

const deletePost = (id) => {
    db.blogs.deleteOne({id: id})
    return
}

const postIdToDelete = "23d3563e-a211-4759-a77e-6de55d1e03ac"


// Uncomment the following line when you're ready to run deletePost
deletePost(postIdToDelete)
