# Apache Jena Fuseki in a Vagrant Box

**Installs [Apache Jena Fuseki](https://jena.apache.org/documentation/fuseki2/) SPARQL server in a Vagrant box**

* Fuseki version: 4.6.1


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

# Queries to Fuseki SPARQL-endpoint 

* Status of all datasets
    * request: `curl http://192.168.60.113/jena/fuseki/$/status -X POST -H 'Accept: application/sparql-results+json,*/*;q=0.9'` 

* SPARQL SELECT query to RXNO dataset
    * request: `curl http://192.168.60.113/jena/fuseki/rxno/query -X POST --data 'query=PREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0APREFIX+rdf%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E%0APREFIX+owl%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2002%2F07%2Fowl%23%3E%0ASELECT+*+WHERE+%7B%3Fsubject+rdf%3Atype+owl%3AClass%3B+rdfs%3Alabel+%3Flabel.%7D+LIMIT+50' -H 'Accept: application/sparql-results+json,*/*;q=0.9'`
    
* SPARQL UPDATE: 
   * denied to all IP except those defined in [ansible/roles/webserver/defaults/main.yml](ansible/roles/webserver/defaults/main.yml) - `127.0.0.1`, `192.168.60.113`
   * request: `curl http://192.168.60.113/jena/fuseki/test/update -X POST --data 'update=PREFIX+foaf%3A+%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0APREFIX+country%3A+%3Chttp%3A%2F%2Feulersharp.sourceforge.net%2F2003%2F03swap%2Fcountries%23%3E%0AINSERT+DATA%0A%7B%0A+country%3Aooo+foaf%3Aname+%22OOOOO%22%40en+.%0A%7D' -H 'Accept: text/plain,*/*;q=0.9'`



# TODO:
* enable [inference](https://jena.apache.org/documentation/inference/)  
