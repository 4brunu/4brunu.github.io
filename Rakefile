#############################################################################
#
# Modified version of jekyllrb Rakefile
# https://github.com/jekyll/jekyll/blob/master/Rakefile
#
#############################################################################

require 'rake'
require 'date'
require 'yaml'

CONFIG = YAML.load(File.read('_config.yml'))
USERNAME = CONFIG["username"]
REPO = CONFIG["repo"]
SOURCE_BRANCH = CONFIG["source_branch"]
DESTINATION_BRANCH = "gh-pages"
DESTINATION_DIRECTORY = "../temp-pages/"

def check_destination
  unless Dir.exist? DESTINATION_DIRECTORY
    sh "git clone https://$GIT_NAME:$GH_TOKEN@github.com/#{USERNAME}/#{REPO}.git #{DESTINATION_DIRECTORY}"
  end
end

namespace :site do
  desc "Generate the site and push changes to remote origin"
  task :deploy do
    # Detect pull request
    if ENV['TRAVIS_PULL_REQUEST'].to_s.to_i > 0
      puts 'Pull request detected. Not proceeding with deploy.'
      exit
    end

    # Configure git if this is run in Travis CI
    if ENV["TRAVIS"]
      sh "git config --global user.name $GIT_NAME"
      sh "git config --global user.email $GIT_EMAIL"
      sh "git config --global push.default simple"
    end

    # Make sure destination folder exists as git repo
    check_destination

    sh "git checkout #{SOURCE_BRANCH}"
    Dir.chdir(DESTINATION_DIRECTORY) { sh "git checkout #{DESTINATION_BRANCH}" }

    # Generate the site
    sh "bundle exec jekyll build"

    # sh "pwd"
    # sh "ls"
    # sh "ls _site"

    # Commit and push to github
    # sha = `git log`.match(/[a-z0-9]{40}/)[0]
    # Dir.chdir("_site") do
    #   sh "pwd"
    #   sh "ls"
    #   # check if there is anything to add and commit, and pushes it
    #   sh "if [ -n '$(git status)' ]; then
    #         git add --all .;
    #         git commit -m 'Updating to #{USERNAME}/#{REPO}@#{sha}.';
    #         git push --quiet origin #{DESTINATION_BRANCH};
    #      fi"
    #   puts "Pushed updated branch #{DESTINATION_BRANCH} to GitHub Pages"
    # end

    # Commit and push to github
    sha = `git log`.match(/[a-z0-9]{40}/)[0]
    Dir.chdir(DESTINATION_DIRECTORY) do
      sh "pwd"
      sh "ls"
      # check if there is anything to add and commit, and pushes it
      sh "if [ -n '$(git status)' ]; then
            git add --all .;
            git commit -m 'Updating to #{USERNAME}/#{REPO}@#{sha}.';
            git push --quiet origin #{DESTINATION_BRANCH};
         fi"
      puts "Pushed updated branch #{DESTINATION_BRANCH} to GitHub Pages"
    end
  end
end
