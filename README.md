# Doubleheader
## Goal
Doubleheader is a basic example project that will require minimal modification from the user to connect to their personal [Amazon Web Services (AWS)](http://aws.amazon.com/) account.  This repository contains everything you will need to deploy a sample "Hello World" web page to an [Elastic Beanstalk (EB)](http://aws.amazon.com/elasticbeanstalk/) environment via [Git](https://git-scm.com/) and the [EB Command Line Interface (EB CLI)](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3.html), the deployment process will then automatically upload sample website content to an S3 bucket via auto-installation of the [s3cmd tool.](https://github.com/s3tools/s3cmd)  This project can be expanded upon for your own use to help you serve up an entire website without having to manually upload projects to EB and assets to S3, with the added .

## Setup
1. Install and setup [Git.](https://git-scm.com/) If you're cloning this project from GitHub you should already be good to go.
2. Install [EB CLI.](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3-install.html) (Note: you may need to restart your machine after installing for modifications to your machines PATH environment variable to work properly)
3. Make a fresh copy of your Doubleheader clone, and be sure to remove any Git files, you will be reinitializing the sample website to work with your EB account.
4. Edit the bucket name in the provided .config file to the name of the S3 bucket you wish to upload your sample files to.
5. Open up your terminal of choice, for our run we used the Git Bash client for Windows.
6. `cd` into the new copy of the sample website files and call `git init`.  This will create new Git information for your local working copy of the repository to be used by EB CLI for the deployment process.
7. Call `git add .` to add all of the files in the working directory.
8. Call `git commit -m "first test deploy"`.
9. Call `eb init` and follow through the steps.  This will create an .elasticbeanstalk directory in your local copy of the repository.  An in depth list of steps can be found [here](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3-configuration.html) via Amazon's documentation.  You will have to provide your aws-access-id and aws-secret-key for your AWS account in step 2.  In step 5, select option `2` for PHP (since the sample web page we provide in Doubleheader is PHP based).
10. Call `eb create`, you will be prompted to provide an environment name and DNS CNAME for the website.  An example `eb create` call can be found [here](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3-getting-started.html) in Amazon's documentation.  AWS will now spin up a new EB environment for your website and do an initial deploy.  A live events list will scroll by giving you an update on the status of the deployment.  If successful, you should be able to log into your AWS account and find a new environment running your index.php file as a webpage.
11. If successful, you should now also see the sample files uploaded to the bucket name you specified for S3 in step 4.  If nothing showed up, be sure to check the log generated in step 11 to see if a command was malformed in the .config file.  In some cases, you may need to create a new IAM policy allowing access to S3 buckets and commands to assign to your EB environment in AWS.  An example policy (which you may have to modify some to get the proper permissions for your specific buckets and commands) can be found at [Will Writes](http://blog.willj.net/2014/04/18/aws-iam-policy-for-allowing-s3cmd-to-sync-to-an-s3-bucket/) blog article on using s3cmd.
12. For any further changes (i.e. as a quick test try changing the message in index.php from `"Hello World"` to something else), add the files you modify and commit via git, then enter `eb deploy`, this will deploy the newest version of your web site to the same environment you created in step 10.  To add more rules and paths of files to upload to S3, modify the .config YAML file.  Some more example commands can be found in [Michael Gallego's Tutorial](http://www.michaelgallego.fr/blog/2013/07/11/automatically-upload-assets-to-s3-when-deploying-to-elastic-beanstalk/) on how to use s3cmd w/ EB.
If everything worked as expected, congratulations!

## Contact
josh@mindaptiv.com
chris@mindaptiv.com

## About
![doubleheader](https://cloud.githubusercontent.com/assets/2531841/8708009/99414c76-2af6-11e5-8c4b-0b064189a783.jpg)
Doubleheader is named for the one-two punch of combining deployment to EB via Git/EB CLI & S3 synchronization w/ EB via s3cmd.  We found many tutorials online for how to do each piece separate, but none that used both in tandem.  We believe integrating both features into a single automated deployment process can help the user focus more on developing and testing their website in a rapid fashion.  Doubleheader is also named for the ~2 week endeavor of guess/check/test/re-test trial-&-error work between two team members to get the process streamlined and working for a production website, and shows (just like the 1989 Transformers Pretender character), two heads can be better than one.
