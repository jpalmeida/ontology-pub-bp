# A simple Semantic Web ontology publication how-to

## About

This is a simple (opinionated) guide to preparing and publishing a Semantic Web OWL ontology (following some FAIR principles and incorporating some good practices).

It is based on [GitHub](https://github.com) for repository and source control, GitHub Pages for hosting, and [pyLODE](https://github.com/RDFLib/pyLODE) for documentation generation. Some recommendations are based on experience using [Protégé](https://protege.stanford.edu)'s support for metadata and [FOOPS! Ontology Pitfall Scanner for FAIR](https://foops.linkeddata.es/FAIR_validator.html).

Author: João Paulo A. Almeida

## Setup of GitHub repository

Create a GitHub repository for your ontology project. For our examples, we will assume a username on GitHub called `user123`, and a repository called `car-ontology`. (Instead of a user, you can also publish your project under an organization on GitHub, so `user123` might as well be an organization name in GitHub.)

Adding a `README.MD` file for the repository is recommended, as this is the text shown when the repository is opened. See <https://github.com/nemo-ufes/gufo/blob/master/README.md> for an example.

Also adding a `LICENSE` file is recommended, matching the license of your ontology. See <https://github.com/nemo-ufes/gufo/blob/master/LICENSE> for an example using Creative Commons Attribution 4.0 International.

You can clone the repository you create and use it as a basis for your work on tools like Protégé.

(If you are new to GitHub, check out <https://docs.github.com/en/get-started/quickstart> and <https://youtu.be/8JJ101D3knE>.)

## Ontology URI and permanent URLs

Adopt an ontology URI which you can match with a permanent URL service such as `http://purl.org/car-ontology#` or `http://purl.org/user123/car-ontology#` if you choose to use the service of [purl.org](http://purl.org).

We recommend a [hash namespace](https://www.w3.org/TR/swbp-vocab-pub/#hash), since the setup is simpler, and entities defined in the ontology will be considered 'fragments' of the ontology, e.g., `http://purl.org/car-ontology#ConvertibleCar`.

For gUFO, we used the URI <http://purl.org/nemo/gufo#>. We setup <http://purl.org/nemo/gufo> to point to
<https://nemo-ufes.github.io/gufo/gufo.ttl> with a `302 Found` http response code (note `https` is used in the target of the redirect, but not in the ontology URI.)

So, in the example, `http://purl.org/user123/car-ontology` should be redirected to `https://user123.github.io/car-ontology/car-ontology.ttl`. See below under Publication with GitHub pages for information on how the Turtle file ends up online in this github.io URL.

(Another example of service for permanent URLs is <https://w3id.org>. It is more complicated to setup than purl.org, and it takes more time too as there are manual steps the maintainers of that service need to take on your behalf. The benefit is that, differently from purl.org, it supports HTTP content negotiation to serve the ontology in multiple serialization formats. See an example of the required [.htaccess file](https://github.com/perma-id/w3id.org/blob/79c131feba2bbf5248cc92d7a3f6515f741e8957/example/.htaccess) for the kinds of rules that need to be written to enable redirection with content negotiation, concerning <http://w3id.org/example>. The approach used for that ontology is to use the same URI to retrieve documentation of the ontology in the form of a Web page, which happens whenever the client is a browser. This is an established practice, but my opinion is that it can be confusing, afterall a URI should identify always a single entity, and an ontology and its documentation are different entities!)

## Versioning

OWL ontologies may have a version URI (or, more generally, IRI), to identify a specific version. Assuming the use of some [semantic versioning](https://semver.org) scheme (with version number structured into MAJOR.MINOR.PATCH), the first release of the ontology would have a version URI `http://purl.org/car-ontology/1.0.0#`. Set up your redirect accordingly. In our running example, `http://purl.org/user123/car-ontology/1.0.0` should redirect to `https://user123.github.io/car-ontology/car-ontology.ttl`.

(If you are using Protégé, note that in the Ontology Version IRI field it suggests an example with `/1.0.0` *after* the hash sign. That is not advisable, as http clients would not be able to resolve different versions of the ontology. This is because the version would be a fragment of the same entity — the ontology as identified with its URI — and what we actually want is to denote a different entity with the version URI.)

## Ontology documentation and recommended meta-data

A bare minimum requirement is that all elements of the ontology are annotated with `rdfs:comment` and `rdfs:label`. The use of `rdfs:isDefinedBy` is also recommended, for example:

```turtle
:ConvertibleCar rdf:type owl:Class ;
                rdfs:subClassOf :Car ;
                rdfs:comment "A Car with a removable roof."@en ;
                rdfs:label "ConvertibleCar"@en ;
                rdfs:isDefinedBy <http://purl.org/user123/car-ontology#> .
```

We recommend the following ontology meta-data:

```turtle
@prefix : <http://purl.org/user123/car-ontology#> .
@prefix owl: <http://www.w3.org/2002/07/owl#> .
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .
@prefix dc: <http://purl.org/dc/elements/1.1/> .
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix vann: <http://purl.org/vocab/vann/> .

@base <http://purl.org/user123/car-ontology#> .

<http://purl.org/user123/car-ontology#> rdf:type owl:Ontology ;
                                         owl:versionIRI <http://purl.org/user123/car-ontology/1.0.0#> ;
                                         owl:versionInfo "1.0.0" ;
                                         dc:title "The Car Ontology"@en ;
                                         dc:creator "Doe, Jane" , "Smith, John" ;
                                         dcterms:bibliographicCitation "Doe, J., Smith. J. \"The Car Ontology\", 2023, http://purl.org/user123/car-ontology"@en ;
                                         dcterms:created "2023-05-01"^^xsd:date ;
                                         dcterms:modified "2023-05-15"^^xsd:date ;
                                         dcterms:language "en" ;
                                         dcterms:license <https://creativecommons.org/licenses/by/4.0/legalcode> ;
                                         vann:preferredNamespacePrefix "car"@en ;
                                         vann:preferredNamespaceUri "http://purl.org/user123/car-ontology#"^^xsd:anyURI ;
                                         rdfs:comment """The objective of the car ontology is to... 
Cite this work as: 
Doe, J., Smith. J. \"The Car Ontology\", 2023, http://purl.org/user123/car-ontology

This work is distributed under Creative Commons Attribution License CC BY 4.0 <https://creativecommons.org/licenses/by/4.0/legalcode>.

For the source repository, see: <https://github.com/user123/car-ontology>"""@en  .
```

See [car.ttl](car.ttl) for the simple example ontology starting with this fragment above.

Check out <http://prefix.cc> to make sure your prefix (`car` identified above `vann:preferredNamespacePrefix`) won't clash with existing ones, and register the chosen prefix in that service.

In addition to those properties above, use when applicable:

* [`owl:priorVersion`](https://www.w3.org/TR/owl-ref/#priorVersion-def) to identify any previous version of the ontology using that version's URI (e.g., `<http://purl.org/user123/car-ontology/0.2.0#>`);
* [`dct:contributor`](http://purl.org/dc/terms/contributor) to acknowledge contributors that are not considered creators;
* [`dct:publisher`](http://purl.org/dc/terms/publisher) to identify an entity "responsible for making the resource available" (typically the organization where the ontology was developed);
* [`dct:source`](http://purl.org/dc/terms/source) to identify a related resource (such as a publication) from which the ontology was derived in whole or in part.

## Publication with GitHub pages

GitHub can serve also as a hosting site for your ontology, such that it can be located (and opened and imported directly from the URL in tools like Protégé). It can also be used to serve any documentation you generate.

On GitHub, navigate to your site's repository.
Under your repository name, click "Settings".
In the "Code and automation" section of the sidebar, click "Pages".
Under "Build and deployment", under "Source", select Deploy from a branch.
Under "Build and deployment", use the branch dropdown menu and select a publishing source; the suggestion is to use the `main` branch and `/docs` folder. Click on "Save".

Place the ontology files (e.g., `car-ontology.ttl`) in the `/docs` folder of your repository (don't forget to commit and push).

Project sites will then be available at `http(s)://<username>.github.io/<repository>` or `http(s)://<organization>.github.io/<repository>`. (After some minutes.)

For example, considering a username called `user123`, and a repository called `car-ontology`, the file will be under `https://user123.github.io/car-ontology/car-ontology.ttl`. This is the URL that your permanent URL should redirect to.

### Generating documentation in html

Generating documentation with tools like [pyLODE](https://github.com/RDFLib/pyLODE) is recommended. See, for example, [car.html](car.html) for the documentation generated automatically for [car.ttl](car.ttl). (If you have Python 3 installed in Linux or Mac OS X, run pyLODE with `pip3 install pylode; pylode car-ontology.ttl -o index.html`. Place `index.html` in the `docs` folder of your repository and it will appear under `https://user123.github.io/car-ontology`.

See also <https://github.com/nemo-ufes/gufo/tree/master/docs> for a markdown overview document, which is rendered in <https://nemo-ufes.github.io/gufo/overview>. It can be used to complement what is generated automatically, and a reference to this kind of documentation can be provided with `rdfs:seeAlso`.

## Findability (the 'F' in 'FAIR' is for 'Findable')

If you serious about publishing your ontology to the world, considering listing it in registries like [LOV](https://lov.linkeddata.es/dataset/lov/suggest).

Also consider assessing your ontology with the [FOOPS! Ontology Pitfall Scanner for FAIR](https://foops.linkeddata.es/FAIR_validator.html), which will check for the presence of metadata and adherence to some established conventions for Semantic Web ontologies.
