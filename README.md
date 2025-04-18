# Interactive-map-of-locations-extracted-from-the-haunted-places-dataset-using-NASA-JPL-MEMEX
This repository exposes how to visualize locations extracted from a dataset using the NASA-JPL-MEMEX GeoParser

<br> By Sena London, MS in Applied Data Science Student @ USC
<br>Spring 2025
<br>Source:
<br>https://github.com/nasa-jpl-memex/GeoParser
<br>https://www.kaggle.com/datasets/sujaykapadnis/haunted-places

# Open a terminal and run
Since Solr server run with Java version 8, Make sure java8 is running 
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

# Run jupyther in the dataset directory "haunted_places"
<br>cd /root/GeoParser/examples/haunted_places
<br>jupyter notebook --allow-root
<br>run the ingest_haunted_data jupiter files
![image (3)](https://github.com/user-attachments/assets/34f4f053-2082-4c12-9f72-27cf52577e30)

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
![image (1)](https://github.com/user-attachments/assets/d182a4b7-2c9a-4227-89ae-a5e3d19709c2)
<br>You have to make sure that you select haunted_index in the index pane
<br>
<br>Output Sample
![haunted_places_map](https://github.com/user-attachments/assets/2572be23-c1cc-4207-8bb6-d353ef2ae999)

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

# wipe the existing core data if run covid data before
curl "http://localhost:8983/solr/admin/cores?action=UNLOAD&core=haunted&deleteIndex=true&deleteDataDir=true&deleteInstanceDir=true"
# And recreate the core
./create-core-haunted.sh

# Then add field and rerun the ingest
- stop the docker
<br>Cleanest way 
<br>cd ~/GeoParser/Docker
<br>docker-compose down

# Riskier if running other services with other dockers
- Force-stops all running containers on your system, not just related to the GeoParser
<br>docker stop $(docker ps -a -q)

- Remove all containers
<br>docker rm $(docker ps -a -q)


