# git-hooks

Some git hooks to make our lives easier and safer.

![example](https://github.com/brianstorti/git-hooks/blob/master/example.png)

## How it works?

These hooks try to keep you on the right path of your development workflow.
It never stops you from doing anything; it just says what you are doing wrong and asks for confirmation to continue.
Here are the rules that these hooks assume that you should follow (fork and customize it if it doesn't fit your needs):

* Master is always deployable
* Every new feature or bugfix should be done in a separated branch (here called "feature branch")
* The feature branches are always created from the master
* After the feature is done, this branch is merged on the "qa" branch, that should be deployed to a qa environment
* As soon as the feature is ready to go to production, the feature branch is merged on master
* The qa branch should never be merged on master
* The qa branch should never be merged on the feature branch
* You should not commit directly on the master or qa branches
* After a feature branch is merged on master, it should be deleted (both locally and remotely)

```
master*   qa   feature_branch
   |       |
   |-------+---[1]->|
   |       |        |
   |       |        |
   |       |<--[2]--|
   |       |        |
   |       |        |
   |       |<--[3]--|
   |       |        |
   |       |        |
   |<------+---[4]--|
   |       |        |

[1] A new feature branch is created, based on master
[2] After my work is done, the feature branch is merged on qa
[3] If any change is needed, I change my feature branch and merge it on qa again
[4] Finally, when the feature is ready to go do production, it's merged on master
```

As always, you can just bypass the validations with `--no-verify`:
```
git checkout master
git add .
git commit --no-verify -m "deal with it"
```

## How to use it?


**Warning: This will override all of your custom git hooks. If you don't have any custom hook, don't worry. But if you do, make sure to back it up first.**

Just copy this on the root path of your project, wait for some seconds and you should be good to go.
```
git clone git@github.com:brianstorti/git-hooks.git /tmp/git-hooks && \
cp /tmp/git-hooks/hooks/* .git/hooks && \
chmod +x .git/hooks/*
```

If you want to use theses hooks for every created or cloned project, you can take advantage of some git awesomeness (requires Git 1.7.1 or newer):
```
mkdir -p ~/.git_template/hooks
git clone git@github.com:brianstorti/git-hooks.git /tmp/git-hooks
cp /tmp/git-hooks/hooks/* ~/.git_template/hooks

git config --global init.templatedir "~/.git_template"
```

## License

Copyright (c) 2013 Brian Thomas Storti

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
"Software"), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE
LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.


[![Bitdeli Badge](https://d2weczhvl823v0.cloudfront.net/brianstorti/git-hooks/trend.png)](https://bitdeli.com/free "Bitdeli Badge")
