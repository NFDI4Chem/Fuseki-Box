# Apache Jena Fuseki in a Vagrant Box

**Installs [Apache Jena Fuseki](https://jena.apache.org/documentation/fuseki2/) SPARQL server in a Vagrant box**

* Fuseki version: 4.1.0


Requirements to run box:
* [Git](https://git-scm.com/downloads)
* [Vagrant](https://www.vagrantup.com/downloads.html)
* [VirtualBox](https://www.virtualbox.org/wiki/Downloads)


## Installation

Run the following steps in Terminal (Linux/macOS) or GitBash (Windows):
```bash
git clone https://git.tib.eu/lab-linked-scientific-knowledge/fuseki-box.git
cd fuseki-box
vagrant up
```

After installation process has finished, **visit Fuseki UI at  <http://192.168.60.113/jena/fuseki/>**
Fuseki UI login details:
* user: `admin`
* password: `changeme` 

`vagrant reload --provision` will re-run the Ansile playbook in the created Vagrant box

## Stop and Restart

It is possible to shut down the virtual box and restart it again in order to save CPU and RAM.

```bash
# shut down
vagrant halt

# restart
vagrant reload --provision
```

In order to suspend the virtual box (save the state) use suspend and resume.

```bash
# save the state to disc
vagrant suspend

# resume from disc
vagrant resume
```

# Test Requests to Fuseki
* Status of all datasets `curl http://192.168.60.113/fuseki/ui/$/status -X POST -H 'Accept: application/sparql-results+json,*/*;q=0.9'` 
* SPARQL SELECT query to RXNO dataset `curl http://192.168.60.113/fuseki/ui/rxno/query -X POST --data 'query=PREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0APREFIX+rdf%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E%0APREFIX+owl%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2002%2F07%2Fowl%23%3E%0ASELECT+*+WHERE+%7B%3Fsubject+rdf%3Atype+owl%3AClass%3B+rdfs%3Alabel+%3Flabel.%7D+LIMIT+5' -H 'Accept: application/sparql-results+json,*/*;q=0.9'`


# TODO:
* webserver debug - remove redirect from / to fuseki - as in production it might interfere with TS

* change variables that will be overwritten by host inventories from  `ansible/group_vars/all.yml` to `ansible/roles/*/defaults/main.yml`
* when deployed to public VMs limit UPDATE SPARQL request to localhost and other IP in webserver configuration
* enable [inference](https://jena.apache.org/documentation/inference/)  

LOAD RXNO
`/usr/local/src/apache-jena-4.1.0/bin/tdb2.tdbloader -loc RXNO --graph=https://raw.githubusercontent.com/rsc-ontologies/rxno/master/rxno.owl` 

` rm /etc/nginx/sites-enabled/default ` 
reload
