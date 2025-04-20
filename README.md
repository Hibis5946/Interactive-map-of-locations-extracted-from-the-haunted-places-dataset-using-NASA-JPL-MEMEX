# Interactive-map-of-locations-extracted-from-the-haunted-places-dataset-using-NASA-JPL-MEMEX
This repository exposes how to visualize locations extracted from a dataset using the NASA-JPL-MEMEX GeoParser

<br> By Sena London, MS in Applied Data Science Student @ USC
<br>Spring 2025
<br>Source:
<br>https://github.com/nasa-jpl-memex/GeoParser
<br>https://www.kaggle.com/datasets/sujaykapadnis/haunted-places

# Open a terminal and run
- Since Solr server run with Java version 8, Make sure java8 is running :
<br>sudo update-alternatives --config java
<br>java -version

# Clone the MEMEX GeoParser from the nasa-jpl-memex repository
git clone https://github.com/nasa-jpl-memex/GeoParser.git

# Clone the Haunted_places cleaned metadata, the associated core files and script
git clone https://github.com/Hibis5946/Interactive-map-of-locations-extracted-from-the-haunted-places-dataset-using-NASA-JPL-MEMEX.git
<br>Haunted_places file: coming soon

# Move the Haunted_places file into the following directory:
GeoParser/examples/

## Navigate into the Docker directory and run:
cd 
<br>cd GeoParser/Docker
<br>docker-compose up -d

# Activate a python virtual environment (venv)
python3 -m venv myenv
<br>source myenv/bin/activate

# Install the required packages and libraries
pip install jupyterlab notebook pandas pysolr requests tqdm

# Navigate into the dataset (haunted_places) directory 
cd /root/GeoParser/examples/haunted_places

# Activate cores in thge dataset (haunted_places) directory
chmod +x create-core-haunted.sh
<br>./create-core-haunted.sh
<br>chmod +x add-fields-haunted.sh
<br>./add-fields-haunted.sh

# Run jupyther in the same directory "haunted_places"
jupyter notebook --allow-root
<br>run the ingest_haunted_data jupiter files
![image (3)](https://github.com/user-attachments/assets/34f4f053-2082-4c12-9f72-27cf52577e30)

####
# Open the Django application in your web browser
http://localhost:8000

####
# In the Django web interface
Set Domain Name to haunted_index.
<br>Set Index Path to http://localhost:8983/solr/haunted/
<br>Click on add index
<br>Click add index to store the index of the domain in the database.
<br>Click on Database Icon Tab
<br>Click on GeoParse button, and then wait (takes some minutes)
<br>Click on View button
![image (1)](https://github.com/user-attachments/assets/d182a4b7-2c9a-4227-89ae-a5e3d19709c2)
You have to make sure that you select haunted_index in the index pane
<br>
<br>Output Sample
![haunted_places_map](https://github.com/user-attachments/assets/2572be23-c1cc-4207-8bb6-d353ef2ae999)

<br>
# Using your own dataset
# Create a folder for your dataset, 
mkdir /root/GeoParser/examples/dataset_name
<br>You can also do it manually by opening the GeoParser folder and create

# Copy manually the following files, and paste in the newly dataset folder
- create-haunted-core.sh
- add-haunted-fields.sh
- Ingest-haunted-data
# Copy manually your dataset.csv to the dataset folder 

# Modify the previous core, ingest files to match your current dataset schema
Open the cores and script file and change haunted and the dataset name into your own dataset name

#
# Other helpful commands #
- Manage Java version:
<br>java -version
<br>sudo update-alternatives --config java
# Not needed (compose start it)
- Start Solr:
<br>cd
<br>cd GeoParser/Solr/solr-5.3.1
<br>bin/solr start
- Stop Solr:
<br>bin/solr stop

# Wipe the existing core data if run covid data before
curl "http://localhost:8983/solr/admin/cores?action=UNLOAD&core=haunted&deleteIndex=true&deleteDataDir=true&deleteInstanceDir=true"
# Recreate the core
./create-core-haunted.sh

# Add field and rerun the ingest
<br>./create-core-haunted.sh
<br>./add-fields-haunted.sh

# Stop the docker
Cleanest way:
<br>cd GeoParser/Docker
<br>docker-compose down
<br>
<br>Riskier if running other services with other dockers:
<br>Force-stops all running containers on your system, not just related to the GeoParser:
<br>docker stop $(docker ps -a -q)
<br>Remove all containers:
<br>docker rm $(docker ps -a -q)


