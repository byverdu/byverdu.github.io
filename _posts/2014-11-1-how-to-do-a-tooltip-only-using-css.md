---
permalink: how-to-do-a-tooltip-only-using-css
layout: post
title: How to do a tooltip only using CSS
---

After working in a project I have been using a lot the CSS pseudo-elements `:after` and `:before` and as well doing triangles with CSS borders. Then something crossed my head, let's do a CSS pop up.

After finished my bootcamp programming there is one thing that I have realized, I got an acceptable understanding in CSS.

<!-- more -->

#### <i class="fa fa-html5"></i> The HTML file

{% highlight scss %}
<nav id="container">
 <ul class="nav_bar">
  <li id="settings"> <i class="fa fa-cogs"></i>    </li>
  <li id="home">     <i class="fa fa-home"></i>    </li>
  <li id="about">    <i class="fa fa-user"></i>    </li>
  <li id="archive">  <i class="fa fa-archive"></i> </li>
 </ul>
</nav>
{% endhighlight %} 


#### <i class="fa fa-css3"></i> The SCSS file

First we set this couple of mixins that will be useful to avoid rewritting the again and again

{% highlight scss %}
// Mixins and variables for all tooltips examples

@mixin bubble_arrow_common{
 visibility: hidden;
 transition:visibility 0s ease-in 0.5s;
 position: absolute;
}

@mixin up_down_arrow_common{
    border-right: 20px solid transparent;
	 border-left: 20px  solid transparent;
}

@mixin right_left_arrow_common{
  border-bottom: 15px solid transparent;
  border-top: 15px solid transparent;
  top: 0;
}

@mixin set_arrow_tooltip{
 @include bubble_arrow_common();
 content: '';
 color: transparent;
}

@mixin set_bubble_tooltip{
 @include bubble_arrow_common();
 box-shadow: 0px 0px 3px;
 padding: 7px;
 border-radius: 11px;
}

@mixin show_tooltip{
 
 &:hover::before,
 &:hover::after {
	visibility: visible;
 }
}

{% endhighlight %} 


#### <i class="fa fa-css3"></i> SCSS example styling container



{% highlight scss %}

#container{
  
 position:relative;
 width: 350px;
 margin: 0 auto;

 .nav_bar{
   list-style: none;
	 display: flex;

	 li{
		margin-left: 40px;
      
    i{
      font-size: 34px;
      color: #ac4142
		}
	 }
	}
}

{% endhighlight %} 




#### <i class="fa fa-css3"></i> SCSS example for top tooltip

This first example is for the house icon

{% highlight scss %}

#home{
	
	&::before{
		
	    @include set_arrow_tooltip();
		@include up_down_arrow_common();
		border-top: 10px solid rgba(25,25,25,0.3);
		top: -16px;
		margin-left: -4px;
	}

	&::after{

		@include set_bubble_tooltip();
		content: "Home";
		top: -60px;
		left: 62px;
		background-color: rgba(172,65,66,0.3);
	}
	
 @include show_tooltip();
}

{% endhighlight %} 


#### <i class="fa fa-css3"></i> SCSS example for bottom tooltip

This second example is for the user icon

{% highlight scss %}

#about{

  &::before{
	
		@include set_arrow_tooltip();
		@include up_down_arrow_common();
		border-bottom: 10px solid rgba(25,25,25,0.3);
		top: 42px;
		margin-left: -7px;
  }

  &::after{

	  @include set_bubble_tooltip();
	  content: "About";
	  top:  53px;
	  left: 130px;
	  background-color: rgba(172,65,66,0.3);
  }

  @include show_tooltip();
}

{% endhighlight %}


#### <i class="fa fa-css3"></i> SCSS example for left tooltip

This third example is for the cogs icon

{% highlight scss %}

#settings{

	&::before{
	
		@include set_arrow_tooltip();
		@include right_left_arrow_common();

		border-left: 15px solid rgba(25,25,25,0.3);
		margin-left: -20px;
 }

  &::after{

	  @include set_bubble_tooltip();
	  content: "Settings";
	  top:  -7px;
	  left: -26px;
	  background-color: rgba(172,65,66,0.3);
  }

  @include show_tooltip();
}

{% endhighlight %} 


#### <i class="fa fa-css3"></i> SCSS example for right tooltip

This fourth example is for the cogs icon

{% highlight scss %}

#archive{

	&::before{
	
		@include set_arrow_tooltip();
		@include right_left_arrow_common();

		border-right: 15px solid rgba(25,25,25,0.3);
		margin-left: 40px;
  }

  &::after{

	  @include set_bubble_tooltip();
	  content: "Archive";
	  top:  -7px;
	  right: -82px;
	  background-color: rgba(172,65,66,0.3);
  }

  @include show_tooltip();
}

{% endhighlight %} 


To take a look to the compile CSS [Click here](https://github.com/byverdu/byverdu.github.io/blob/master/demos/tool_tip.css)


### Live demo

> All my pixel measures are hard coded so probably you will need to fix them if you are planning to use it.

<nav id="pop_up_demo">
 <ul class="nav_bar">
  <li id="settings"> <i class="fa fa-cogs"></i>    </li>
  <li id="home">     <i class="fa fa-home"></i>    </li>
	<li id="about">    <i class="fa fa-user"></i>    </li>
	<li id="archive">  <i class="fa fa-archive"></i> </li>
 </ul>
</nav>


