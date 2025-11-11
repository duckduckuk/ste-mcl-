Simple Guide: Adding a New Page (e.g., FAQ)
1. 🐍 Update app.py: Create the Route (The Server Side)
You need to tell Flask what URL to respond to and what file to render.

Action: Open app.py and add this new code block just below your existing routes:

Python

# app.py

# ... (Routes for index, about, services, contact)

# Route for the FAQ page
@app.route('/faq/')
def faq():
    # Renders templates/faq/index.html
    return render_template('faq/index.html', page_title='FAQ', active_page='faq')


if __name__ == '__main__':
    # ...
2. 📂 Create the Template File (The Content)
You need to create the actual HTML file that holds the content for your new page.

Action:

Create a new folder inside your templates directory named faq.

Inside the faq folder, create a new file named index.html.

Content for templates/faq/index.html:

HTML

{% extends "base.html" %}

{% block title %}Frequently Asked Questions{% endblock %}

{% block content %}
<div class="container mx-auto p-8">
    <h1 class="text-4xl font-extrabold text-gray-800 mb-4">Frequently Asked Questions</h1>
    <p class="text-lg text-gray-600">This is the unique content for the FAQ page.</p>
    <!-- Add your questions and answers here -->
</div>
{% endblock %}
3. 🔗 Update _menu.html: Add the Link
You need to modify the central list of pages so the link appears in your menu and gets the "active" highlight correctly.

Action: Open templates/_menu.html and add the new page to the {% set pages = [...] %} list.

Content for templates/_menu.html (Add the new line):

HTML

<!-- templates/_menu.html -->
<div class="menu">
    <div>
        <div>
            <!-- Add the new entry ('faq', 'FAQ') before Contact -->
            {% set pages = [('index', 'Home'), ('about', 'About'), ('services', 'Services'), ('faq', 'FAQ'), ('contact', 'Contact')] %}
            
            {% for endpoint, label in pages %}
            <li class="btn 
                {% if active_page == endpoint %}active{% endif %}
            ">
                <a href="{{ url_for(endpoint) }}">{{ label }}</a>
            </li>
            {% endfor %}
        </div>
    </div>
</div>
🚀 Final Step
After making these three changes, restart your Flask server.

The new "FAQ" link will appear in your menu, and clicking it will take you to the clean URL /faq/, loading the content from your new file.
