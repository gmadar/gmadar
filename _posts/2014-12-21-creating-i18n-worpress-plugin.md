---
layout: post
title:  "Creating an i18n WordPress Plugin"
date:   2014-12-21 13:36:32 +0300
categories: placeholder
permalink: "creating-an-i18n-wordpress-plugin/"
---

It was not an easy task to search for all steps needed to create a WordPress plugin that supports multiple language.

So I’m listing here all the steps I learned in the proccess of developing an i18n WordPress plugin.

# Step 1 : Choose a Domain For Your Plugin Texts

A domain is a name space you choose to facilitate your texts under. And you control when these texts will be available.

What I did was to add a function when the plugin was loaded

{% highlight javascript %}
add_action('plugins_loaded', 'my_custom_init_function');
{% endhighlight %}

This function is called when the plugins are loaded, In ‘my_custom_init_function’ I load the text with the domain name I picked for the texts:

{% highlight javascript %}
function my_custom_init_function() {
 $plugin_dir = basename(dirname(__FILE__));
 load_plugin_textdomain( 'my-custom-domain-name', false, $plugin_dir . '/language');
}
{% endhighlight %}

the [load_plugins_textdomain][link1] load the translation from the third parameter location. I chose to put the translation files inside the plugin so it will be part of the plugin package. I’ll cover on how to create the translation files in Step 3

# Step 2 : Wrap All Your Texts With The Translation Function

We need to declare which text is for translation. We do that with the [__ (double underscore)][link2] function. The second parameter of the __ function is the text domain we chose in step 1.  So an example usage will be:

{% highlight javascript %}
__( 'Some sample text', 'my-custom-domain-name' )
{% endhighlight %}

And we are done! The only thing that is left is  to do the actual translation – That will be done in the next step

# Step 3 : Translate Your WordPress Plugin

Translation in WordPress is made with .po and .mo files. You use the .po files in a text editor and these files are converted to .mo files which are binary files. You can save a lot of headache by letting some other plugin to create those files for you. I played with a few plugins and the one that I liked the most was [Codestyling Localization][link3]. With this plugin you translate your plugin directly from the admin panel ( tools > localization ) and you can also generate the .mo file in one click.

# More Information

You can have multiple text domains in your plugin, that make sense if you have different areas your plugin is running under and than you can make a text domain for each area. For example if your plugin is running in the admin panel and in a blog post it make sense to separate the two into two text domains.

[link1]: https://codex.wordpress.org/Function_Reference/load_plugin_textdomain
[link2]: http://codex.wordpress.org/I18n_for_WordPress_Developers
[link3]: https://wordpress.org/plugins/codestyling-localization/