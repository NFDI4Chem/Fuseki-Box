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

After installation process has finished, visit open refine Fuseki UI at <http://192.168.60.113>

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