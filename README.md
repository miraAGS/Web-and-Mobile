# Web and Mobile


## TasksApi 

TasksApi reflects a RESTful API, which is an interface that implements the contraints of the REST architectural style. It depicts the four (4) main HTTP methods, in manipulating JSON data, that are used for RESTful Services: 

* GET 

```python
@app.route('/todo/api/v1.0/tasks', methods=['GET'])
def get_tasks():
    return jsonify({'tasks': tasks})


@app.route('/todo/api/v1.0/tasks/<int:task_id>', methods=['GET'])
def get_task(task_id):
    task = [task for task in tasks if task['id'] == task_id]

    if len(task) == 0:
        abort(404)

    return jsonify({'task': tas
```
* PUT

```python
@app.route('/todo/api/v1.0/tasks/<int:task_id>/update', methods=['PUT'])
def update_task(task_id):
    task = [task for task in tasks if task['id'] == task_id]

    if len(task) == 0:
        abort(404)
    if not request.json:
        abort(400)
    
    task[0]['title'] = request.json.get('title', task[0]['title'])
    task[0]['description'] = request.json.get('description', task[0]['description'])
    task[0]['done'] = request.json.get('done', task[0]['done'])

    return jsonify({'task': task[0]})

```
* POST

```python
@app.route('/todo/api/v1.0/tasks/new', methods=['GET', 'POST'])
def create_task():
    form = TaskForm
    if form.validate_on_submit:
        task = Task(title=form.title.data, description=form.description.data)
        db.session.add(task)
        db.session.commit()

    task = {
        'id': task[-1]['id'] + 1,
        'title': request.json['title'],
        'description': request.json.get('description', ""),
        'done': False
    }
    tasks.append(task)
    return jsonify({'task': task}), 201
    
```

* DELETE

```python
app.route('/todo/api/v1.0/tasks/<int:task_id>/delete', methods=['DELETE'])
def delete_task(task_id):
    task = [task for task in tasks if task['id'] == task_id]

    if len(task) == 0:
        abort(404)

    tasks.remove(task[0])
    return jsonify({'result': True})
```

## My Flask Blog

### Main Features of the Flask Blog

Users are able to:

* Login into existing account

  ![Image of Login Screen](images/Login.png)
  
* Register for a new account

  ![Image of Register Screen](https://github.com/miraAGS/Web-and-Mobile/blob/main/images/Register.PNG)
  
* View existing posts 

  ![Image of Home](https://github.com/miraAGS/Web-and-Mobile/blob/main/images/Home.PNG)
  
* Create a new post 

  ![Image of New Post Screen](https://github.com/miraAGS/Web-and-Mobile/blob/main/images/newPost.PNG)
  
* View Profile Page of current user and other users
  
  The current user will also be able to follow other users pages
  
  ![Image of Profile Screen](https://github.com/miraAGS/Web-and-Mobile/blob/main/images/Profilepage.PNG)

  
* Update and Delete posts created

![Image of Login Screen](https://github.com/miraAGS/Web-and-Mobile/blob/main/images/Update_delete.PNG)

### Security 

#### Protecting Users' Passwords
In ensuring the protection of users' passwords, aside from the Werkzeug library which was used at first, Bcrypt was applied in examining different options for hashing passwords.

```python 
...
hashed_password = bcrypt.generate_password_hash(form.password.data).decode('utf-8')
...
```

#### Forget User Password

In the event that a user forgets the password for his profile, using Google's email server and Flask-Mail, the application was able to send and email with a link and a generated token bin order for the user to reset their password

```python

app.config['MAIL_SERVER'] = 'smtp.gmail.com'
app.config['MAIL_PORT'] = 587
app.config['MAIL_USE_TLS'] = True
app.config['MAIL_USERNAME'] = os.environ.get('EMAIL_USER')
app.config['MAIL_PASSWORD'] = os.environ.get('EMAIL_PASSWORD')
mail = Mail(app)
```

 ![Image of Reset Password1 Screen](https://github.com/miraAGS/Web-and-Mobile/blob/main/images/reset_passwordprompt.PNG)
 ![Image of Reset Password3 Screen](https://github.com/miraAGS/Web-and-Mobile/blob/main/images/resetpasswordSuccessful.PNG)
 ![Image of Reset password2 Screen](https://github.com/miraAGS/Web-and-Mobile/blob/main/images/ResetPassword.png)
 ![Image of Reset Password4 Screen](https://github.com/miraAGS/Web-and-Mobile/blob/main/images/changepassword.PNG)
 ![Image of Reset Password5 Screen](https://github.com/miraAGS/Web-and-Mobile/blob/main/images/changeSuccessful.PNG)


### Database 

In creating the database for the blog, Flask-SQLAlchemy, an extension from Flask was imported which supports SQLAlchemy. 

```python 

...
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///site.db'
db = SQLAlchemy(app)
...
```
