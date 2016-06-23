Markdown
========

.. image:: plugin_small.png
   :align: center
   :alt: The Markdown plugin in action
   :target: plugin.png

.. contents::

{:toc}

# About
-----

This plugin provides a real-time preview of rendered Markdown, that is,
[Markdown](http://daringfireball.net/projects/markdown) converted to `HTML`
and inserted into an HTML template and loaded into a
[WebKit](http://www.webkit.org) view.

# Features
--------

* Allows placing the preview in the sidebar or message window areas
* Updates the preview on-the-fly as you type, automatically.
* Allows simple customization of fonts and colours and complete control
  with custom template files.

# Usage
-----

The preview is active by default for all documents with a Markdown filetype
set. To set a document's filetype, choose from the menus:

.. image:: set_filetype.png
   :align: center
   :alt: Choosing Document->Set Filetype->Markup Languages->Markdown source file
   :target: set_filetype.png

Other than that the operation should be fully automatic. Use the Plugin
Preferences mechanism to customize some settings as described below.

For more information on Markdown syntax, read the
[Markdown Syntax Documentation](http://daringfireball.net/projects/markdown/syntax).

## Preferences

.. image:: settings.png
   :align: center
   :alt: The Markdown plugin's preferences GUI
   :target: settings.png

Using Geany's normal Plugin Preferences mechanism, you can customize some
important settings related to the Markdown preview. The preferences dialog
allows changing the following settings:

| Name         |   Description                                                     |
| ------------ | ----------------------------------------------------------------- |
| Position     |    The area of Geany's UI to put the preview view, currently either in the sidebar or message window (bottom) areas. | 
| Font         |    The regular body font of the preview. | 
| Code Font    |  The font to use for the code tags (monospaced) font of the preview. | 
| BG Color     |  The preview's background color. | 
| FG Color     |  The preview's foreground (text) color. | 
| Template     |  The file containing the HTML template for the preview. | 

There's two ways to access the Plugin settings, one is through the
Plugin Manager using the buttons highlighted below:

.. image:: plugin_mgr.png
   :align: center
   :alt: The Plugin Manager dialog showing the Help and Preferences buttons.
   :target: plugin_mgr.png

Clicking the `Help` button opens this document in HTML format in your web
browser. The other way to access the plugin's preferences is through the
`Edit` menu as pictured below:

.. image:: plugin_prefs.png
   :align: center
   :alt: Accessing plugin preferences from the Edit menu.
   :target: plugin_prefs.png

## Custom Templates


You can provide a custom HTML template file which contains the substitution
strings that get replaced at run-time. The following substitution strings
are available:

| Substitution String           | Description | 
| ----------------------------  | -------------------------------------------- | 
| `@@markdown@@`              | The most important substitution string and gets replaced with the HTML generated from the editor's Markdown buffer. Not having this one in the template makes the plugin completely useless. | 
| `@@font_name@@`             | The normal font family. | 
| `@@code_font_name@@`        | The code/monospace font family. | 
| `@@font_point_size@@`       | The size in points of the normal font. | 
| `@@code_font_point_size@@`  | The size in points of the code/monospace font. | 
| `@@bg_color@@`              | The background color in hex/HTML color notation. | 
| `@@fg_color@@`              | The foreground (text) color in hex/HTML color notation. | 

### Standard version

The default template file (at the time of writing) contains the following
HTML code::

```html
    <html>
      <head>
        <style type="text/css">
          body {
            font-family: @@font_name@@;
            font-size: @@font_point_size@@pt;
            background-color: @@bg_color@@;
            color: @@fg_color@@;
          }
          code {
            font-family: @@code_font_name@@;
            font-size: @@code_font_point_size@@pt;
          }
        </style>
      </head>
      <body>
        @@markdown@@
      </body>
    </html>
```

### Modified version

The following template file enables you to have the following improvements:

* For **header 1**, displayed in red color empaphized, with red underlining
* For **header 2**, displayed in orange color smaller than **header 1**, with orange underlining
* For **header 3**, displayed in green color smaller than **header 2**
* For **header 4**, displayed in blue color smaller than **header 3**

HTML code::

```html
    <html>
      <head>
        <style type="text/css">
          body {
            font-family: @@font_name@@;
            font-size: @@font_point_size@@pt;
            background-color: @@bg_color@@;
            color: @@fg_color@@;
          }
          code {
            font-family: @@code_font_name@@;
            font-size: @@code_font_point_size@@pt;
          }
          h1, h2, h3, h4, h5, h6 {
            margin: 1.3em 0 1em;
            padding: 0;
            font-weight: bold;
          }
          
          h1 {
            color: #dd1600;
            font-size: 1.6em;
            border-bottom: 1px solid #dd1600;
          }
          
          h2 {
            color: #ee9c00;
            font-size: 1.4em;
            border-bottom: 1px solid #ee9c00;
          }
          
          h3 {
            color: #6bb065;
            font-size: 1.3em;
          }
          
          h4 {
            color: #36648b;
            font-size: 1.2em;
          }
          
          h5 {
            font-size: 1em;
          }
          
          h6 {
            font-size: 1em;
            color: #777;
          }
          

        </style>
      </head>
      <body>
        @@markdown@@
      </body>
    </html>
```

As you can see it's just normal HTML/CSS and you can tweak it to make the
preview contents look exactly how you want. The preview view is a WebKit
browser, the same one used by [Google's Chrome Browser](http://google.com/chrome) and [Apple's Safari Browser](http://apple.com/safari) as well as numerous others, and it supports many
modern features such as HTML5 and CSS3 support (at least partially).

If you mess up the default `template.html` file, just delete it and the
default one will be recreated the next time the Markdown plugin is reloaded
(for example when Geany restarts).

# Requirements
------------

The plugin depends on the following libraries:

* [GTK+](http://www.gtk.org>) 2.16 or greater
* [WebKitGTK+](http://webkitgtk.org) 1.1.18 or greater

# License
-------

The Markdown plugin is licensed under the GNU General Public License,
version 2. For the full text of the license, please visit
[http://www.gnu.org/licenses/gpl-2.0.html]. The GPL license covers all code
and files *not* in the ``discount`` directory.

All code inside the ``discount`` directory is under a BSD-style license
(see the ``discount/COPYRIGHT`` file) and all contributions to this code
*will* remain under this license. This will make it easier to integrate
improvements to Discount back upstream if it ever makes sense. So far the
only changes are superficial to allow it to build with the Geany-Plugins
build system and to prevent some compiler warnings.

# Authors
-------

The Geany Markdown plugin is written and maintained by::

    Matthew Brush <matt(at)geany(dot)org>

The plugin includes the Discount Markdown library, developed by::

    David Loren Parsons <http://www.pell.portland.or.us/~orc>

# Contact
-------

You can email me at `matt(at)geany(dot)org`, or find me on the
`#geany` IRC channel on FreeNode, with the nickname `codebrainz`.
