# private_gpt_docker_image
An attempt to create a docker image for the privateGPT, which works on linux cpu and gpu machine.

## Some Info
1. The container images with 'gpu' string in its name are for leveraging the gpu on the host machine, otherwise the image is for cpu only.
2. This image is built by simply entering into the ubuntu:latest image and then installing the private_gpt as mentioned on its repo, and then commiting the changes to a new image.
3. Dockerfile for building the image will be available in future.
4. These images are only for linux machines, you can try on other os on your own.

## Instructions to get it running
### Assumptions:
I am asumming that you are working on a linux machine and have docker configured on it also you should be familiar with docker for better experience.

### Step to run it.
1. First download the model(ggml-gpt4all-j-v1.3-groovy.bin) image used in this contianer from this link https://gpt4all.io/models/ggml-gpt4all-j-v1.3-groovy.bin
2. Save the model in directory of your choice on local pc, i am assuming that it is saved in '~/models/' directory.
3. Pull the docker image by using command
   ```docker pull ghcr.io/logicalbhanu/private_gpt:latest```
4. Put all your documents over which you want the private_gpt to be queried in a directory of your choice, i am assuming this directory as '~/source_documents'.
5. Run the image in the interactive mode with the below command
   ```docker run -it --name my_private_gpt -v ~/models/:/root/privateGPT/models -v ~/source_documents/:/root/privateGPT/source_documents private_gpt:latest /bin/bash```
6. Once entered into the docker, run the command to enter into the privateGPT directory as follows
   ```cd /root/privateGPT```
7. Run command inisde the docker to process the documents you have in source_documents directory as follows
   ```python ingest.py```
8. After this you are at the position to start the private_gpt prompt to ask your queries from the documents, use this command for that
   ```python privateGPT.py```

### Steps to exit
1. type ```exit``` to exit from private_gpt prompt, then type ```exit``` to exit from the container itself.

**Note**
At present, every time you start the container you have to go through all the steps mentioned in the **steps to run it** heading, in future i will try to create a script to automate this, also after exiting from the docker you will need to remove the container via the command ```docker rm -f my_private_gpt`` to use the name again otherwise change the name when running the contianer again(not recommended as it will take extra disk space).

