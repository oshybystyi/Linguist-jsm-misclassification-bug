
# Linguist jsm misclassification bug
Repo created to reproduce bug https://github.com/github/linguist/issues/2377

The ui.jsm is taken from [here](https://github.com/Exclumice/FireX-Pixel-Perfect/blob/f05270b23dea663c14943fc1f3524e8eeb0dfd1d/content/ui.jsm)

### Steps I've made

1. Installed linguist (ubuntu 14.04).
   ```
   $ sudo gem install github-linguist
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
   The output from last command should be "Javascript".

3. After adding .gitattributes with content:
   ```
   *.jsm linguist-language=Javascript
   ```
   `project.language` returns 'Javascript' (did not commit that in repo).

### Resolved (solution)

Wrong modeline was set for this file. So it is better to change `Mode: Java` on `Mode: Javascript` (https://github.com/github/linguist/issues/2377#issuecomment-98330724).
