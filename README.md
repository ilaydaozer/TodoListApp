<h1>TodoListApp using Python with Flask</h1>
This Flask application is a To-Do List application.<br/> Flask is a micro web framework used for building web applications with Python. <br/>It is designed to be simple and fast, allowing for quick development of web applications, and its flexible nature enables it to be extended for various needs.<br/><br/>
<b>1 - Importing Flask and Application Creation</b><br/> <hr/>
<i>   from flask import Flask, render_template, request, redirect, url_for</i> <br/>
<i>   app = Flask(__name__, template_folder='templates')</i> <br/>
Imports the Flask class and other necessary functions (render_template, request, redirect, url_for) from the Flask library. Creates an instance of the Flask application class. The __name__ argument represents the name of the module where the application is located. The template_folder argument specifies the folder where HTML templates are located.<br/><br/>
<b>2 - Data Storage</b><br/> <hr/>
<i>   todos = [] </i> <br/>
Initializes an empty list named todos. This list stores the tasks added by users and their statuses (whether they are completed or not).<br/><br/>
<b>3 - Routing to the Homepage</b><br/> <hr/>
<i>@app.route('/')<br/>
def index():<br/>
    return render_template('index.html', todos=todos)
</i><br/>
Directs requests to the homepage to this function. The render_template function generates a response using the specified HTML template. The todos list is passed to the HTML template and displayed to the user.<br/><br/>
<b>4 - Adding a New Task</b><br/> <hr/>
<i>
  @app.route('/add', methods=['POST'])<br/> 
def add():<br/> 
    todo = request.form['todo']<br/> 
    todos.append({'task': todo, 'done': False})<br/> 
    return redirect(url_for('index'))<br/> 
</i>
This route allows adding a new task. It retrieves form data from a POST request and adds a new task to the todos list. Then, it redirects the user to the homepage.<br/><br/>
<b>5 - Editing a Task</b><br/> <hr/>
<i>
  @app.route('/edit/<int:index>', methods=['GET', 'POST'])<br/> 
def edit(index):<br/> 
    todo = todos[index]<br/> 
    if request.method == 'POST':<br/> 
        todo['task'] = request.form['todo']<br/> 
        return redirect(url_for('index'))<br/> 
    else:<br/> 
        return render_template('edit.html', todo=todo, index=index)<br/> 
</i>
This route allows editing an existing task. It shows the task editing form with a GET request. With a POST request, it receives the updated task and saves it.<br/><br/>
<b>6 - Checking Task Status</b><br/> <hr/>
<i>
  @app.route('/check/<int:index>')<br/>
def check(index):<br/>
    todos[index]['done'] = not todos[index]['done']<br/>
    return redirect(url_for('index'))<br/>
</i>
This route toggles the status of a specific task (marks it as completed or incomplete).<br/><br/>
<b>7 - Deleting a Task</b><br/><hr/>
<i>
  @app.route('/delete/<int:index>')<br/>
def delete(index):<br/>
    del todos[index]<br/>
    return redirect(url_for('index'))<br/>
</i>
This route allows deleting a specific task from the list.<br/><br/>
<b>8 - Running the Application</b><br/> <hr/>
<i>
  if __name__ == '__main__':<br/>
    app.run(debug=True)<br/>
</i>
This if block ensures that the application is run directly when the script is executed. Setting debug=True enables debug mode, allowing for detailed error messages in case of errors.<br/><br/>
<b>9 - Jinja2 and HTML Pages</b><br/> <hr/>
In edit.html and index.html utilizes Jinja2 templating engine. Jinja2 is a popular template engine commonly used with Python web frameworks like Flask. It includes special tags like {% %} and {{ }} for control structures and variables respectively.<br/>
<ul>
  <li>
    Expressions within {% %} are control structures, typically used for loops, conditions, etc.
  </li>
  <li>
    Expressions within {{ }} represent the values of variables and are used to generate dynamic content within the template.
  </li>
</ul>
For example, the {% for todo in todos %} statement initiates a loop and generates repeating HTML content for each item in the todos list. The {{ todo['task'] }} expression represents the value of the 'task' key in the todo dictionary.<br/>
These special tags are part of the Jinja2 template language.


