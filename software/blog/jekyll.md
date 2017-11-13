$ sudo apt-get install ruby-full
$ sudo gem install jekyll

$ jekyll build
# => The current folder will be generated into ./_site
$ jekyll build --watch --destination <destination>
# => The current folder will be generated into <destination>
#    watched for changes, and regenerated automatically.
$ jekyll serve
# => A development server will run at http://localhost:4000/
# Auto-regeneration: enabled. Use `--no-watch` to disable.
