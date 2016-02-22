# jekyll-watch-test

This is a bare-bones project that reproduces the following error that occurs after a Git hook is added to a Jekyll project (using `git-scripts`) each time `jekyll serve` runs:

```
grimlock:jekyll-watch-test egillespie$ jekyll serve
Configuration file: /Users/egillespie/Projects/jekyll-watch-test/_config.yml
            Source: /Users/egillespie/Projects/jekyll-watch-test
       Destination: /Users/egillespie/Projects/jekyll-watch-test/_site
 Incremental build: disabled. Enable with --incremental
      Generating... 
                    done in 0.224 seconds.
        ** ERROR: directory is already being watched! **

        Directory: /Users/egillespie/Projects/jekyll-watch-test/node_modules/git-scripts/bin/hooks

        is already being watched through: /Users/egillespie/Projects/jekyll-watch-test/node_modules/git-scripts/bin/hooks

        MORE INFO: https://github.com/guard/listen/wiki/Duplicate-directory-errors
 Auto-regeneration: enabled for '/Users/egillespie/Projects/jekyll-watch-test'
Configuration file: /Users/egillespie/Projects/jekyll-watch-test/_config.yml
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.
```

## Steps to Manually Reproduce Error

Here are the steps required to create this project from scratch:

1. Create an empty GitHub repository.
2. `git clone git@github.com:egillespie/jekyll-watch-test.git` (use URL for empty repo)
3. `cd jekyll-watch-test/`
4. `bundle init`
5. `vi Gemfile` (Add `gem 'jekyll', '=3.1.1'`)
6. `bundle install`
4. `bundle exec jekyll new .`
5. `npm init -y`
6. `npm install --save-dev git-scripts`
7. `vi .gitignore` (add `node_modules`) 
8. `vi _config.yml ` (add `exclude: [node_modules,package.json]`)
9. `vi package.json` (add `"git": { "scripts": { "pre-push": "echo git-scripts pre-push message says what" } }`)
10. `git add -A .`
11. `git commit -m "Add project"`
12. `git push origin master` (Will see message "git-scripts pre-push message says what" in output)
13. `bundle exec jekyll serve` (Will see ERROR message)
