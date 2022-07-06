# 2022 GINGER On-Site Training at the University of Cape Town (UCT)
**Dates**: April 1-8, 2022<br/>
**Venue**: Neuroscience Centre, Groote Schuur Hospital, Observatory, Cape Town, South Africa<br/>
**Teaching Fellows**: [Kumar Veerapen, PhD](mkveerapen@gmail.com) and [Carla Marquez-Luna, PhD](mailto:carlamarquezluna@gmail.com)<br/>
[**GINGER Fellows**](https://www.broadinstitute.org/neurogap/2020-2024-cohort)<br/>
[What is GINGER?](https://www.broadinstitute.org/stanley-center-psychiatric-research/neurogap/global-initiative-neuropsychiatric-genetics-education-research-ginger)<br/>


_For this week long on-site training, Carla and Kumar guided the fellows through:_


## Refresher of the [previous on-site training in Kampala, Uganda](https://github.com/atgu/GINGER_cloud)
Lead: Kumar Veerapen
Materials: `slideDeck/GINGER2022_day1_refresher.pdf` [link](https://github.com/mkveerapen/2022_GINGER_UCT/blob/main/slideDeck/GINGER2022_day1_refresher.pdf)

In this section, Kumar covered what Konrad covered in Kampala by running through how to use Google cloud for computing and using Rstudio on a cloud instance. 

The Rstudio on cloud instance did not work and therefore, Kumar and Carla used `R` on the terminal to run through some of the phenotyping exercises found on the last few slides in the materials' slide deck.

If someone out there wants to try, Kumar used the following code block to run Rstudio on the cloud
```
#must provide fellows with the .json file that is available on the Dropbox
#use local on computer R

#set R environment variable
Sys.setenv("GCE_AUTH_FILE" = "PATH-TO/gingeriimak-1f2aeff3dc03.json")

library(googleComputeEngineR)
gce_global_project("gingeriimak")
gce_global_zone("us-central1-b")

#creating a new VM because the old one doesn't have the API permissions, name a new VM with the Rstudio stuff
vm <- gce_vm(template = "rstudio", name = "veerapen-2", username = "veerapen", password ="abc123", predefined_type = "e2-medium")

#copy and paste the external IP address into a Chrome browser as http://<IP>
#give it about 1 minute to warm up before you try?

#kumar needs to create a docker image for this to include R packages but was not done in the end
```

## Introduction to Linux
Lead: Kumar Veerapen
Materials: 

Slide deck: `slideDeck/GINGER2022_day1_linux.pdf` [link](https://github.com/mkveerapen/2022_GINGER_UCT/blob/main/slideDeck/GINGER2022_day1_linux.pdf)

Practice set: `practiceSet/GINGER2022_day1_linux_practice.pdf` [link](https://github.com/mkveerapen/2022_GINGER_UCT/blob/main/practiceSet/GINGER2022_day1_linux_practice.pdf)

Using virtual machines launched by the fellows, the fellows followed up the R exercises with a linux refresher where Kumar introduced Linux again to the fellows. 
We then attempted the linux exercises using the practice set (Thank you, Dan Kinnamon from the University of Miami). 

## Introduction to PLINK 
Lead: Kumar Veerapen
Materials: 

Slide deck: `slideDeck/GINGER2022_day2_plink.pdf` [link](https://github.com/mkveerapen/2022_GINGER_UCT/blob/main/slideDeck/GINGER2022_day2_plink.pdf)

Practice set: `/practiceSet/GINGER2022_day2_plink_practice.pdf` [link](https://github.com/mkveerapen/2022_GINGER_UCT/blob/main/practiceSet/GINGER2022_day2_plink_practice.pdf)

This spanned most of day 2 where we first went through PLINK as an important tool in genetic analyses. 
We then followed this up with running through the practice set together.

Just in case the fellows would like to try out running this using a [Docker image](https://github.com/mkveerapen/2022_GINGER_UCT/tree/main/dockerFile) in this repo, we would suggest using the docker file.

How was the image built:
```
docker build -f Dockerfile .
docker tag a35d7c6bb3f3 us.gcr.io/gingeriimak/ginger-uct:0.1
docker push us.gcr.io/gingeriimak/ginger-uct:0.1
```

Example of how to run in on one of the GINGER VM:

```
sudo apt-get install docker.io
gcloud auth configure-docker
 wget "https://github.com/GoogleCloudPlatform/docker-credential-gcr/releases/download/v2.1.0/docker-credential-gcr_linux_386-2.1.0.tar.gz"

tar -xvzf docker-credential-gcr_linux_386-2.1.0.tar.gz
sudo mv docker-credential-gcr /usr/bin/
sudo chmod +x /usr/bin/docker-credential-gcr

docker-credential-gcr gcr-login
#follow instructions and use Broad email
sudo chmod 666 /var/run/docker.sock

docker pull us.gcr.io/gingeriimak/ginger-uct:0.1 #pull image to you
docker run -it  -v /home/kumar/:/mnt/home us.gcr.io/gingeriimak/ginger-uct:0.1 #mount your local directory to your image
```

## Step-by-step Genome-Wide Association Study (GWAS)
Lead: Carla Marquez-Luna
Materials: 

Slide deck: `slideDeck/GINGER2022_day3-5_GWAS.pdf` [link](https://github.com/mkveerapen/2022_GINGER_UCT/blob/main/slideDeck/GINGER2022_day3-5_GWAS.pdf)

Practice set instructions: `practiceSet/GINGER2022_day3-5_GWAS_practice.pdf` [link](https://github.com/mkveerapen/2022_GINGER_UCT/blob/main/practiceSet/GINGER2022_day3-5_GWAS_practice.pdf) 

Practice set data using 1000 genomes (following Kumar's data structure) [link](https://www.dropbox.com/sh/1soglilyfj0y2u0/AACrXL2wUNoUIyoA72m27NIda?dl=0)


We first introduced the fellows to what is a GWAS. Then we did a refresher of PLINK and some basic commands. Carla also mentioned that it would be important to keep both PLINK 1.9 and 2.0 because some historical commands like sex check and using non-binary plink files are only available in the older 1.9 version.
Carla went through all steps in GWAS by going through sections in the slide deck, followed by the corresponding section in the practice set (PCA in slide deck to then PCA practice set).
The final goal was to get the fellows to obtain a Manhattan and a QQ plot.
All of this was run on a local machine because we wanted the fellows to learn how to run a GWAS without worrying about running it on a VM since Rstudio was not working as well as we wanted it to. We passed the practice set data around to the fellows using a flash drive.
