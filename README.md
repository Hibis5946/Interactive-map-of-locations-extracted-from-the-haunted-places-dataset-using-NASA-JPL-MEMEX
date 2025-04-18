# Interactive-map-of-locations-extracted-from-the-haunted-places-dataset-using-NASA-JPL-MEMEX
This repository exposes how to visualize locations extracted from a dataset using the NASA-JPL-MEMEX GeoParser

# This is ReadMe Update for nasa-jpl-memex/GeoParser
# By Sena London, MS in Applied Data Science Student @ USC
# Spring 2025
# Source: https://github.com/nasa-jpl-memex/GeoParser

# Open a terminal and run
# Since Solr server run with Java version 8, Make sure java8 is running 
sudo update-alternatives --config java
java -version

# Clone the MEMEX GeoParser from the nasa-jpl-memex repository
git clone https://github.com/nasa-jpl-memex/GeoParser.git

## Navigate in the Docker to run the compose-d ##
cd 
cd GeoParser/Docker
docker-compose up -d

# Activate a python virtual environment (venv)
python3 -m venv myenv
source myenv/bin/activate

# Install the required packages and libraries
pip install jupyterlab notebook pandas pysolr requests tqdm

# Create a folder for your dataset, here I choose to do it in the example folder
mkdir /root/GeoParser/examples/haunted_places
You can also do it manually by opening the GeoParser folder and create

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
cd /root/GeoParser/examples/haunted_places

# Optional if want to test covid19 metadata.csv file, 
#but don't need this, you can upload your own haunted file as metadata.cs
./download-metadata.sh 

# Need this
chmod +x create-core-haunted.sh
./create-core-haunted.sh

chmod +x add-fields-haunted.sh
./add-fields-haunted.sh

# Run jupyther in the dataset directory "haunted_places" directory
cd /root/GeoParser/examples/haunted_places
jupyter notebook --allow-root

####
# Open the Django application in your web browser
http://localhost:8000

####
# In the Django web interface
Set Domain Name to haunted_index.
Set Index Path to http://localhost:8983/solr/haunted/
Click on add index
Click add index to store the index of the domain in the database.
Click on Database Icon Tab
Click on GeoParse button, and then wait (takes ~10 minutes)
Click on View button
You have to make sure that you select haunted_index in the index pane


###
# Other helpful commands #
# But not necessary

# Manage Java version
java -version
sudo update-alternatives --config java

# Not needed (compose start it)
# Start Solr
cd
cd GeoParser/Solr/solr-5.3.1
bin/solr start
# Stop Solr
bin/solr stop
#

# wipe the existing core data if run covid data before
curl "http://localhost:8983/solr/admin/cores?action=UNLOAD&core=haunted&deleteIndex=true&deleteDataDir=true&deleteInstanceDir=true"
# And recreate the core
./create-core-haunted.sh

# Then add field and rerun the ingest

#stop the docker
# Cleanest way 
cd ~/GeoParser/Docker
docker-compose down

# Riskier if running other services with other dockers
# Force-stops all running containers on your system, not just related to the GeoParser
docker stop $(docker ps -a -q)

#Remove all containers
docker rm $(docker ps -a -q)


