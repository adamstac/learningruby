# I created this repo using the GitHub API

I learned how to create a repo on GitHub using the GitHub API. Here's how I did it.

## How I got started

After learning some new Ruby tricks with [the Jumpstart Lab MicroBlogger tutorial](http://tutorials.jumpstartlab.com/projects/microblogger.html), I wanted to try using what I had learned to hack on the [GitHub API](http://developer.github.com/).

The best place to get started with the GitHub API is their [development guides](http://developer.github.com/guides/), specifically [the getting started guide](http://developer.github.com/guides/getting-started/).

## Get your OAuth token

The first step to working with the GitHub API is to get your OAuth token. You can go the route of basic authentication, but that's not quite as secure.

I ran the following command to kickoff the process:

    curl -i -u adamstac \
         -d '{"scopes": ["user", "repo", "notifications", "gist"]}' \
         https://api.github.com/authorizations

If you read the OAuth section of the getting started guide, you might want to take note that I changed my scopes from what was suggested to expand my token's auth to expand my access. Check out
[scopes](http://developer.github.com/v3/oauth/#scopes) to learn more. For the purposes of creating a GitHub repo from the command line "notifications" and "gist" aren't required but hey, it's my token and I'll do with it what I want.

After you run that command you get back some output and in that output is your OAuth token.

## Install Octokit

[Octokit](http://octokit.github.io/) is the simple and official way to work with the GitHub API. Specifically, we need to install [octokit.rb](https://github.com/octokit/octokit.rb).

    gem install octokit

## Hop into IRB

IRB is a Rubyist's best friend. The entirely of what needs done to create a new repo will be done with our new OAuth token and in IRB.

Require `octokit`.

    require 'octokit'

initialize your `@client` object and authenticate to the GitHub API with your OAuth token.

    @client = Octokit::Client.new(:login => "adamstac", :oauth_token => "5199831f4dd3b79e7c5b7e0ebe75d67aa66e79d4")

Create your repo.

    @client.create("repo_name", options = {:description => "The description of your repo", :has_wiki => false, :auto_init => true})

Check out the [create_repository](http://rdoc.info/gems/octokit/Octokit/Client/Repositories#create_repository-instance_method) method to learn more about your other options. When reading the documentation, you may notice that I opt'd to use the alias `create` instead.

## Your new repo

Congratulations! Head to to GitHub and check out your new repo.

## Further exploration

To further explore working with the GitHub API I suggest checking out [the API docs](http://developer.github.com/) and also the code in [Hub](https://github.com/defunkt/hub), specifically [hub/lib/hub/github_api.rb](https://github.com/defunkt/hub/blob/master/lib/hub/github_api.rb).