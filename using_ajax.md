https://www.youtube.com/watch?v=82hnvUYY6QA
> Fetching Text
```HTML
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Ajax 1 - Text File</title>
</head>
<body>
  <button id="button">Get Text File</button>
  <br><br>
  <div id="text"></div>

  <script>
    // Create event listener
    document.getElementById('button').addEventListener('click', loadText);

    function loadText(){
      // Create XHR Object
      var xhr = new XMLHttpRequest();
      // OPEN - type, url/file, async
      xhr.open('GET', 'sample2.txt', true);

      console.log('READYSTATE: ', xhr.readyState);

      // OPTIONAL - used for loaders
      xhr.onprogress = function(){
        console.log('READYSTATE: ', xhr.readyState);
      }

      xhr.onload = function(){
        console.log('READYSTATE: ', xhr.readyState);
        if(this.status == 200){
          //console.log(this.responseText);
          document.getElementById('text').innerHTML = this.responseText;
        } else if(this.status = 404){
          document.getElementById('text').innerHTML = 'Not Found';
        }
      }

      xhr.onerror = function(){
        console.log('Request Error...');
      }

      // xhr.onreadystatechange = function(){
      //   console.log('READYSTATE: ', xhr.readyState);
      //   if(this.readyState == 4 && this.status == 200){
      //     //console.log(this.responseText);
      //   }
      // }

      // Sends request
      xhr.send();
    }

    // readyState Values
    // 0: request not initialized 
    // 1: server connection established
    // 2: request received 
    // 3: processing request 
    // 4: request finished and response is ready

    // HTTP Statuses
    // 200: "OK"
    // 403: "Forbidden"
    // 404: "Not Found"
  </script>
</body>
</html>
```



> Fetching JSON

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Ajax 2 - Local JSON</title>
</head>
<body>
  <button id="button1">Get User</button>
  <button id="button2">Get Users</button>
  <br><br>
  <h1>User</h1>  
  <div id="user"></div>
  <h1>Users</h1>  
  <div id="users"></div>

  <script>
    document.getElementById('button1').addEventListener('click', loadUser);
    document.getElementById('button2').addEventListener('click', loadUsers);

    function loadUser(){
      var xhr = new XMLHttpRequest();
      xhr.open('GET', 'user.json', true);

      xhr.onload = function(){
        if(this.status == 200){
          var user = JSON.parse(this.responseText);
          
          var output = '';

          output += '<ul>' +
            '<li>ID: '+user.id+'</li>' +
            '<li>Name: '+user.name+'</li>' +
            '<li>Email: '+user.email+'</li>' +
            '</ul>';

          document.getElementById('user').innerHTML = output;
        }
      }

      xhr.send();
    }

    function loadUsers(){
      var xhr = new XMLHttpRequest();
      xhr.open('GET', 'users.json', true);

      xhr.onload = function(){
        if(this.status == 200){
          var users = JSON.parse(this.responseText);
          
          var output = '';
          
          for(var i in users){
            output += '<ul>' +
              '<li>ID: '+users[i].id+'</li>' +
              '<li>Name: '+users[i].name+'</li>' +
              '<li>Email: '+users[i].email+'</li>' +
              '</ul>';
          }

          document.getElementById('users').innerHTML = output;
        }
      }

      xhr.send();
    }
  </script>
</body>
</html>
```

> Fetching from external server(git api)
```HTML
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Ajax 3 - External API</title>
  <style>
    .user{
      display: flex;
      background:#f4f4f4;
      padding:10px;
      margin-bottom:10px;
    }

    .user ul{
      list-style: none;
    }
  </style>
</head>
<body>
  <button id="button">Load GitHub Users</button>
  <br><br>
  <h1>Github Users</h1>
  <div id="users"></div>

  <script>
    document.getElementById('button').addEventListener('click', loadUsers);

    // Load Github Users
    function loadUsers(){
      var xhr = new XMLHttpRequest();
      xhr.open('GET', 'https://api.github.com/users', true);

      xhr.onload = function(){
        if(this.status == 200){
          var users = JSON.parse(this.responseText);

          var output = '';
          for(var i in users){
            output +=
              '<div class="user">' +
              '<img src="'+users[i].avatar_url+'" width="70" height="70">' +
              '<ul>' +
              '<li>ID: '+users[i].id+'</li>' +
              '<li>Login: '+users[i].login+'</li>' +
              '</ul>' +
              '</div>';
          }

          document.getElementById('users').innerHTML = output;
        }
      }

      xhr.send();
    }
  </script>
</body>
</html>
```
