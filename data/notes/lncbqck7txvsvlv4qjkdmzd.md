

##### Handling multiple related projects:

## Monorepos

Mono (single) repo (repository) is the concept of having a shared codebase of multiple projects. 

The opposite of this would be to spread projects across different repositories e.g. repo-A contains BFF code, repo-B contains client code, repo-C is a micro service etc. 

### Advantages

When multiple repositories exist for projects that are interlinked, you issues such as:
- Having to create multiple pull-requests in various projects which are merged in the 'correct' order to minimize breaking changes
- Difficulty of using updated dependencies locally before they are updated on remote e.g. npm libraries.

Having a monorepo can mean:
- managing multiple projects is much easier
- dependencies reflect locally immediately
- improves collaboration between teams by ensuring ownership of ecosystem cohesiveness - poly repos pipelines are often independent and breaking changes can be missed

### In practice

A code repository can be structured in various ways to reflect a mono repo. An example could be:

```bash
- apps/
--- app-one
--- app-two
- packages/
--- ui
--- utilities
--- eslint-config
--- ts-config

```




----

#### References

1. https://www.robinwieruch.de/javascript-monorepos/?ck_subscriber_id=1441143038




-----------

some potentially interesting things:
https://yarnpkg.com/features/workspaces - yarn v2 workspaces overview - shows how easy it is to tie node packages together. other relevant docs are zero installs/offline cache, both super important when it comes to monorepo on CI (re: solving 'how to manage dependencies for N projects')
https://github.com/lerna/lerna - tool for managing monorepos. supports npm or yarn workspaces. yarn v2 covers a lot of its features. ive played with it a LOT and NEVER actually used it. always seemed needless/too specific to package based monorepos (read: not enterprise based monorepos)
https://monorepo.guide/ - thinkmill (aus consultancy) high level intro to monorepos & links to some of their own tools / examples
https://www.atlassian.com/git/tutorials/monorepos - atlassian overview of monorepo architecture & common pitfalls/strategies for solving git scaling
https://www.youtube.com/watch?v=W71BTkUbdqE - old video but an overview of google's monorepo. blew my mind. their investment in tooling is insane.
some of my own stuff:
https://github.com/meatwallace/yarks#clipboard-release-strategy - monorepo package publishing strategy outline from a tool i wrote that uses git, semantic-release and yarn v2/berry workspaces
https://github.com/meatwallace/foundations/tree/master/packages - basic yarn v2 package-based monorepo using the above package for deployment)
https://github.com/meatwallace/tbd - basic yarn v2 app/enterprise based monorepo. its missing anything advanced atm re: scaling but foundationally it's something i could use.
