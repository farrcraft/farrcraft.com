---
title: AWS CodeCommit
author: Josh
type: post
date: 2017-01-09T00:17:15+00:00
url: /blog/2017/01/09/aws-codecommit/
socialShare: false
categories:
  - Code

---
## The Picture So Far

I&#8217;ve used a number of VCS flavors and platforms over the years.  I started with CVS, moved on to SVN for a good long while, and was finally converted over to Git long after it had achieved its critical mass.  I had a sourceforge account (which I loved) long before it became the reviled product it is today, flirted for a bit with beanstalk, and now use github in its public and private forms on a daily basis.  I&#8217;ve even hosted my own private repository servers.



Most recently I ran a private gitlab installation on a t2.small AWS instance backed by a puny db.t2.micro RDS instance.  I don&#8217;t use it very much or very often, so it&#8217;s worked out pretty well and with little investment.  Or, at least it did for the first 408 days of uptime.  One day, the web interface just started returning 500 error messages.



After an embarrassing amount of time just trying to remember how to SSH into the server, I discovered there were apparent filesystem errors in the root volume.  The volume acted as if it were full even though it wasn&#8217;t.  I tried a few corrective actions on the instance to no avail.  It appeared that the only recourse would be to terminate the instance and start with a new one.  In theory, this wouldn&#8217;t be a big deal.  Even though this is a tiny personal server environment, I still built everything using AWS CloudFormation and Chef.  It&#8217;s been a while since I&#8217;ve touched the automation.  The bits have just been sitting there rotting away.  The Disaster Recovery scenario has also never been fully tested on this setup.  But, In Theory &#8211; It Should Work &#8482;.


## A Time For Change



DR curiosities aside, I decided to give an alternative a try rather than restore my existing Gitlab server.  I happened to stumble onto the AWS CodeCommit offering around the same time while working on a completely unrelated project.  This seemed to be a cheaper and easier solution for my needs.  The majority of features offered by a Gitlab or other similar product aren&#8217;t necessary for what I need.  Everything on top of SSH-based Git access is just frosting that I can as easily do without.



Now here&#8217;s the bad news.  My git server is dead at this point.  All I have to work with are the existing cloned working directories of my repositories.  I won&#8217;t be able to create mirrored clones directly from the server.


## Getting Setup

There is a little bit of setup for users to be able to access CodeCommit repositories.  Each user needs to have an AWS IAM user account configured with appropriate policies attached.  There are canned policies for administrative, power user, and read only access and it should be simple enough to adjust the stock policies for more granular permissions if necessary (For instance, limiting which repositories users can access).  Each IAM user also needs to have an additional SSH key policy attached with the public key embedded in the policy.  This second policy is only necessary when using SSH to access repositories.  If you&#8217;re planning on dealing with a number of users, the policies can also be assigned to groups in order to simplify management.  Keep in mind there are additional costs associated with the IAM and KMS products too.  It&#8217;s something like $1 per SSH key per month plus the charge based on the number of requests made.



The last piece of configuration, if you&#8217;re using SSH you need to add an entry to your ~/.ssh/config for the AWS CodeCommit service endpoint and specify your username.  The username is an access key that is associated with the SSH public key when it is embedded in the IAM policy.  If you&#8217;re using HTTPS instead of SSH, then you&#8217;ll need to install the AWS CLI tools to work with your IAM account and then configure git to use it as a credential helper.  Once that is all setup, you can go on using git like normal with the AWS CodeCommit repositories.



The AWS console has a simple interface for creating new repositories, with only the repository name and its description the only inputs.  I was pleasantly surprised to see that the UI is able to display repository content and renders markdown, including default display of README.md files.  There are options for retrieving the repository URL in either SSH or HTTPS format and selecting the branch being displayed.  Settings-wise, the only other feature is to set the default branch.



Once I had my repositories created, all I had left to do was push my working copies to the new URLs.  The documentation recommends making a fresh clone and using the &#8211;mirror option when doing these migrations.  Since I didn&#8217;t have access to my upstream server anymore, I just did a push of my existing clones.  This seemed to work just fine for my basic repositories.



An interesting aspect of the repository URLs, they don&#8217;t appear to be namespaced to any sort of account or user.  This is unlike github, where each repository is anchored to an organization or username.  I&#8217;m not sure if this means that there is a single global repository namespace similar to the way S3 bucket names are first come, first serve or if there is a backend process that disambiguates the repository name based on the IAM user / account correlation.



##  Final Thoughts

Overall, I&#8217;m happy with the service.  Setup wasn&#8217;t overly complex and the documentation was all very clear about the required steps to get going.  After that it pretty much just works.  If you&#8217;re looking for a hosted git solution with all of the bells and whistles of modern social code hosting products a la Github or Gitlab, this isn&#8217;t it.  If all you need is a stripped down basic hosted git server, this should fit the bill perfectly.


One issue that did trip me up after a bit of use was the HTTPS-based user credential setup.  I had setup one of my Macbook Pro laptops to use HTTPS instead of SSH.  Even though it seemed to work just fine when I initially configured the credential helper, it eventually stopped working.  After a bit of troubleshooting, I found that the credentials were cached in my keychain.  The credential helper only provides a short term access token that eventually expires.  I had to remove the cached credential from my keychain and make sure to not save it in the future any time I pushed a repository.