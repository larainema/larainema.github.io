---
title: "Contribute to OpenStack"
date: 2015-12-02
categories: 
  - "openstack"
tags: 
  - "openstack"
---

This August, I transferred to a new team as an upstream contributor on the OpenStack Infrastructure team. I started my new journal in the OpenStack world, I have been focusing on the jenkins-job-builder, OpenStack CI and OpenStack QA projects. I had my first OpenStack patch merged on August 11, 2015, I would like to write and share my experience about contribute to OpenStack projects.

- **What to contribute?**                                                                                            

My first patch is a bug fix for openstack documentation, documentation is the easiest start for the first patch, also you can ask for help from your colleagues to find out where to contribute, If you don’t have a buddy to make recommendations, just pop into the #openstack-infra #openstack-qa and #openstack-doc channel in IRC and just ask for suggestions.

- **Setup your dev** **environment**                                                                OpenStack has done an excellent job of documenting the [steps for new developers](http://docs.openstack.org/infra/manual/developers.html#getting-started) and I recommend following those instructions.

- 1. Account Setup                                                                                   First, You’ll need a [Launchpad account](https://launchpad.net/+login), since this is how the Web interface for the Gerrit Code Review system will identify you. Also to contribute to any OpenStack project, you’ll need to create a community account and sign the agreement. Make sure the email you provide for your OpenStack email address matches your Ubuntu Single Sign On email address! Also make sure to [update your contact information](https://review.openstack.org/#/settings/contact) on Gerrit.You’ll also want to [upload an SSH key to Gerrit at review.openstack.org](https://review.openstack.org/#/settings/ssh-keys) while you’re at it, so that you’ll be able to commit changes for review later. This is different from adding a key to Launchpad. Ensure that you have run these steps to let git know about your email address:
        
        ```
        git config --global user.name "Firstname Lastname"
        git config --global user.email "your_email@youremail.com"
        git config --global http.proxy http://web-proxy.cce.hp.com:8088 (optional for env under firewall)
        git config --global https.proxy http://web-proxy.cce.hp.com:8088 (optional for env under firewall)
        ```
        
    2. Install git-review
        
        ```
        apt-get install git-review
        git config --global gitreview.scheme https
        git config --global gitreview.port 443
        git config --global gitreview.username yourgerritusername
        ```
        
    3. Working on a projectClone a repository in the usual way, for example:
        
        ```
        git clone https://git.openstack.org/openstack/<projectname>.git
        debug: nc review.openstack.org 29418
        debug: ssh -p 29418 larainema@review.openstack.org gerrit version
        ```
        
    4. If you didn’t work under the Great China firewall, the envroument will works, but the port 29418 is blocked by the firewall, so ssh didn’t work in China, you need to access Gerrit by HTTPS.Keep in mind that you will need to generate an [HTTP password in Gerrit](https://review.openstack.org/#/settings/http-password) to use this connection. You should run the following command before “git review -s”:
        
        ```
        git remote add gerrit https://<username>:<password>@review.openstack.org/<umbrella repository name>/<repository name>.git
        ```
        
    5. Obtain commit-msg
        
        ```
        $ scp -p -P 29418 <your username>@<your Gerrit review server>:hooks/commit-msg <local path to your git>/.git/hooks/ 
        $ curl -Lo <local path to your git>/.git/hooks/commit-msg <your Gerrit http URL>/tools/hooks/commit-msg
        ```
        
    6. In general you should be using a local Python rather than a system Python. You know if you’re using system Python if you have to type “sudo” anytime you want to do anything beyond running a program (like pip). Virtualenv makes doing this really easy. My colleagoue have a great blog about [how to use virtualenv](https://rbtcollins.wordpress.com/2015/07/12/bootstrapping-developer-environments-for-openstack/)

 

- **Run the tests**                                                                                                      Once you’ve cloned the git repository, follow the instructions in the README at the parent level to do any necessary local setup. It will likely involve installing a bunch of python dependencies. See the section above for my recommendation involving using virtualenv for this.After configuring and installing, before touching anything else, I highly recommend running the tests to make sure everything works on your system. It’s incredibly hard to troubleshoot when you’re not sure if your patch broke something or if it was a setup issue that’s causing test failures. To run the tests you’ll need to set up tox if you haven’t already. It’s really straightforward (pip install tox), see the [OpenStack Python Developer Docs](http://docs.openstack.org/infra/manual/python.html) if you’re not sure how.

 

- **Make the changes**
- ```
    git checkout -b TOPIC-BRANCH
    git commit -a
    git review
    ```
    

[Git commit messages](https://wiki.openstack.org/wiki/GitCommitMessages) should start with a short 50 character or less summary in a single paragraph. The following paragraph(s) should explain the change in more detail.

- **Update the changes**
- ```
    git commit -a --amend
    git review
    ```
    
- **Get your patch reviewed**                                                                                          Once the test have passed, you’ll need to get your change accepted by 2 core members in order to get it merged. If your patch has been reviewed and says “Needs Workflow” it means another core needs to approve it before it can be merged. To find out who the core members are that can +2 or approve your patch, visit the project’s page in review.openstack.org. Click on “Access” at the top of the screen and then click on any of the project-core links to see a list of people. You can add names as Reviewers to your change from your change’s url or you can ask in #openstack-infra if those individuals could review your change. Once your patch has been approved, it will be automatically merged!

 

- You can watch your progress as an OpenStack contributor at [Stackalytics](http://www.stackalytics.com/)!

 

### Useful Links

- OpenStack Developers’ Guide –[http://docs.openstack.org/infra/manual/developers.html](http://docs.openstack.org/infra/manual/developers.html)
- Virtualenv – [https://virtualenv.pypa.io/en/latest/](https://virtualenv.pypa.io/en/latest/)
- DevStack – [http://docs.openstack.org/developer/devstack/](http://docs.openstack.org/developer/devstack/)
- OpenStack Python Developers’ Guide –[http://docs.openstack.org/infra/manual/python.html](http://docs.openstack.org/infra/manual/python.html)
- Git Commit Messages – [https://wiki.openstack.org/wiki/GitCommitMessages](https://wiki.openstack.org/wiki/GitCommitMessages)
- Stackalytics – [http://www.stackalytics.com](http://www.stackalytics.com/)
