# Ontology publication how-to (incorporating some best-practices)

This is a simple (opinionated) guide to preparing and publishing a Semantic Web ontology (following some FAIR principles).

It is based on GitHub for repository and source control and GitHub Pages for hosting.

## Setup of GitHub repository

Create a GitHub repository for your ontology project. For our examples, we will assume a username on GitHub called `user123`, and a repository called `car-ontology`. (Instead of a user, you can also publish your project under an organization on GitHub.)

A `README.MD` file for the repository is recommended. See <https://github.com/nemo-ufes/gufo/blob/master/README.md> for an example.

A `LICENSE` file is also recommended. See <https://github.com/nemo-ufes/gufo/blob/master/LICENSE> for an example using Creative Commons Attribution 4.0 International.

## Ontology prefix and permanent URLs

Adopt an ontology prefix which you can match with a permanent URL service, e.g., <http://purl.org>.

For, example, for gUFO, we used <http://purl.org/nemo/gufo#>. We setup <http://purl.org/nemo> to point to
<https://nemo-ufes.github.io/gufo/gufo.ttl> with a 302 Found (note `https` is used in the target of the redirect, but not in the prefixes.)

So, in our example, the prefix should be <http://purl.org/car-ontology#> or <http://purl.org/user123/car-ontology#> if you choose to group the permanent URLs hierarchically.

(Another example of service for permanent URLs is <https://w3id.org>. It is more complicated to setup than purl.org, and it takes more time too, but it supports HTTP content negotiation to serve the ontology in multiple serialization formats and also to use the same URL for documentation of the ontology. See <https://github.com/perma-id/w3id.org/blob/79c131feba2bbf5248cc92d7a3f6515f741e8957/example/.htaccess> for the kinds of rules that need to be written for that, concerning <http://w3id.org/example>.)

What about version IRI?

## Ontology documentation

Mininum requirement is that elements of the ontology are annoted with `rdfs:comment`. 

## Recommended meta-data



Publication of documentation
documentation pages with pylode

## Publication with GitHub pages

GitHub can serve also as a hosting site for your ontology, such that it can be located (and opened and imported directly from the URL in tools like Protégé. It can also be used to serve any documentation you generate.

On GitHub, navigate to your site's repository.
Under your repository name, click "Settings".
In the "Code and automation" section of the sidebar, click "Pages".
Under "Build and deployment", under "Source", select Deploy from a branch.
Under "Build and deployment", use the branch dropdown menu and select a publishing source; the suggestion is to use the `main` branch and `/docs` folder. Click on "Save".

Place the ontology files (e.g., `car-ontology.ttl`) in the `/docs` folder of your repository (don't forget to commit and push).

Project sites will then be available at `http(s)://<username>.github.io/<repository>` or `http(s)://<organization>.github.io/<repository>`. (After some minutes.)

For example, considering a username called `user123`, and a repository called `car-ontology`, the file will be under `https://user123.github.io/car-ontology/car-ontology.ttl`. This is the URL that your permanent URL should redirect to.




Generating documentation with tools like [pyLODE](https://github.com/RDFLib/pyLODE) is recommended. See for example <http://purl.org/nemo/doc/gufo>, for the kind of documentation generated from a customized version of pyLODE. See <https://github.com/nemo-ufes/gufo/tree/master/docs> for a markdown overview document, which is rendered in <https://nemo-ufes.github.io/gufo/overview>.



## Registration


registration in repositories
prefix.cc
void
lov

https://foops.linkeddata.es/FAIR_validator.html
