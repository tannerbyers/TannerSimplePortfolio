---
title: "Hugo Tips and Tricks"
date: 2020-03-01T21:50:31-05:00
draft: false
---

I am not sure about you but when I first tried to customize a hugo theme, I was very confused. It takes about 2 minutes to get a website up and running but probably about a week to figure out how to properly customize features from the base theme. 

### How do I add a javascript feature?

You can add your JS snippet into a partial override. I recommend the header.html for the JS you want on every page. So just copy:

 {{< highlight Go>}}
 ./themes/{your theme name}/layouts/partials/header.html
{{< / highlight >}}
 move to  (create the folders if they're not already there)
 {{< highlight Go>}}
 ./layouts/partials/header.html{{< / highlight >}}
 
**Now edit it to your hearts content!**

*header.html*
{{< highlight HTML "linenos=table,hl_lines=5-7,linenostart=1" >}}
<nav class="navigation">
    <section class="container">
      <a class="navigation-title" href="{{ .Site.BaseURL | relLangURL }}">
        {{ .Site.Title }}
        <script>
          console.log("FREE THE CODE")
        </script>      
      </a>
      {{ if or .Site.Menus.main .Site.IsMultiLingual }}
      <input type="checkbox" id="menu-toggle" />
      <label class="menu-button float-right" for="menu-toggle"><i class="fas fa-bars"></i></label>
      <ul class="navigation-list">
        {{ with .Site.Menus.main}}
          {{ range sort . }}
            <li class="navigation-item">
              <a class="navigation-link" href="{{ .URL | absLangURL }}">{{ .Name }}</a>
            </li>
          {{ end }}
        {{ end }}
        {{ if .Site.IsMultiLingual }}
          {{ $node := . }}
          {{ .Scratch.Set "separator" true }}
          {{ range .Site.Home.AllTranslations }}
            {{ if ne $.Site.Language .Language }}
              {{ if $node.Scratch.Get "separator" }}
                <li class="navigation-item menu-separator">
                  <span>|</span>
                </li>
                {{ $node.Scratch.Set "separator" false }}
              {{ end }}
              <li class="navigation-item">
                <a href="{{ .Permalink }}">{{ .Language.LanguageName }}</a>
              </li>
            {{ end }}
          {{ end }}
        {{ end }}
      </ul>
      {{ end }}
    </section>
  </nav>
{{< / highlight >}}

---------------------------------------

### How do I add custom css?

To override the CSS, just add your own CSS file with a link tag after all of those, linking to an appropriate file in /static. 
Now you may be saying " I guess this means that we probably have to override the header.html partial to specify the additional CSS link?"

The answer: 

![well yes, but actually no.](https://i.ytimg.com/vi/IGXYzNm29bQ/hqdefault.jpg "Logo Title Text 1")


This is a common problem when users try to customize a theme. In some of my themes I include an option to easily insert custom stylesheets. Maybe you can do a pull request to add the following scheme to the theme:

Inside the config file I assign an array to a variable:
 {{< highlight Go>}}
[params]
    custom_css = ["css/foo.css", "css/bar.css"]{{< / highlight >}}

You can reference as many stylesheets as you want. Their paths need to be relative to the static folder.

Inside the header partial you can include every custom stylesheet from above beside the original one:
 {{< highlight Go>}}
{{ range .Site.Params.custom_css -}}
    <link rel="stylesheet" href="{{ . | absURL }}">
{{- end }}{{< / highlight >}}
This way you don’t touch the header partial at all but you’re still able to overwrite CSS classes.

---------------------------------------

I'll add more tips as I think of them 😊