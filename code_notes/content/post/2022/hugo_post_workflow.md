---
title: "Hugo workflow for posting a blog"
date: 2022-07-03T09:45:32-05:00
draft: false
author: "Jesus Capistran"
tags: ["python", "hugo"]
---

It has been a week since I configured and deployed my Blog with Hugo, I have notpost anyhting since then. Then Today I have experience a lot of trouble in the workflow for posting. That means, the new skill which is not training is inmediatly forgotten. Then lest write this mini guide to get back and remember the posting worflow in Hugo.  

## 1. Create a new Markdown file with Hugo 

The Hugo post should be write locally using a Markdown editor. To create the new file is important to enter into your repository. Mine is called CodeNotes 

- Directory: ``Github/blog/CodeNotes``
	- Github is the folder where I store all my Github repositories 
	- blog is a new folder where I will test every Hugo Blog I will create to learn. In this case the only blog is called CodeNotes.
	- CodeNotes contains the HugoBlog, this is the place we will be working. 

Lets go to the CodeNote folder and create the new entry: 

1. ``cd blog/Codenotes``
2. `hugo new content/post/2022/hugo_post_workflow.md`

The command ``hugo new`` will create a markdown file in ``content/post/2022/file.md`` This command is important because the new file will create markdown file with the following front matter. The basic structure includes the ``title:``, ``date``, and  `draft`. Therefore, the following  infor should be added.

``````
---
title: "Hugo workflow for posting a blog"
date: 2022-07-03T09:45:32-05:00
draft: true
author: "Jesus Capistran"
tags: ["python", "hugo"]
---
``````
## 3. Preview your file in Hugo Server 

Now is time to preview the file you are writing. This can be achieved by using the command ``Hugo Server``. This command will create a local server to explore how your post its going to look once the html files are deployed. 

1. Go to CodeNotes folder
2. write: ``Hugo server``

Preview yor file by opening the link generated link: [http://localhost:1313/](http://localhost:1313/)

``````
(base) ➜  Github cd blog/code_notes
(base) ➜  code_notes git:(main) ✗ hugo server
Start building sites …
hugo v0.101.0+extended darwin/amd64 BuildDate=unknown

                   | EN
-------------------+-----
  Pages            | 22
  Paginator pages  |  0
  Non-page files   |  0
  Static files     |  0
  Processed images |  0
  Aliases          |  5
  Sitemaps         |  1
  Cleaned          |  0

Built in 124 ms
Watching for changes in /Users/capis/Documents/Github/blog/code_notes/{archetypes,content,data,layouts,static,themes}
Watching for config changes in /Users/capis/Documents/Github/blog/code_notes/config.yml
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
``````

## 4. Create the public folder(HTML files)

Once you are satisfied with the local results for your bew blog post, is time to convert the markdown files into html. For this task there is no other think to do than write `Hugo` in ther CodeNotes folder. 

Let's do it: 

```(base) ➜  code_notes git:(main) ✗ hugo
Start building sites …
hugo v0.101.0+extended darwin/amd64 BuildDate=unknown

                   | EN
-------------------+-----
  Pages            | 25
  Paginator pages  |  0
  Non-page files   |  0
  Static files     |  0
  Processed images |  0
  Aliases          |  6
  Sitemaps         |  1
  Cleaned          |  0

Total in 240 ms
(base) ➜  code_notes git:(main) ✗
```
After using `Hugo` command the html are generated in the public folder ``CodeNotes/Public``. Is this folder which contains the whole Hugo Blog (html pages) which form your statis site. 

As you can see, every time you create a blog post, all the html sites should be generated. Let's deplot the Public folder into Github Pages. 

## 5. Deploy into Github Pages 

The new post was created locally, next we preview it using `Hugo server`, and we create the html files using `hugo`, now is time to deploy the Public folder into github pages. 

Note: Remember the Public folder is linked to a second repository in github. That means the first repository called CodeNotes will contain the markdown files and the second repository will contain the html files we are generating in the public folder. 

``````
(base) ➜  code_notes git:(main) ✗ cd public
(base) ➜  public git:(main) ✗ git add .
(base) ➜  public git:(main) ✗ git commit -m "post July 03, Hugo posting workflow"
[main 17dc849] post July 03, Hugo posting workflow
 23 files changed, 179 insertions(+), 84 deletions(-)
 rewrite archives/index.html (66%)
 rewrite index.html (83%)
 rewrite index.json (96%)
 create mode 100644 post/2022/hugo_post_workflow/index.html
 rewrite post/hugo_tutorial/index.html (76%)
 rewrite post/index.html (63%)
 rewrite post/welcome_code_notes/index.html (74%)
 create mode 100644 tags/hugo/index.html
 create mode 100644 tags/hugo/index.xml
 create mode 100644 tags/hugo/page/1/index.html
(base) ➜  public git:(main)

``````

That's all, now you can wait aproximately 1 minute and check your online webpage: 

-  This is mine: [http://jesuscapistran.github.io/](http://jesuscapistran.github.io/)



> If you want to check How to deploy a new Hugo Site into Github Pages follow the video of my second post: [Deplot a Hugo blog in Github](https://jesuscapistran.github.io/post/hugo_tutorial/)
