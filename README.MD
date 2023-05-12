# Ontology publication how-to incorporating some best-practices

This is a simple (opinionated) guide to preparing and publishing a Semantic Web ontology.

It is based on GitHub for repository and source control and GitHub Pages for hosting.

## Setup of GitHub repository

Create a GitHub repository for your ontology project. For our examples, we will assume a username on GitHub called `user123`, and a repository called `car`. (Instead of a user, you can also publish your project under an organization on GitHub.)

A README.MD file for the repository is recommended. See <https://github.com/nemo-ufes/gufo/blob/master/README.md> for an example.

A LICENSE file is also recommended. See <https://github.com/nemo-ufes/gufo/blob/master/LICENSE> for an example using Creative Commons Attribution 4.0 International.

## Ontology prefix and permanent URLs

Adopt an ontology prefix which you can match with a permanent URL service, e.g., <http://purl.org>.

For, example, for gUFO, we used <http://purl.org/nemo/gufo#>. We setup <http://purl.org/nemo> to point to
<https://nemo-ufes.github.io/gufo/gufo.ttl> with a 302 Found (note `https` is used in the target of the redirect, but not in the prefixes.)

So, in our example, 


(Another example of service is <https://w3id.org>.)



## Ontology documentation

TODO

## 

Publication of documentation




README.MD

LICENSE file

recommended meta-data

registration in repositories
prefix.cc
void
lov

repository on github

purl.org

documentation pages with pylode

github pages




On GitHub, navigate to your site's repository.
Under your repository name, click "Settings".
In the "Code and automation" section of the sidebar, click "Pages".
Under "Build and deployment", under "Source", select Deploy from a branch.
Under "Build and deployment", use the branch dropdown menu and select a publishing source; the suggestion is to use the `main` branch and `/docs` folder. Click on "Save".

Place the ontology files (e.g., `car.ttl`) in the `/docs` folder of your repository, commit and push.

Project sites will then be available at `http(s)://<username>.github.io/<repository>` or `http(s)://<organization>.github.io/<repository>`. (After some minutes.)

For example, considering a username called `user123`, and a repository called `car`, the file will be under `https://user123.github.io/car/car.ttl`. This is the URL that your permanent URL should redirect to.

