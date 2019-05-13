This is a minimal example of a book based on R Markdown and **bookdown** (https://github.com/rstudio/bookdown). Please see the page "Get Started" at https://bookdown.org/ for how to compile this example.

Here the rendered book version is password protected through a js script in the docs-folder, together with the landing index.html.

The JS-script translates the password into a SHA256 has-key, this is the folder name within `docs/` folder that the book should be rendered into. 
In the `_bookdown.yml` you need to add the extra option `output_dir: "docs/GENERATED_SHA_HASH_FROM_PASSWORD"`.
This means that when you build the book locally (with `bookdown::render_book("index.Rmd", "bookdown::gitbook")`), the book will be built into that specified folder, which will also be generated by the command.

I recommend having a small script handy to purge this dacs/hash/ directory, rebuild based on new docs, commit and puch to github in a script in the repo (I call mine `_deploy.sh`), and have the simple R-code above in a script called `_build.R`. 

``` 
# clone the repository to the book-output directory
git pull

# Purge the old files to make sure new ones are built
git rm -rf docs/SHA_GENERATED/

Rscript _build.R

git add --all *
git commit -m "Update the book"
git push -q origin master
```

If github repo has github pages turned on for the  `docs` folder. You will land on the index.html page, which is directly in the `docs` folder. 
Once the correct password it typed in the field, an html iframe will cover the entire view-screen with the rendered book. 

You can copy this repo and build further on it to set up your password protected rendered book. 

The result can be seen at [https://athanasiamo.github.io/bookdown_password/](https://athanasiamo.github.io/bookdown_password/)