## williamgrimes.xyz

Personal blogging website built with *Cryogen*:

http://cryogenweb.org/

### Running the Server

The web server can be started from the `my-blog` directory using either Leiningen:

```bash
lein serve # or lein serve-fast
```

or tools-deps:

```bash
clojure -X:serve # or clojure -X:serve-fast
```

The server will watch for changes in the `content` and `themes` folders and recompile the content automatically. The `*-fast` variants perform [fast but partial compilation](https://cryogenweb.org/docs/fast-compilation.html) of only the changed page/post.

You can also generate the content without bringing up a server either via:

```
lein run
```

or via:

```
clojure -M:build
```

### Writing a new post to github pages

This [gist](https://gist.github.com/chrisjacob/825950/133aae5c3fd6e49cb145c7a59c6fb098db4013c4) describes the git branching strategy to setup the git repository with a `gh-pages` branch.

1. Write a new post
``` bash
cd williamgrimes.github.io
git branch # verify branch is cryogen
lein serve
echo {:title \"\"\n :layout :post\n :toc false\n :tags  [\"\" \"\"]}\n\n# Title > content/md/posts/yyyy-mm-dd-post-title.md
# Start writing
```

2. Push the post to cryogen branch
``` bash
git add content/md/posts/yyyy-mm-dd-post-title.md
git push -u origin cryogen
```

2. Push the web-page to `gh-pages`
``` bash
cd public
git branch # verify it is gh-pages
git add *
git push -u origin gh-pages
```

