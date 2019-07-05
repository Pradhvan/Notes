# Data driven apps with Flask

```Python
app = flask.Flask(__name__)

@app.route('/<category>')
def index(category):
    return "hello world !"
```

* *app* creates a single app instance.
* *app* is a variable and can be be named anything, a good convetion is to name it as app.
* app.route maps URLs to views with a unique pattern, optional HTTP verb and route data.
* Static files will be be actomatically served from */static*. 

```Python
{% block main_content %}

    <h1>Python Package Index</h1>

    <h2>Packages</h2>

    {% for p in packages %}

        <div>
    <span class="title">
        {{ p.name.upper() }}
    </span>
            <span class="version">
        {{ p.version }}
        {% if p.summary %}
             <span>
             {{p.summary}}
             </span>
        {% endfor %}
    </span>
        </div>

    {% endfor %}
{% endblock %}
```
* Loops in jinja are written with *{% for %}* block of iterables.
* Looping p in packages till the {% endfor %}, so if p is three times, it would apprear three times in the html.
* Values are written with {{% expressiong %}} i.e *{{p.version}}*
* If statements are written with {% if %}, if the condition is not met it would just remove that block from the rendered html.
* Flask folder structure:
```Python
Project Folder
|-- app.py
|-- data
|-- static
|   |-- css
|   |-- img
|   `-- js
|-- templates
|-- viewmodels
`-- views
```
