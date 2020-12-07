## 2.     Git Branching

 

 

### Branching Workflows

We have 6 types of branches which are master branch, framework develop branch, feature branch, bug fix branch, test case branch and release branch.

 

#### master branch

Firstly, each repository has a master branch. This is the main branch, every one will update from this branch to get the latest code in most situation. We also treat this branch as the develop branch for the test owners to merge all test cases. But before test owner submit test cases, they should ensure test cases are passed in the local. 

 

#### framework develop branch

To ensure framework quality, we do not submit the feature of framework directly to the master branch. We creat a framework develop branch. This branch is only for framework develop, test cases can just merge to the master branch. Nightly tests will be run on the Jenkins system. Only after all framework tests are passed, the commits of on this branch will be merged to master branch. 

 

#### feature branch

During the framework feature developing, the developer should create specific feature branch for developing. There would be multiple feature branches if developing is parallel. After the feature is done and the code is merged, this branch should be deleted. The pull request in this branch should only be made to framework develop branch. 

 

#### bug fix branch

When bug is found. The developer should create a specific branch for the bug fix, This branch is usually created from the mater. It do not has any restriction for making a pull request. There may be multiple bug branches too.

 

#### test case branch

Test case branch is the branch where test owners develop their test cases. This branch can make pull request directly to master branch. But this branch can only commit change under the project folder the test owner is working on. Otherwise the pull request will be declined.

 

#### release branch

After all framework tests passed, it still has chance to cause exception when running test cases with huge device, such as performance tests, the whole test will last several hours. So we added a new branch called release branch. If new framework feature is merged to master, the release test will be triggered, which is a set of performance tests. Report bug if the test is failed. Only after the performance test is passed, or all the bugs are fixed, this branch will be merged to the release branch. 

 

#### typical scenario

When framework need to develop new features in the framework, they create a feature branch, after the feature is done, they make pull request to the framework develop branch. To provide the framework with good quality, framework tests will be run before merge to the master branch. Bug will be reported if any test failed. After all framework test are passed or all bugs are fixe. A tag will be add to the framework develop branch and push to the master branch. A set of performance test may be trigger, after all tests are passed a rag will be added and the commits will be pushed to the release branch. 

 

When test owner want to develop a test case they can create a test case branch from master or release branch. During the develop, they can update from master or release branch to get new feature. If a user find a bug in the framework, they will report the bug on the Jira system. Then framework team will need a bug fix branch to fix the bug. After the bug is fixed they can update again.

![image-20201207221844966](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201207221844966.png)

​                               

 

### Merge Conflict

Merge action happens when we use git pull or git update command. In most cases git can merge the difference automatically, but sometimes it can not , this is called conflict. We will see the message below. 

[Picture]

 

#### Why it happens?

Multiple person change same part of the file will cause the conflict, git can not decide which change should be kept. 

 

#### How to solve it?

After git detect conflict, it will keep both change in the file. After <<<<< HEAD and before =======, it is our change, after ======= and before >>>>> it is other’s change. We need to decide which is correct change, it’s better to discuss with others before we decide which one to keep. 

 

Please remember delete the line with these labels, >>>>> ====== <<<<<<.

 

#### Notice

In some rare case, we found that git can not compare the change correctly in xml format. So keep either part of the conflict will cause the test script can’t work. So before you star to correct the conflict, make sure git compare them correctly. 

 

 

### Avoid Conflict

Fix conflict is annoying, so we’d better to prevent it happen.

 

#### Separate the ownership

If we edit the file serially, it will not cause conflict. If each file has a single owner, when we want to edit file which is owned by others, we can notify the owner, the owner will make sure no one is editing the same part of the test script. 

 

If multiple person is working on same test script, we can separate the ownership base on test set, as long as the change only inside the test set node. 

 

#### Update the code before editing

Lot of people take part in the automation project, so there will be some change in one or two days. It is necessary to update the code to the latest version before we start to doing some change. More commits from the latest code will cause git harder to merge especially in xml format. Beside you may change some part which has already changed by other without knowing.  

 

 