An idea for a blog
==================

Obviously I have this, or some other idea for a long while. Now it's time to pinpoint it.

The blog will be about web craftsmanship. I want to write on regular basis (no less then once a week) about things I'm learning in this field.

I want to create and maintain my own engine for this. The reasons are:

* it will be a nice playground development,

* I will have everything my way.

* I will be able to write about developing my blog on my blog - [like that](/2015-07-12-static-isomorphic-react-blog.md).

Technical considerations
------------------------

* Isomorphic app

  Rendered to static files on build time. Raw markdown and metadata should be hosted along compiled HTML for client side routing and rendering.

* Adhere to *progressive enhancement* principles

* Git integrated

  Both engine and content should be version controlled. There should be two separate repos. Eventually I want to post and update via `git push`.

  As much metadata as possible should be gathered from repo. This would ideally include:

  * Publication date (i.e. the [date given post was merged to master](http://stackoverflow.com/questions/11327535/finding-the-date-time-a-file-appeared-in-a-git-branch)?)
  * Editing history
  * Authors (if there were changes merged from pull requests)

Nice to have features
---------------------

* Twitter integration

  Display my tweets and retweets in a feed among blog posts.

  Post updates to Twitter automatically.

* Stack Exchange integration

  Display my Stack Exchange activity (questions and answers) in a feed among blog posts.
