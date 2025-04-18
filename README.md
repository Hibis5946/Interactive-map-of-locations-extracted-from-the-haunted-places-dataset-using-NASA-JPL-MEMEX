# Interactive-map-of-locations-extracted-from-the-haunted-places-dataset-using-NASA-JPL-MEMEX
This repository exposes how to visualize locations extracted from a dataset using the NASA-JPL-MEMEX GeoParser

<br>This is ReadMe Update for nasa-jpl-memex/GeoParser
<br> By Sena London, MS in Applied Data Science Student @ USC
<br>Spring 2025
<br>Source: https://github.com/nasa-jpl-memex/GeoParser

# Open a terminal and run
<br>Since Solr server run with Java version 8, Make sure java8 is running 
<br>sudo update-alternatives --config java
<br>java -version

# Clone the MEMEX GeoParser from the nasa-jpl-memex repository
<br>git clone https://github.com/nasa-jpl-memex/GeoParser.git

## Navigate in the Docker to run the compose-d ##
<br>cd 
<br>cd GeoParser/Docker
<br>docker-compose up -d

# Activate a python virtual environment (venv)
<br>python3 -m venv myenv
<br>source myenv/bin/activate

# Install the required packages and libraries
<br> pip install jupyterlab notebook pandas pysolr requests tqdm

# Create a folder for your dataset, here I choose to do it in the example folder
<br>mkdir /root/GeoParser/examples/haunted_places
<br>You can also do it manually by opening the GeoParser folder and create

# Copy manually the following files, from the covid19 folder and paste in the dataset folder (haunted_places)
- create-core.sh
- add-fields.sh
- Ingest COVID data

# Modify the previous file to match your folder name or how you want
- Open the files and change covid19 to haunted
- You can personalize the filename to your dataset
- Change the core name from Covid19 to Haunted or personalize name
- Personalize "Ingest COVID data" to your dataset name and column 

# Copy manually your dataset.csv to the dataset folder (haunted_places)

# Now go to the terminal and run
<br>cd /root/GeoParser/examples/haunted_places

# Optional if want to test covid19 metadata.csv file, 
<br>but don't need this, you can upload your own haunted file as metadata.cs
<br>./download-metadata.sh 

# Need this
<br>chmod +x create-core-haunted.sh
<br>./create-core-haunted.sh

<br>chmod +x add-fields-haunted.sh
<br>./add-fields-haunted.sh

# Run jupyther in the dataset directory "haunted_places" directory
<br>cd /root/GeoParser/examples/haunted_places
<br>jupyter notebook --allow-root

####
# Open the Django application in your web browser
<br>http://localhost:8000

####
# In the Django web interface
<br>Set Domain Name to haunted_index.
<br>Set Index Path to http://localhost:8983/solr/haunted/
<br>Click on add index
<br>Click add index to store the index of the domain in the database.
<br>Click on Database Icon Tab
<br>Click on GeoParse button, and then wait (takes ~10 minutes)
<br>Click on View button
<br>You have to make sure that you select haunted_index in the index pane


###
# Other helpful commands #
<br>But not necessary

- Manage Java version
<br>java -version
<br>sudo update-alternatives --config java

# Not needed (compose start it)
- Start Solr
<br>cd
<br>cd GeoParser/Solr/solr-5.3.1
<br>bin/solr start
- Stop Solr
<br>bin/solr stop
#

# wipe the existing core data if run covid data before
<br>curl "http://localhost:8983/solr/admin/cores?action=UNLOAD&core=haunted&deleteIndex=true&deleteDataDir=true&deleteInstanceDir=true"
# And recreate the core
<br>./create-core-haunted.sh

# Then add field and rerun the ingest

- stop the docker
<br>Cleanest way 
<br>cd ~/GeoParser/Docker
<br>docker-compose down

# Riskier if running other services with other dockers
<br>Force-stops all running containers on your system, not just related to the GeoParser
<br>docker stop $(docker ps -a -q)

- Remove all containers
<br>docker rm $(docker ps -a -q)


