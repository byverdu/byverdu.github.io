---
permalink: how-to-start-writing-scss
layout: post
title: How to start writing Scss
---

I really like writing CSS, even that I haven't never done a really large project I realized that sometimes you have to write the same rule over and over.

Digging a little bit I have found out that out there is some useful tools to help you with this problem. Today I will talk about Sass that is based on Ruby.

<!-- more -->

{% highlight ruby %}
def foo
  puts 'foo'
end
{% endhighlight %}

So, you are talking about Scss but you say Sass?

It's basically the same, for a better understanding read this post: [http://thesassway.com/editorial/sass-vs-scss-which-syntax-is-better]()

The idea behind is to follow the DRY (Don't Repeat Yourself) pattern and avoid having really large files. Sass is a ``ruby gem`` but you don't have to know anything about ruby, only opening a terminal window and type:

``gem install sass``

That's all, you have Sass installed. The most basic structure folder:

<pre>
.
└── app
    ├── sass
    │   └── style.scss
    └── style.css
</pre>

You write your **scss** files and after compile them you have a really nice and clean **css** output.

The best way to compile the **scss** files is by watching folders or files.

<pre>
sass --watch app/sass:public/stylesheets
</pre> 

<pre>
sass --watch input.scss:output.cs
</pre>

---

There is a lot of cool things that you can do with Sass, for example using variables. 

<pre><code>
$text_color: #123456;
    
a     { color: $text_color; }
    
.text { color: $text_color }
</code></pre>

You can also play with arithmetic operations:

<pre><code>
$width: 800px;
    
.wrapper{ width: $width-50; } /* 750px */
    
aside   { width: $width/2 }   /* 400px */
</code></pre>

---

Scss will accept any valid css code and the possibility to nest rules, take a look to the following example:

<pre><code class="css">
.look_btn{
  text-decoration: none;
  text-align: center;
  color: $head_col_shad;
  box-shadow: $box-shadow, -1px -1px 1px;
      
  &:hover{
      color: $link_color;
      background: $head_col_text;
      box-shadow: none;
  }
}

</code></pre>

Below is the CSS output. At the begining could seem that we write more (in fact we do) but the really power about this is that if we change any variable value will update automatically all the rules that contain that variable.

<pre><code>
.look_btn {
  text-decoration: none;
  text-align: center;
  color: #535353;
  box-shadow: 1px 1px 1px, -1px -1px 1px; 
 }
 
 .look_btn:hover {
    color: #F54A08;
    background: #ffffff;
    box-shadow: none; 
  }
</code></pre>

---

You can extend rules to avoid writing the same code for two diferent elements.

<pre><code class="css">
.message{
  margin: 5px;
  padding: 5px;
  border-radius: 4px;
  box-shadow: 0 0 3px rgba(0,0,0,0.4);
}
.notice{
	@extend .message;
	background-color: rgba(67,183,120,0.75);
}
.errors{
	@extend .message;
	background-color: rgba(245,74,8,0.75);
}
</code></pre>

CSS output:

<pre><code>
.message, .notice, .errors {
  margin: 5px;
  padding: 5px;
  border-radius: 4px;
  box-shadow: 0 0 3px rgba(0, 0, 0, 0.4);
}
.notice {
  background-color: rgba(67, 183, 120, 0.75); 
}
.errors {
  background-color: rgba(245, 74, 8, 0.75); 
}
  
 </code></pre>
 
 ---
 
 If you are repeating blocks of code you can always use mixins to help you out, they are functions where you place the code which will be called wherever you use it.
 
 <pre><code class="css">
 @mixin link_style{
	text-decoration: none;
	color: red;
	letter-spacing: 1px;
	&:hover{text-decoration: underline;
  }
}

/* You have to include the mixin in your scss code  */
/* You can even extend it */

.link_wrap a { 
    	@include link_style; 
        border:  1px solid black;
        display: block;
}
</code></pre>
 
