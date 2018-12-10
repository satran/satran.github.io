---
layout: post
title: On Writing Pull Requests Well
---

I had a conversation recently with a colleague about pull
requests. After a few discussions to and fro I thought it might serve
him and me best if I could pen my thoughts.

For those still unfamiliar with the concept of Pull Requests, a GitHub
jargon, it is a way to request changes to a software repository. Email
was used in the past and still is in the Kernel community. GitLab
calls it Merge Requests. These principles apply for any method you
chose to use.


### Motivation
Motivation is the main factor that decides how a Pull Request
ends up. When I create a Pull Request here are my primary motivations:
- I want the reviewer to understand the intent of my change
- The reviewer should be able to spot things that I have missed out
  while making the change

When I consider these motivations, my attitude towards creating the
pull request changes. When my primary motivation is to finish the
ticket that I am working on as soon as possible a Pull Request can
look like a nightmare for the reviewer. I'm not undermining the need
to finish a ticket. It is how we earn money so it is important, but it
is secondary.

In this article I list three principles I value the most when creating
a Pull Request.

### 1. The size of the PR matters
When a Pull Request is long it is a cognitive load for the
reviewer. The longer it gets, the more difficult it is for the
reviewer to keep the changes in his head. I prefer short Pull
Requests. It is a bit more of effort from my side, but it ensures my
Pull Request is easily reviewed and is merged on time. The longer a
Pull Request the longer it takes to review and thus get merged.

### 2. If you must, use git commits
There are times when it is difficult to make small changes as it would
either not be feature complete, would break tests, or add your valid
reason here. At these times I tend to break it down in small git
commits. This way the reviewer can follow my change process via
the git history.

### 3. Don't do too many changes in the same PR
It is all too alluring to rename a variable or restructure a file in
the same PR where you want to fix a bug. Don't. It makes it difficult
for the reviewer to see what has actually changed. What is actually a
few lines of change now looks like multiple functions deleted and new
ones added. It is best to keep the changes to one functionality or bug
fix.

Code is written for others to read. I think this has been said several
times in the community. Pull Requests follow the same principle, even
more so. It conveys what I as an author propose to alter/modify in the
project. It is not easy. It takes time and thought. But the benefits
out weights the costs. If I want the reviewer to do a good job it is
my job to make it easy for him. Remember the motivation, it changes
how a Pull Request is made.
