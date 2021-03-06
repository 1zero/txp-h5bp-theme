# txp-h5bp-theme: a replacement for the Textpattern CMS default theme

This project is designed as a proposed replacement (TXP5) for the default theme that comes as standard with the Textpattern CMS (TXP4). It is intended as a starting point for new users learning the Textpattern CMS for the first time or existing users that want to adapt their current code for modern standards, and is not intended as a finished production theme (though you could use it as such if you want to).

#### Features

1. The code is commented throughout with helpful information to help you learn some of the techniques and tags available within Textpattern.
2. Current best practices gathered from all over the web - in particular the [HTML5 Boilerplate](http://html5boilerplate.com/) and the [Less Framework](http://lessframework.com/).
3. Responsive CSS grid adapts to various device screen sizes.
4. No images used at all.
5. Tested on a wide range of devices, browsers and operating systems.

You can see the latest version of the theme running at [http://www.philwareham.co.uk/](http://www.philwareham.co.uk/).

## Before you begin (fresh installs)

### Adjust Textpattern preferences

#### Essential

1. Set 'Automatically append comments to articles?' to 'no'. [More info](http://textpattern.com/faq/95/comment-display-confusion).
2. Set 'Allow PHP in pages?' to 'yes'. Leave 'Allow PHP in articles?' and 'Allow raw PHP?' set to 'no' for security reasons (you don't really want to allow authors to add their own custom PHP within their articles).

#### Recommended but optional

1. You may decide you don't want to leave Textpattern managed images files loose in the 'images' directory - it may be tidier (and more secure) to create an additonal 'cms' directory within the 'images' directory and use that for any Textpattern managed images instead. You then set the Textpattern advance preference 'Image directory' to your new directory 'images/cms'. Make sure that PHP is able to write to 'images/cms' (usually chmod 777) - you can also set the original 'images' directory back to something more secure (such as chmod 755).
2. Removing 'sbl.spamhaus.org' from the advanced preference 'Spam blacklists (comma-separated)' may yield a (very minor) speed increase.
3. You might want to set 'New comment means site updated?' to 'yes' since [search engines like fresh content](http://www.seoguide.org/seo201-google-ranking.htm).

### Delete surplus forms

There were a number of forms and pages that formed part of the original default theme for Textpattern. For the most part we will be reusing those existing forms with our own code. However, there are some forms you can safely remove from the system as we will not be using them (in fact the original default Textpattern theme does not require them either - they are mostly left over from earlier versions of Textpattern and not used any more).

#### You can safely delete the following forms from your fresh install:

* lofi (article type form)
* noted (link type form)
* popup_comments (comment type form)
* single (article type form)

## How to use these files

Textpattern differs from many CMS solutions in that it stores the all template files (used to build the final page a browser sees) directly in the database as 'styles' (the CSS styling), 'pages' (the main page templates) and 'forms' snippets of code and logic that form building blocks within the 'pages'.

However, many coders like to use their preferred IDE (integrated development environment) to write code and leverage all the tools within those applications provide to make code writing easier. That means you will have to copy/paste from your IDE into the corresponding parts of the Textpattern admin-side which adds a bit of time.

With CSS files you could simply use external stylesheet and link in the traditional way (see below). However there is another solution in the form of the ['cnk_versioning' Textpattern plugin](http://forum.textpattern.com/viewtopic.php?id=27516), which effectively moves the 'styles', 'pages' and 'forms' back out of the database and into external directories for easier editing - a good solution when used in combination with an IDE. If you do use that plugin then dropping the files from this project into your correspondingly named directories will suffice. Detailed information on how to use ckn_versioning is [available at the Textpattern forum](http://forum.textpattern.com/viewtopic.php?id=27516).

### CSS

#### /css/default.css

You can either copy/paste the whole stylesheet into admin area > presentation > style > default, and link as:

    <txp:css format="link" />

or serve as an external stylesheet and link as (for example):

    <link rel="stylesheet" href="/css/default.css">

There are advantages/disadvanatges to both methods...

Keeping style within the database by using the first method means you can make adjustments to the code without the need for FTP or a text editor, but is less flexible because you either lose the tools available in a dedicated IDE (integrated development environment) or have to paste your new code from the IDE which is time consuming. You can however make use of versioning tools such as 'cnk_versioning' Textpattern plugin to streamline this process somewhat (see above).

The second method is much more traditional and flexible though it relies on you having FTP access to change the CSS files.

### Forms

The forms follow the cnk_versioning standard of labelling, in that 'xxxx.misc.txp' is a misc type form, 'xxxx.article.txp' is an article type form, etc. This is only for file structure, when you actually create new forms within Textpattern you should **not** include the '.xxxx.txp', just the first part of the filename. See the analytics form description below.

#### /forms/article_listing.article.txp

Copy/paste over the existing form of the same name that was part of the standard Textpattern install. Used to display listings of articles and is called from the 'default.txp' page when viewing category lists of articles, and the 'archive.txp' page when viewing the archive list of articles.

#### /forms/comment_form.comment.txp

Copy/paste over the existing form of the same name that was part of the standard Textpattern install. Used to format the form for inputting comments.

#### /forms/comments_display.article.txp

Copy/paste over the existing form of the same name that was part of the standard Textpattern install. Used to display all the comments features, and calls other comment type forms.

#### /forms/comments.comment.txp

Copy/paste over the existing form of the same name that was part of the standard Textpattern install. Used to display the individual comments.

#### /forms/default.article.txp

Copy/paste over the existing form of the same name that was part of the standard Textpattern install. Used to display the written article, either as an individual article of part of a set of articles. When called on an individual article basis this form also calls the 'comments_display.article.txp'.

#### /forms/files.file.txp

Copy/paste over the existing form of the same name that was part of the standard Textpattern install. You can call this form from within an article by simply using `<txp:file_download id="xxx" />` (you don't need to specify a form name as 'files' is the default form for files) - you can also call this form from within other any other forms and pages using the same method (just mind your `<p>`'s).

#### /forms/images.misc.txp

Create a new form in the system with name of 'images' and type of 'misc', then copy/paste the code from this file into it. This form can optionally be used in your page/form templates. You could also, for example, display article_images by inserting the following code into a written article...

    notextile. <txp:images form="images" />

...you should use the `notextile.` prefix in this instance because the HTML `<figure>` tag cannot be wrapped inside a `<p>` tag.

#### /forms/links.link.txp

Copy/paste over the existing form of the same name that was part of the standard Textpattern install. You can call this form from within a form, page or article by using `<txp:linklist form="links" />`.

#### /forms/plainlinks.link.txp

Copy/paste over the existing form of the same name that was part of the standard Textpattern install. You could for example use this form to display a list of the 10 most recently added links in the admin-side links page by using `<txp:linklist wraptag="ul" break="li" limit="10" />` within a form, page or article (you don't need to specify a form name as 'plainlinks' is the default form for links). Note we are using 'wraptag' and 'break' attributes to add the `<ul>` and `<li>` respectively. We've also limited the list to 10 items - the default is unlimited (no limit).

#### /forms/search_input.misc.txp

Copy/paste over the existing form of the same name that was part of the standard Textpattern install. Note that this form makes use of the following tag...

    <txp:text />

...which is used to target language strings from the database 'txp_lang' table for the language you set in the Textpattern preferences. For example to display 'Search' in your chosen language the tag would be:

    <txp:text item="search" />

You can get a idea of the items you can target with this tag by looking through the specific language file within the textpattern > lang directory which was created as part of your installation. You would probably not use this tag very often unless you were designing a multi-language site as it adds needlessly to the amount of PHP database calls (that is also true for other tags such as `<txp:site_name />`) - it's included here purely as an example of what the tag is for.

#### /forms/search_results.article.txp

Copy/paste over the existing form of the same name that was part of the standard Textpattern install. This form displays the search results, if any exist.

### Pages

#### /pages/archive.txp

This page template is utilised when viewing a list of articles.

Copy/paste over the existing page of the same name that was part of the standard Textpattern install.

#### /pages/default.txp

This page template is utilised as the standard page layout.

Copy/paste over the existing page of the same name that was part of the standard Textpattern install.

#### /pages/error_default.txp

This page template is utilised when viewing a page error (such as a 404 page not found).

Copy/paste over the existing page of the same name that was part of the standard Textpattern install

### JavaScript

#### /js/modernizr.js

The theme uses [Modernizr](http://www.modernizr.com/) to provide a HTML5 shim for older pre-HTML5 browsers. Modernizr is a great tool that also equips you with a set of tests that can be used to help provide a good experience to all end users, regardless of their browser choice (within limits!) - techniques commonly known as 'progressive enhancement' or 'graceful degradation' depending on whether you add features for capable browsers or provide fallback methods for less-capable browsers respectively.

It is strongly recommended that you read the Modernizr documentation available at their website and then build you own streamlined version of Modernizr with just the tests you'll actually foresee yourself using (the version included here is a full 'kitchen-sink' version with all tests included, not ideal for production use).

## Known issues

Here is a list of current known issues and suggested workarounds if available, none of these issues break the theme so this is purely optional...

#### rel="home" attribute is currently invalid HTML5

The attribute `rel="home"` generated on the navigation bar home link is currently not in the HTML5 draft specification, though it has been proposed and is likely to be accepted at some point soon.

#### acronym tag

Textile (currently v2.2) uses the `<acronym>` tag which is invalid HTML5, instead of the valid `<abbr>` tag. As a workaround, and if you do use abbreviations in articles, you could manually edit the file '/textpattern/lib/classTextile.php' which was part of the Textpattern installation:

Find the following code at around line 435...

    '<acronym title="$2">$1</acronym>',

And replace with...

    '<abbr title="$2">$1</abbr>',

A support ticket has been raised highlighting this issue with Textile but there is currently no ETA as to when (or if) this tag will be updated, due to maintaining backwards compatibility.

#### Unnecessary div wrapper within comments input form

On the comments input form there was a workaround to prevent a XHTML Strict validation error by wrapping a `<div>` (with a class of 'comments-wrapper') inside the `<form>` tag. This is unnecessary for HTML5 validation, so if you don't need it for styling you can safely go ahead and remove it if you wish. Manually edit the file '/textpattern/publish/comment.php' which was part of the Textpattern installation:

Find the following code at around line 144...

    n.'<div class="comments-wrapper">'.n.n;

And either delete the line or replace (comment out) with...

    // n.'<div class="comments-wrapper">'.n.n;

Find the following code at around line 218...

    $out .= n.n.'</div>'.n.'</form>';

And replace with...

    $out .= n.'</form>';

Leaving it in place will not affect HTML5 validation so it's down to your personal preference as to whether you leave the div in the code or not.

#### input type 'email' and input type 'url'

Textpattern (currently v4.4.1) does not utilise the HTML5 input field types 'email' and 'url', instead rendering those input fields as standard type 'text'. Whilst this is fine and indeed still valid code, some devices benefit from having an input clearly defined as such - for example the Apple iPhone displays a different layout of it's keyboard based on what the field is for, so it's good practice to use those types if you can.

To achive this you will need to install and activate the ['rah_replace' Textpattern plugin](http://rahforum.biz/plugins/rah_replace). Then amend you form code as follows:

Change line 14 of 'comment_form.comment.txp' to...

    <txp:rah_replace from='type="text"' to='type="email"'><txp:comment_email_input /></txp:rah_replace></p>

Change line 17 of 'comment_form.comment.txp' to...

    <txp:rah_replace from='type="text"' to='type="url"'><txp:comment_email_input /></txp:rah_replace></p>

## License

Major components:

* Modernizr: MIT/BSD license
* jQuery: MIT/GPL license
* HTML5Doctor CSS reset: Public Domain

Everything else:

* [The Unlicense](http://unlicense.org) (aka: public domain)