# Elytron Project Website Based on Jekyll

## Getting Started

These instructions will allow you to run the Elytron website locally for development and testing purposes.

### Installation
The following steps are based on the [Jekyll static site generator docs](https://jekyllrb.com/docs/).

1. Install a full [Ruby development environment](https://jekyllrb.com/docs/installation/)
2. Install jekyll and [bundler](https://jekyllrb.com/docs/ruby-101/#bundler)  [gems](https://jekyllrb.com/docs/ruby-101/#gems) 
  
        gem install jekyll bundler

3. Fork the [project repository](https://github.com/wildfly-security/wildfly-elytron), then clone your fork.
  
        git clone git@github.com:YOUR_USER_NAME/wildfly-elytron.git

4. Change into the project directory:
  
        cd wildfly-elytron

5. Checkout the [develop](https://github.com/wildfly-security/wildfly-elytron/tree/develop) branch:
  
        git checkout develop

6. Use bundler to fetch all required gems in their respective versions

        bundle install

7. Build the site and make it available on a local server
  
        bundle exec jekyll serve

   If you encounter the following message:

        FATAL: Listen error: unable to monitor directories for changes.  
        
   Please refer to these [instructions](https://github.com/guard/listen/wiki/Increasing-the-amount-of-inotify-watchers) to fix this.       
        
8. Now browse to http://localhost:4000/wildfly-elytron/

> If you encounter any unexpected errors during the above, please refer to the [troubleshooting](https://jekyllrb.com/docs/troubleshooting/#configuration-problems) page or the [requirements](https://jekyllrb.com/docs/installation/#requirements) page, as you might be missing development headers or other prerequisites.


**For more regarding the use of Jekyll, please refer to the [Jekyll Step by Step Tutorial](https://jekyllrb.com/docs/step-by-step/01-setup/).**

## Writing a blog post

To write a blog post:

1. Add an author entry in [_data/authors.yaml](https://github.com/wildfly-security/wildfly-elytron/tree/develop/_data/authors.yaml)
    - Your profile picture is fetched from [the Gravatar service](https://gravatar.com/). Create an account,
      and then associate your email with the account. Validate your picture with [the email checker](https://gravatar.com/site/check/). 
      The field `emailhash` in authors.yaml is set using [these instructions](https://gravatar.com/site/implement/hash/),
      or with the output from the following command:
        ```bash
        echo -n 'email@address.com' | awk '{NF=1;printf "%s", tolower($1);}' | md5sum - | awk 'NF=1'
        ```
2. Create a blog post entry under [_posts](https://github.com/wildfly-security/wildfly-elytron/tree/develop/_posts)
    - The file name should be `yyyy-mm-dd-slug.adoc`
3. Your blog post should be in asciidoc format (take a look at other blogs posts in the _posts directory to see examples)
    - To view your blog post without needing to build locally, the following steps can be used:
        - If you haven't done so already, generate a fine-grained GitHub token following the instructions
          [here](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens#creating-a-fine-grained-personal-access-token). Use this value to add a `PUSH_GITHUB_TOKEN` secret to your
          repository secrets (i.e., https://github.com/<YOUR_GITHUB_USERNAME>/wildfly-elytron/settings/secrets/actions).
            - You should set the **Resource owner** to your user account, and **Repository access** to "Only select repositories" and then your fork of `wildfly-elytron`. The only **Repository permissions** needed are "Access: Read and write" for _Contents_ and _Actions_ (this also enables "Access: Read" for _Metadata_, which is required).
        - Simply push your changes to the `develop` branch on your `wildfly-elytron` fork. This will trigger a website
          build that will get pushed to the `gh-pages` branch on your fork. Then browse to
          http://<YOUR_GITHUB_USERNAME>.github.io/wildfly-elytron/blog and click on your post.
            - The `gh-pages` branch must already exist in your fork before you can build the site. You
              can copy it from this repo by running these commands locally:
                ```bash
                git fetch upstream
                git checkout gh-pages # This should include a message that the branch is tracking upstream/gh-pages
                git push origin gh-pages
                ```
    - To view your blog post locally, first follow the instructions [above](https://github.com/wildfly-security/wildfly-elytron/tree/develop#installation) to build the Elytron website
      locally. Then browse to http://localhost:4000/wildfly-elytron/blog and click on your post.
4. Submit a pull request against the `wildfly-elytron` `develop` branch

