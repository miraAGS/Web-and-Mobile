# Web and Mobile


## TasksApi 

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

In the event that a user forgets the password for his profile, they are able to reset their password by a link with a generated token being sent to their email. 

 ![Image of Reset Password1 Screen](https://github.com/miraAGS/Web-and-Mobile/blob/main/images/reset_passwordprompt.PNG)
 ![Image of Reset Password3 Screen](https://github.com/miraAGS/Web-and-Mobile/blob/main/images/resetpasswordSuccessful.PNG)
 ![Image of Reset password2 Screen](https://github.com/miraAGS/Web-and-Mobile/blob/main/images/ResetPassword.png)
 ![Image of Reset Password4 Screen](https://github.com/miraAGS/Web-and-Mobile/blob/main/images/changepassword.PNG)
 ![Image of Reset Password5 Screen](https://github.com/miraAGS/Web-and-Mobile/blob/main/images/changeSuccessful.PNG)
