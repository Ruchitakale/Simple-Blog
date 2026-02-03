<!DOCTYPE html>
<html>
<head>
    <title>Simple Blog</title>
    <style>
        body {
            font-family: Arial;
            background: #f4f4f4;
            padding: 20px;
        }

        h1 {
            text-align: center;
        }

        .container {
            max-width: 600px;
            margin: auto;
            background: skyblue;
            padding: 20px;
            border-radius: 8px;
        }

        input, textarea {
            width: 90%;
            padding: 10px;
            margin: 5px 0;
        }

        button {
            padding: 10px;
            margin-top: 5px;
            cursor: pointer;
        }

        .post {
            background: #eee;
            padding: 10px;
            margin-top: 10px;
            border-radius: 5px;
        }

        .post button {
            margin-right: 5px;
        }
    </style>
</head>

<body>

<h1>Simple Blog</h1>

<div class="container">

    <input type="text" id="title" placeholder="Post Title">
    <textarea id="content" placeholder="Write content..."></textarea>
    <button onclick="addPost()">Add Post</button>

    <h2>All Posts</h2>
    <div id="posts"></div>

</div>

<script>
    let posts = [];
    let editIndex = -1;

    function addPost() {
        let title = document.getElementById("title").value;
        let content = document.getElementById("content").value;

        if (title === "" || content === "") {
            alert("Please fill both fields");
            return;
        }

        if (editIndex === -1) {
            posts.push({title, content});
        } else {
            posts[editIndex] = {title, content};
            editIndex = -1;
        }

        document.getElementById("title").value = "";
        document.getElementById("content").value = "";

        showPosts();
    }

    function showPosts() {
        let output = "";

        posts.forEach((post, index) => {
            output += `
                <div class="post">
                    <h3>${post.title}</h3>
                    <p>${post.content}</p>
                    <button onclick="editPost(${index})">Edit</button>
                    <button onclick="deletePost(${index})">Delete</button>
                </div>
            `;
        });

        document.getElementById("posts").innerHTML = output;
    }

    function deletePost(index) {
        posts.splice(index, 1);
        showPosts();
    }

    function editPost(index) {
        document.getElementById("title").value = posts[index].title;
        document.getElementById("content").value = posts[index].content;
        editIndex = index;
    }
</script>

</body>
</html>
