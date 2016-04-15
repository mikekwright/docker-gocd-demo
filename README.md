Docker - GoCD Demo
============================================================

I am a huge fan of CI/CD and at work we are trying to migrate from a monolithic build
that is using jenkins, to a more streamlined process using 
[throughtworks go](https://www.thoughtworks.com/go://www.thoughtworks.com/go/) which has
a very nice looking ui.   

**Note: [Snap CI](https://snap-ci.com) I believe is based on this product.**     

## Usage

For the first run we will not be tieing into a user management system, however you can use something else (such as
LDAP) to get users managed externally.    

        <server_url>/go/admin/config/server     



### Plugins

For this demo I wanted to test a number of different things, including pull request builds so 
here is the list of plugins that are automatically setup and used with the application.  

1. [Build Github/Stash Pull Requests](https://github.com/ashwanthkumar/gocd-build-github-pull-requests)     
2. [Build Status Github/Stash Notifier](https://github.com/gocd-contrib/gocd-build-status-notifier)    
3. [Slack Build Notifier](https://github.com/ashwanthkumar/gocd-slack-build-notifier)    
4. [Email Notifier](https://github.com/gocd-contrib/email-notifier)     
5. [Docker pipeline plugin\*](https://github.com/Haufe-Lexware/gocd-plugins/wiki/Docker-pipeline-plugin)    

**Note: The Docker pipeline plugin may not be used if it cannot meet our running needs**    

## Notes



## Other

In the future look into seeing if the need or desire for [gocd-janitor](https://github.com/ashwanthkumar/gocd-janitor)
to be setup on a cron job and run.    


