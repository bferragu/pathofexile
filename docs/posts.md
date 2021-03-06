posts
=====

Relevant files:
* `pathofexile/forum/posts.py`
* `pathofexile/forum/post_server.py`
* `pathofexile/forum/templates/post.html`
* `pathofexile/forum/templates/invalid.html`
* `post_server.sh`


Summary
-------

Isolates the contents of the first post of a thread on the Path of Exile
forums. For shop threads, this is usually the entire contents of the shop. This
code will parse out the contents of the original post while still using the
HTML, CSS, and Javascript from www.pathofexile.com.

`post_server.py` is a small HTTP server which listens for requests to           
`http://<server address>:8080/shop/<shop thread number>`, and then returns
relayed HTML content of the first post in the requested thread. To start the
server in the background, run `item_server.sh` when the virtualenv is active.

For an improved way to do this which enables programmatic access of item data,
see <a href="items.md">Items</a>.


Shop Thread Embeds
------------------

This part of the codebase allows you to isolate the first post of a shop thread
while retaining the CSS and Javascript responsible for style and functionality.

It was developed to allow iframe-style embeds on http://www.poearena.com.

This functionality is handled by the PostIsolator class, which scrapes the HTML
of a shop thread and parses it out:


    >>> import pathofexile.forum.posts
    >>> p = pathofexile.forum.posts.PostIsolator(516116)
    >>> p.html

        < complete html for the first post only of shop thread 516116 >
