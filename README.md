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
