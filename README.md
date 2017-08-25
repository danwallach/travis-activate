# travis-activate.py 

If you have a GitHub project with an ever-growing number of repos, and
you want to automatically activate those repos for Travis-CI builds
without having to manually click all the switches on their web site,
then this script is for you.

## Installation


1) If you haven't already done this, you'll first need to `pip install
requests` for a necessary library.

2) You need to get a "token" for Travis-CI, which isn't the same thing
as the "token" that Travis-CI displays when you log into it. (Why?
Dunno.)

3) First, get a GitHub token with all the "Repo" privileges. You do
this on the GitHub website
[(instructions)](https://github.com/blog/1509-personal-api-tokens). 

4) Use this GitHub token to get a corresponding Travis token:
5) Install the `httpie` command-line tool or work out an equivalent
   to the request below with something else.
6) Run this one-liner, or something like it, which tells Travis your
  GitHub API token and returns you a Travis-API token.

```
echo '{"github_token": "XXXXX"}' | http POST https://api.travis-ci.com/auth/github User-Agent:HTTPIE/1.0 Accept:application/vnd.travis-ci.2+json
```

7) Now you'll have a Travis API token. Edit the `travis-activate.py`
script and paste it at the top where the code says `travisToken = `.
(If you're doing this for multiple repos, you could presumably modify
this script to take the token as an external argument. We're more
interested in having a script that "just works" without any
environmental dependencies.)

8) Edit the `githubProject` and `repoRegex` strings to reflect your
   project (the string after `https://github.com/` when you visit
   any of your repositories) and then a regular expression that lets
   you pick which repos you want to include vs. ignore.


## Usage

Now you can simply run `python travis-activate.py` and
it will both activate any previously inactive repos (matching the
regex) and will request a rebuild for them. Easy!
