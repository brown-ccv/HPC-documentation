# Version Control

Version Control refers to the management of changes made to source code or any such large amount of information in a robust manner by multiple collaborators. Version Control is a crucial part of software development as it ensures data integrity during code sharing and also acts as a safeguard against accidental loss of changes made to the code. Moreover it allows multiple people to contribute to a code base in a transparent manner, preventing any loss of information. The two main types of version control systems are:

1. Centralized Version Control System \(CVCS\) - eg. SVN \(Subversion\)
2. Distributed Version Control system \(DVCS\) - eg. Git, Mercurial

In the CVCS model, a single large repository is maintained on a server. All clients \(read: contributors\) check out files from this server and submit changes to it. SVN \(Subversion\) is a very popular tool for CVC. Examples of organizations where SVN is used: Facebook, Apache Software Foundation.

In the DVCS model, all clients have their own copy of the repository. They can maintain changes in their local repository and periodically sync with the central repository. A very popular tool is Git. Git has become more popular of late because of an emphasis on Open Source software. Online hosting sites like [GitHub](https://github.com) and [BitBucket](https://bitbucket.org) which are integrated with Git make it easier to distribute Open Source code. Moreover, they also allow better access control for different contributors.

What model or tool to choose depends on your requirements. Both SVN and Git are installed on Oscar as modules. Here are some helpful links to get started with version control:

* [Getting Started - About Version](https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control) [Control](https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control)
* [Apache Subversion](https://subversion.apache.org/docs) [Documentation](https://subversion.apache.org/docs)
* [Atlassian Git Tutorials and Training](https://www.atlassian.com/git/tutorials)

## SVN at Brown

CIS at Brown maintains a server where you can host your SVN repository. See this page for more information: [https://it.brown.edu/services/type/version-control-subversion](https://it.brown.edu/services/type/version-control-subversion)

## Git Configuration

While using Git on Oscar, make sure that you [configure Git](https://www.atlassian.com/git/tutorials/setting-up-a-repository/git-config) to have your correct Name and Email ID to avoid confusion while working with remote repositories \(eg. GitHub, BitBucket\).

```bash
$ git config --global user.name "John Smith“
$ git config --global user.email john@example.com
```

