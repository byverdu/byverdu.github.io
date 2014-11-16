---
permalink: how-to-host-your-blog-at-github-using-jekyll-and-poole

layout: post

title: How to host your blog at GitHub using Jekyll and Poole
---

After I have finished my programming bootcamp I have realized some things, the first one is that I love Git and the version control (commit and commit), the second one is that I love too spending time with the Command Line Interface (talking directly with the OS) and the latest but not the less important I LOVE CODING.

<!-- more -->

I am really impress about all the brilliant brains that are out there that are giving all this amazing tools for the rest of mortals. 

So far today I am going to explain how you can host your blog in [Github pages](https://pages.github.com/), and add some functionality to it. This tutorial is for Mac users.

Further steps:

<ul class="fa-ul">
  <li><i class="fa-li fa fa-square-o"></i>Start a repo that contains your blog.</li>
  <li><i class="fa-li fa fa-square-o"></i>Install a Jekyll theme.</li>
  <li><i class="fa-li fa fa-square-o"></i>Add some more functionality.</li>
  <li><i class="fa-li fa fa-square-o"></i>Style it.</li>
</ul>

The truth is that you should be able to have all this configuration running in a really short time.


## <i class="fa fa-github"></i> Step 1 

By default GitHub lets you can host one site per GitHub account and organization, and unlimited project sites. I am going to concentrate with the GitHub account.

We need to create a new repo with a name that has to be like `username.github.io`, in my case is `byverdu.github.io`. Then what we want is to have that repo locally so we can make changes and push them to GitHub. For do this just type this command into the terminal, changing username with your own details.

`git clone https://github.com/username/username.github.io`

So far we have our repo set up in GitHub and locally, the next step is to connect them and have the website available online. 

> Normally the GitHub pages tutorial will tell you to create a `index.html` file and push it to have the website ready, we will skip that step and do it in the next section.


<ul class="fa-ul">
  <li><i class="fa-li fa fa-check-square"></i>Start a repo that contains your blog.</li>
</ul>


## <i class="fa fa-eyedropper"></i> Step 2 

In addition to supporting regular HTML content, GitHub Pages support [Jekyll](http://jekyllrb.com), a simple, blog-aware static site generator. Jekyll makes it easy to create site-wide headers and footers without having to copy them across every page. Is highly recommended to install Jekyll on your computer to preview your site.

Jekyll is written in Ruby, so for be able to run everything you need the next configuration on your Mac (Sorry Windows).

1. Any Mac comes with Ruby pre-installed, run `ruby --version` in a terminal window and if your version is 1.9.3 or 2.0.0 you are ready to go, otherwise [follow this](https://www.ruby-lang.org/en/downloads/).

2. The easiest way is to install Jekyll is using the GitHub gem that will install all the dependencies that you need. `gem install github-pages`.

The previous gem will install on your machine the following gems: 

{% highlight ruby %}
$ github-pages versions
+-----------------------+---------+
| Gem                   | Version |
+-----------------------+---------+
| jekyll                | 2.4.0   |
| jekyll-coffeescript   | 1.0.0   |
| jekyll-sass-converter | 1.2.0   |
| kramdown              | 1.3.1   |
| maruku                | 0.7.0   |
| rdiscount             | 2.1.7   |
| redcarpet             | 3.1.2   |
| redCloth              | 4.2.9   |
| liquid                | 2.6.1   |
| pygments.rb           | 0.6.0   |
| jemoji                | 0.3.0   |
| jekyll-mentions       | 0.1.3   |
| jekyll-redirect-from  | 0.6.2   |
| jekyll-sitemap        | 0.6.0   |
+-----------------------+---------+
{% endhighlight %} 


3. Now that we have Jekyll installed locally what we want is to add a template that will make our life easier. A really good one is [Poole](http://getpoole.com/), written by @mdo. In my case I have chosen Lanyon. The only thing that you need to do is download the theme that you want and paste everything inside the folder that contains the repo that you just cloned from step 1. 

Now to get your site live on internet you only need to push to GitHub.

`cd folder/cloned/repo` --> `git add --all` --> `git commit -m 'first commit'` --> `git push`

That's all, you will receive a email from GitHub telling you that your site is live or that something went wrong during the process. If the email is telling you that all is `Ok` you can visit `http://username.github.io` in your browser and see your new site, by now will contain all the info that is in your chosen theme. 


<ul class="fa-ul">
  <li><i class="fa-li fa fa-check-square"></i>Start a repo that contains your blog.</li>
  <li><i class="fa-li fa fa-check-square"></i>Install a Jekyll theme.</li>
</ul>


## <i class="fa fa-cogs"></i> Step 3

How to use your Jekyll site?. 


```
# Project structure

_include    # HMTL files to include in your site as sections
_layouts    # Common templates
_posts      # Your posts
_site       # Contains your compiled site
public      # Where you place your CSS, JS and images
_config.yml # Your site configuration
about.md    # Any markdown file will be converted as an html page

```

##### <i class="fa fa-cog"></i> _config.yml

This is the most important file, is the place where you can set up the name of your blog, how to compile Sass, the way to show your links...

{% highlight yaml %}
# Setup
title:            Byverdu
tagline:          '|| Vallverdu'
description:      'There is no place like GitHub'
url:              http://byverdu.github.io/
baseurl:          /
{% endhighlight %}


##### <i class="fa fa-cog"></i> _posts

By default your url is going to have the format `year-month-day-post-name`, if you want to have it excluding the date you can do this.

On your `_config.yml` make sure that you have this configuration

{% highlight yaml %}
permalink:           pretty
relative_permalinks: true

excerpt_separator: "<!-- more -->" # Adds read more feature
{% endhighlight %}

Maybe there is a better solution but the one that I have found is forcing you to write every time the permalink in all your posts.

{% highlight HTML %}
<!-- your post.md file -->
---
permalink: how-to-host-your-blog-at-github-using-jekyll-and-poole

layout: post

title: How to host your blog at GitHub using Jekyll and Poole
--- 
{% endhighlight %}

If you want to add the `<!-- read more -->` feature to your blog you only need to add the `excerpt_separator` property to your `_config.yml` and in your `index.html` change {% raw %} {{post.content}}  by  {{post.excerpt}} {% endraw %}


##### <i class="fa fa-cog"></i> Add Google Analytics and Disquss

To do this step we are going to work with the `_include folder`. We need to create a `google_analytic.html` file and a `disquss.html` file inside the folder with your user preferences.

{% highlight HTML %}
<!-- google_analytic file -->

<script>
  (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
  (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
  m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
  })(window,document,'script','//www.google-analytics.com/analytics.js','ga');

  ga('create', 'UA-342267239443-1', 'auto');
  ga('send', 'pageview');

</script>

{% endhighlight %}


{% highlight HTML %}
<!-- disquss file -->

<div id="disqus_thread"></div>
<script type="text/javascript">
    /* * * CONFIGURATION VARIABLES: EDIT BEFORE PASTING INTO YOUR WEBPAGE * * */
    var disqus_shortname = 'shortname'; // required: replace example with your forum shortname

    /* * * DON'T EDIT BELOW THIS LINE * * */
    (function() {
        var dsq = document.createElement('script'); dsq.type = 'text/javascript'; dsq.async = true;
        dsq.src = '//' + disqus_shortname + '.disqus.com/embed.js';
        (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(dsq);
    })();
</script>
<noscript>Please enable JavaScript to view the <a href="http://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>

{% endhighlight %}

Now we need to add {% raw %} {% include google_analytics.html %} in your ` _include/head.html`

and {% include disquss.html  %} {% endraw %} in your `_layouts/post.hmtl` 

<ul class="fa-ul">
  <li><i class="fa-li fa fa-check-square"></i>Start a repo that contains your blog.</li>
  <li><i class="fa-li fa fa-check-square"></i>Install a Jekyll theme.</li>
  <li><i class="fa-li fa fa-check-square"></i>Add some more functionality.</li>
</ul>


## <i class="fa fa-css3"></i> Step 4

Jekyll already comes with sass built in, the only thing that you need to do is change the extension of any css file for `.sass` or `.scss` and add the 2 lines with 3 dashes at the top of the file and you are ready to go.

If you are planning to use partials, is as easy as adding the code below to your `_config.yml` file, create a `_sass` folder that will contain your partial files and inside your main sass file use the ` @import` rule to add the partials 

```yaml
sass:
  sass_dir: _sass
```
```css
---

---

@import 'base';
@import 'fonts';

```

<ul class="fa-ul">
  <li><i class="fa-li fa fa-check-square"></i>Start a repo that contains your blog.</li>
  <li><i class="fa-li fa fa-check-square"></i>Install a Jekyll theme.</li>
  <li><i class="fa-li fa fa-check-square"></i>Add some more functionality.</li>
  <li><i class="fa-li fa fa-check-square"></i>Style it.</li>
</ul>

Sources

[Github pages](https://pages.github.com/)

[Jekyll](http://jekyllrb.com/)

[joshualande.com](http://joshualande.com/jekyll-github-pages-poole/)

[Sass and Jekyll](http://markdotto.com/2014/09/25/sass-and-jekyll/)