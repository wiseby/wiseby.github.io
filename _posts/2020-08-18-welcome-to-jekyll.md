---
layout: post
title: "Welcome to Jekyll!"
date: 2020-08-18 11:44:40 +0200
---

You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:

{% highlight ruby %}
def print_hi(name)
puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/

\*\*\* **Update 13/9 2022** \*\*\*

Installation issues with som gem packages.

- upgraded to the latest github-pages version 277
- This upgraded Jekyll to version 3.9.2
- The new version of Jekyll added support for Ruby 3.0 and 3.1
- Needed to add gem [**webrick**](https://jekyllrb.com/news/2022/03/27/jekyll-3-9-2-released/)

I also had errors with nokogiri, but that was relates to gems not working with ruby version 3 and missing dependencies for native libraries such as libxml2.

Link to fix [Trouble of Nokogiri gem installing](https://7in4tranlh.wordpress.com/2016/10/26/trouble-of-nokogiri-gem-installing/)
