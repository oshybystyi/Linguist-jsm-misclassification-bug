
# Linguist jsm misclassification bug
Repo created to reproduce bug https://github.com/github/linguist/issues/2377

Steps I've made
=====
1. Installed linguist.
   ```
   ...
   Successfully installed github-linguist-4.5.4
   ...
   ```
2. Cd to repo folder and run next commands in irb1.9.1:
   ```ruby
   require 'rugged'
   require 'linguist'
   
   repo = Rugged::Repository.new('.')
   project = Linguist::Repository.new(repo, repo.head.target_id)
   project.language       #=> "Java"
   ```
   The output from last command should be "Javascript"