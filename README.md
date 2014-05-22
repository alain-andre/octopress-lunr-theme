octopress-lunr-theme
====================

All the needed for lunrjs search on octopress. in easy steps.

This post is inspired from [jekyll-lunr-js-search](https://github.com/slashdotdash/jekyll-lunr-js-search) and [octopress-lunr-js-search](https://github.com/yortz/octopress-lunr-js-search/blob/master/plugins/search_generator.rb). I couldn't find easy plugins to install/use so I decided to create a minimalist theme that integrated it directly. [This theme](https://github.com/alain-andre/octopress-lunr-theme) is based on a structure allowing [Octopress updates](http://octopress.org/docs/updating/).

![Example](http://alain-andre.fr/images/capture.png)

## Plugin installation.
This theme only modify the **source/_includes/custom/head.html** file.
You can execute the following commands to gain a lot of time.

This part explains how to quickly install the plugin as well as the structures that it needs. Let's start by working on a new branch just in case your theme in place does not support this quick installation.

    $ git checkout -b octopress-lunr-theme
    $ sed -i "/^end/c\  gem 'json'\n  gem 'nokogiri'\nend" Gemfile
    $ bundle install
    $ git clone https://github.com/alain-andre/octopress-lunr-theme.git .themes/octopress-lunr-theme
    $ # If you do not have a theme installed (first install), you must command : bundle exec rake install
    $ bundle exec rake install["octopress-lunr-theme"] # In any case
    $ bundle exec rake new_page['search']
    mkdir -p source/search
    Creating new page: source/search/index.markdown
    $ echo "{% include custom/lunr_search/entries.html %}" >> source/search/index.markdown
    $ cp .themes/octopress-lunr-theme/plugins/octopress_lunr_theme.rb plugins/octopress_lunr_theme.rb
    $ sed -i "/^simple_search:/c\simple_search: #" _config.yml
    $ sed -i "s/^default_asides: \[/default_asides: \[custom\/asides\/lunr_search.html, /" _config.yml
    $ bundle exec rake generate
    $ git add -A
    $ git commit -m "lunr-js-search Installation"


Voilà, you just need now to do a `bundle exec rake preview` to see everythings working. Now it's time to go back to your master branch and check if there is changes at your **source/_includes/custom/head.html** file.

    $ git checkout master
    $ git merge octopress-lunr-theme


## Pour les français
J'ai fais un [post](http://www.alain-andre.fr/blog/2014/04/24/installer-lunr-search-sur-octopress) sur mon blog qui est plus détaillé.
