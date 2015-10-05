# BlackDoc
Blackdoc is the default theme for easily creating a gu-cs-notes page. 
It's based on [karloespiritu's Blackdoc](https://github.com/karloespiritu/BlackDoc).

## Background
This theme is used to put together a series of lecture notes and host them online. 
The hosting is done via Github Pages. Github Pages will host a site for free from any Github repository with a site in a gh-pages branch. Particularly, gh-pages should contain a static site -- a site without any dynamic content like a database -- and will compile and produce sites from the Jekyll tool really well. 
As a result, the Blackdoc theme is built on Jekyll. Jekyll's a great choice for writing up lecture notes because the notes can be written [in Markdown](http://daringfireball.net/projects/markdown/), a plaintext, easy-to-read analogue for HTML. 
Markdown allows us to create really good looking pages from our lecture notes without putting in much effort at all, and allows us to include highlighted code, compiled LaTeX, images and more. 


## Usage
If you'd like to use the theme, download the source as a zip from the Github sidebar ([or from here!](https://github.com/gu-cs-notes/BlackDoc/archive/master.zip)), and unpack into the base of your repo. 

### Configuring
The whole site is configured from the `_config.yml` file. Hop into the file, and you'll spot a few comments (python-style) where some things should be edited to configure the theme. 
Particularly, the baseurl is important to get right; it's injected into the HTML at compilation, so an incorrect structure will break your URLs. It should be of the form `/REPO-NAME`. 
Other things to edit are the title and tagline of the site and a description of the course, the site's URL, and the Github repo URL for the site.

### Adding content
Content for the Blackdoc theme always begins with some YAML code at the top of the page, seperated from the Markdown content by two horizontal lines. This YAML frontmatter can contain anything, but two things you want to define are `layout` and `title`. Blackdoc will use both of these to generate pages and styles. 

#### Layout
The layout tag is important, because Jekyll understands pages and posts and treats them differently. In the Blackdoc theme, Jekyll will take any Markdown document at the root of the directory which has `layout: page` in the YAML frontmatter and add it to the sidebar, creating a static page from the document. This is the recommended way to lay out course content, as rather than organising by lecture, you can organise by lecture content. Then, when you want to study the use of Sound in HCI, there's a Sound page in the sidebar to click on. 

However in addition to pages, we can also have blog posts. Jekyll is blog-centric, and will collect any Markdown in the _posts/ directory as a blog article. If you want that blog post to be laid out correctly, use `layout: post` and use the document title YYYY-MM-DD-TITLE-GOES-HERE.md and the post will get added to the blog with the title specified in the YAML `title: ` tag, and the date in the filename as the publishing date. 

#### Tying it all together
The title is fairly obvious; whatever the title of the page or post is, add it after the `title: ` tag. So, valid YAML frontmatter for a page on Sound would look like this: 

> ---
> title: Sound
> layout: page
> ---

Neat, huh? 
For examples of using Markdown and Jekyll forntmatter, check out the [Guidelines page](http://gu-cs-notes.github.io/Guidelines). 


## Getting the site out there
*TO WRITE*
