# lychee remaps

This is a collection of [lychee](https://github.com/lycheeverse/lychee) remap expressions. 

## What are remaps?

The `--remap` option rewrites URLs into other URLs. It takes a list of space-separated pairs of strings.  
The first string is the old URL regex pattern and the second string is the new URL regex pattern.
    
<details>
  <summary>
    Click here for more details.
  </summary>

  In the following example, any match of `example.com` is replaced with `example.org`:
  
  ```bash
  lychee --remap 'example.com example.org' -- https://example.com/sitemap.xml 
  ```
  
  You can use this option multiple times to remap multiple domains and you can use
  regular expressions.
  
  Remap is a powerful feature.
  Instead of just replacing domains, you can also use regular expressions to
  replace parts of the URL.
  
  For more information about the `--remap` option,
  check out the documentation at https://lychee.cli.rs and see [#620](https://github.com/lycheeverse/lychee/pull/620), [#1129](https://github.com/lycheeverse/lychee/issues/1129), and the [example config file](https://github.com/lycheeverse/lychee/blob/4d31fb777dc6ddb0f870336c0875c218c5014624/lychee.example.toml).
</details>

## Remap expressions

#### Allow index files when checking a folder

When deploying HTML files to some common platforms like Netlify or Gitlab Pages (or even on a typical Apache HTTP environment), you can rely on the platform to use an "index file", namely, for an URL like https://example.com/foo, it will serve ./public/foo/index.html if such a file exists.

From the [Apache Server documentation](https://httpd.apache.org/docs/trunk/getting-started.html#content):

> Typically, a document called index.html will be served when a directory is requested without a file name being specified. For example, if DocumentRoot is set to /var/www/html and a request is made for http://www.example.com/work/, the file /var/www/html/work/index.html will be served to the client.

Here is the remap expression:

```
lychee --remap 'example.com/((?!.html).)*$ example.com/$1/index.html' https://example.com/foo
```

This command will match URLs that do not contain a slash in the last segment of the path, implying they do not have a file extension like .html, and appends /index.html to the end of these URLs. Therefore, URLs like https://example.com/foo.html won't be affected by this command, as they already have .html at the end. But URLs like https://example.com/foo will be transformed to https://example.com/foo/index.html.

## Contributing

Please contribute your own remap expressions here! You can just edit this file and create a pull request.



