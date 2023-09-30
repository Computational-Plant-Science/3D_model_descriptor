# 3D_model_descriptor

Building a 3D root Descriptor:

To encode the maize root structure variation in genotype and interaction with environment using Quaternion representation of maize root Structure




Example of 3D maize root structure v.s. Visualization of Quaternion rotation vectors

![Optional Text](../master/media/example.png)



Example of 3D root Descriptor to enocde genotype varition of a test panel of field-grown maize root samples

![Test data](../master/media/example_12_genotypes.png)

![Descriptor result](../master/media/12_genotype_composition.gif)



Summary of our 3D root Descriptor pipeline

![3D Descriptor pipeline](../master/media/pipeline.png)




## Input


Skeleton/structure of 3D root models(A Graph with edges and nodes) of M samples with N different treatment/genotypes 

Graph representation of a 3D root Skeleton/structure (*.ply) in Polygon File Format or the Stanford Triangle Format. 

Computed from [Computational-Plant-Science / 3D_model_traits_demo](https://github.com/Computational-Plant-Science/3D_model_traits_demo) 



## Output

1. Computed quaternion values in 3 different definitions

	(Average, Composition Differential of quaternion values of all paths from the root stem tip nodes)

2. Cluster center of N quaternion values of different treatment/genotypes using all M samples 

	Transformation matrixes between each pair of different treatment/genotypes in total N different treatment/genotypes 

	Number of transformation matrixes = N!2!(N − 2)!  (combinations without repeat, order does not matter)

3. Mahalanobis Distance between each pairs of different treatment/genotypes in total N different treatment/genotypes.  
	
	Same number as “Number of transformation”

4. The rotation angles between each pairs of different treatment/genotypes were computed from Transformation matrix.

5. The transformation distance between each pairs of different treatment/genotypes can be computed from Transformation matrix.

6. Statical analysis of correlation between rotation angles with Genotype and Environment.    	G*E  


![3D descriptor alogrithm design](../master/media/Alogrithm.png)








## Requirements

[Docker](https://www.docker.com/) is required to run this project in a Linux environment.

Install Docker Engine (https://docs.docker.com/engine/install/)



## Usage


We suggest to run the pipeline inside a docker container, 

The Docker container allows you to package up your application(s) and deliver them to the cloud without any dependencies. It is a portable computing environment. It contains everything an application needs to run, from binaries to dependencies to configuration files.


There are two ways to run the pipeline inside a docker container, 

One was is to build a docker based on the docker recipe file inside the GitHub repository. In our case, please follow step 1 and step 3. 

Antoher way is to download prebuild docker image directly from Docker hub. In our case, please follow step 2 and step 3. 


1. Build docker image on your PC under linux environment
```shell

git clone https://github.com/Computational-Plant-Science/3D_model_descriptor.git

docker build -t 3D_model_descriptor -f Dockerfile .
```
2. Download prebuild docker image directly from Docker hub, without building docker image on your local PC 
```shell
docker pull computationalplantscience/3D_model_descriptor
```
3. Run the pipeline inside the docker container 

link your test 3D model path (e.g. '/home/test/test.ply', $path_to_your_3D_model = /home/test, $your_3D_model_name.ply = test.ply)to the /srv/test/ path inside the docker container
 ```shell
docker run -v /$path_to_your_3D_model:/srv/test -it 3D_model_descriptor

or 

docker run -v /$path_to_your_3D_model:/srv/test -it computationalplantscience/3D_model_descriptor

```

4. Run the pipeline inside the container
```shell
python3 pipeline.py -p /srv/test/ -m $your_3D_model_structure_file_name.ply

```
  


# Author
Suxing Liu (suxingliu@gmail.com), Alexander Bucksch (bucksch@arizona.edu)


## Other contributions

Docker container was maintained and deployed to [PlantIT](https://portnoy.cyverse.org) by Wes Bonelli (wbonelli@uga.edu).
