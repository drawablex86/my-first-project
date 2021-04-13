---
layout: default
title: How-to-create-a-blog-using-Jekyll
---

# How to create a blog using Jekyll
### Source: https://happycoding.io/tutorials/html/jekyll

# Jekyll

Creating separate html pages for each of your blog pages is going to be a pain in the ass. Handling navigation bar will be cumbersome when your blog eventually grows and have a lot of pages to manage.
  Updating a bunch of files every time you make a change is not what you want to be doing, you should be focusing on your writing instead.

At that point you might look for using a database, but that requires a server. You might build your own JavaScript webapp that fetches post content from files, but that would require a lot of work from scratch.

Wouldn’t it be nice if there was a way to avoid having individual HTML files for every post, without requiring a server or hacky JavaScript code?
*That is what Jekyll is offering you*

----

# Installing Jekyll
1. [For windows](https://jekyllrb.com/docs/installation/windows/)
2. [Others](https://jekyllrb.com/docs/installation/)


*Note*: while trying to install jeykll I faced a lot of set backs. Now I am trying to see if Ruby 2.5 version plus dev kit will work. Also the installation path should be a one word folder.

*warning* Path file names shouldn't contain any special letter or spaces. https://github.com/jekyll/jekyll/issues/7587

----


# Starting Jekyll

To start things off, create a new directory or repo and add an `index.html` file to it:

```
<!DOCTYPE html>
<html>
  <head>
    <title>My Blog</title>
    <link rel="stylesheet" type="text/css" href="/styles.css">
  </head>
  <body>
    <div class="content">
      <nav>
        <a href="/index.html">Home</a>
      </nav>

      <h1>My Blog</h1>
      <p>Welcome to my blog!</p>

      <hr>
      <footer>Thanks for visiting my blog!</footer>
    </div>
  </body>
</html>
```


- Completed the installation of jekyall
- Cloned a test repository to my local pc
- Opened the file path to it in cmd prompt
- To start Jekyll, which builds your site and runs a local server, `cd` to your directory and execute this command:

```
jekyll serve
```

- You site will be locally available at : http://127.0.0.1:4000/ or http://localhost:4000/

**Note** Everytime you want to run a server to a local website folder, you need to use the jekyll serve command with the cmd prompt opened in that path (or use cd)

----

# Adding another page into the mix

add a `contact.html` page to your site:

```
<!DOCTYPE html>
<html>
  <head>
    <title>Contact Me</title>
    <link rel="stylesheet" type="text/css" href="/styles.css">
  </head>
  <body>
    <div class="content">
      <nav>
        <a href="/index.html">Home</a>
        <a href="/contact.html">Contact</a>
      </nav>

      <h1>Contact Me</h1>
      <p>You can email me at kevin@happycoding.io!</p>

      <hr>
      <footer>Thanks for visiting my blog!</footer>
    </div>
  </body>
</html>
```

Inside the navigation bar, each time we add a new page, we will have to add additional information, which is redundant work.

In order to solve that we use something called *layouts*

----

# Using Layout
All that repeated content also makes it harder to update your site. If you want to change the `<nav>` section, you have to change it on every page!

To save yourself from all that trouble, you can use a **layout** to move your shared HTML into a single place. To create a layout, follow these steps:

1.  Create a new directory named `_layouts`
    
2.  Create a new file in the `_layouts` directory named `default.html`
    
3.  Save this content to the `default.html` file:
    
    ```
    <!DOCTYPE html>
    <html>
      <head>
        <title>My Blog</title>
        <link rel="stylesheet" type="text/css" href="/styles.css">
      </head>
      <body>
        <div class="content">
          <nav>
            <a href="/index.html">Home</a>
            <a href="/contact.html">Contact</a>
          </nav>
    
          {{ content }}
    
          <hr>
          <footer>Thanks for visiting my blog!</footer>
        </div>
      </body>
    </html>
    ```
    
    Notice the `{{ content }}` part of this file.
	
4.  Modify your `index.html` and `contact.html` files so that they contain **front matter** (a list of `key: value` pairs between `---`) at the top pointing to the layout you just created.
    
5.  Below the front matter, the only content you need to type out is that what you want to insert as `{{ content }}` into the layout. For example your blog post.

(*Here complex questions arises infront of me, like even if it helps in  templating, how will i manage the navigation into multiple blogs posts and enable tag based search and what not*)

For example, here’s `index.html`:

```
---
layout: default
---

<h1>My Blog</h1>
<p>Welcome to my blog!</p>
```

The front matter at the top tells Jekyll to take the content from the file and insert it into the `default.html` layout.


*It’s now much easier to change the `<nav>` or `<footer>` on every page, because you only need to change it in one file! It’s also easier to add a new page, because you only need to specify the content, not all of the surrounding HTML.*

----

# Front Matter
- Front matter is a set of `key: value` properties at the top of a file.
- Its separated from the content body using two sets of `---` three dashes.

For example, right now the `default.html` layout sets the `<title>` of every page to `My Blog`.

```
<title>My Blog</title>
```

To customize this for every page, first define a `title` property in each file. Here’s the `contact.html` file:

```
---
layout: default
title: Contact Me
---

<h1>Contact Me</h1>
<p>You can email me at kevin@happycoding.io!</p>
```

**Next, modify the `default.html` layout file to use that property:**

```
<title>{{ page.title }}</title>
```

This tells Jekyll to take the `title` property from the front matter of the individual page and include it in the HTML that it outputs.

*You can set any custom properties you want in a page’s front matter and then use those properties in your layout files.*


# Posts
Now comes the most powerful feature of the Jekyll
1.  Create a new directory called `_posts` which will hold all of your blog posts (or tutorial posts, or recipe posts, or whatever kind of post you want).
    
2.  Inside the `_posts` directory, create a post file with this naming pattern:
    
    ```
    YYYY-MM-DD-your-post-title.html
    ```
    
3.  Then inside your post file, add your content. You can also specify a layout using front matter, so each post only contains its own content!
    

For example, here’s `2021-04-13-firstpost.html`:

```
---
layout: default
---

<h1>My first sample blog</h1>
<p>April 13, 2021</p>
<p>Today I wrote my first post using html!</p>
<p>Since i still haven't learn to embedd images in html or how to organise them in the source file, I am unable to add an image to this post.</p>
```

Now you can access that post at Now you can access that post at ]
http://localhost:4000/2021/04/13/firstpost.html

*Note: even if the file formatting is 2021-01-01-title.html the webaddress should be slashs ie 2021/01/01/title.html*

# Customizing Post URLs

By default, a post is available at URL `/YYYY/MM/DD/post-title.html`.

Using the `permalink` property in a post’s front matter you can changes how the post url is named (a custom url)

See the [Permalinks](https://jekyllrb.com/docs/permalinks/) page for different keywords you can use to build a post’s URL format.

For example, if you wanted to use the title without the date, you could add this property to a post’s front matter:

```
permalink: /:title.html
```

Now the URL of the post will be `/firstpost.html` instead of `//2021/04/13/firstpost.html`.


````
---

layout: default

title: Beach

permalink: :title  <!-- Permalink becomes whatever the title here is, ex: it will be /beach here -->

---

  

<h1\>Beach</h1\>

<p\>April 13, 2021</p\>

<p\>I am a beach!</p\>

<img src\="/images/1.jpg" />
````

**Additional Notes**
- You don't have to add permalink: :title syntax on all posts
- It can be configured using a `_config.yml` file
- Add the line `permalink: :title` to the yml file
- You will have to re-run the jekyll server to rebuild the broken link
- Jekyll uses .yml files as a global directory 

# Iterating Over Posts

Putting your files inside the `_posts` directory can help keep your site organized, but there’s another benefit to using posts: you can write code that iterates through them!

*That is, you can create a table of contents based on your existing posts in the index page itself*
 For example, modify your `index.html` file to contain this content:
 
{% raw %}
```html
---
layout: default
title: My Blog
---

<h1>My Blog</h1>
<p>Welcome to my blog!</p>

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
```
{% endraw %}

Notice the code in between {% raw %}`{% %}`{% endraw %} characters. This is called [Liquid](https://shopify.github.io/liquid/), which is a language used by Jekyll that lets you output HTML using things like `if` statements, `for` loops, and variables (which you saw above with  `post.title`).

# Markdown

And for the final reveal it jekyll can translate markup to html!!! **Yay!!**



For example, here’s `2021-03-02-lake.md`:

```
---
layout: default
---

# Lake

March 2nd, 2021

Today I went on a walk around the lake!

![lake](/images/lake.jpg)
```

When you run Jekyll, Jekyll converts this Markdown into HTML, inserts it as the content in the `default.html` layout, and then serves that HTML at the URL specified by the `permalink` property in `_config.yml`.