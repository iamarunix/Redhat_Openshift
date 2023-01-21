# Managing Images

In this use case, we will understand how the normal image is used and after adding few functionalities, how to use it as updated image for current and other projects.

##  Step 1  Pull the Nginx image from quay.io registry
```
$ podman pull quay.io/redhattraining/nginx:1.17

```

## Step 1.2  Ensure image is available in your local server
```
$ podman images
```
## Step 1.3  Create the container using the downloaded image with port mapping 8080 for localhost and 80 for container
```
$ podman run --name con_1 -dp 8080:80 quay.io/redhattraining/nginx:1.17
```
## Step 1.4  Login to the container
```
$ podman exec -it con_1 /bin/bash
```
## Step 1.5  Update the index.html with some content
```
root@b9d5739af239/:$ echo 'This is use case 3' > /usr/share/nginx/html/index.html
```
## Step 1.6  Get out of the "con_1" container
```
root@b9d5739af239:/$ exit 
```
## Step 1.7  Check the output of "con_1" container webserver
```
$ curl 127.0.0.1:8080
This is use case 3
```
## Step 1.8  Stop the container 
```
$ podman stop con_1
```
## Step 1.9  Take the backup of the "con_1" container in the name of "myimage_1.1" image in the localhost
```
$ podman commit -a <author Name> <current_container_name> <new_current_image_name>>
$ podman commit -a arun con_1 myimage_1.1
```
## Step 1.10  Check the current images
```
$ podman images
```
## Step 2.1  Now, run the container from the new image "myimage_1.1"  
```
$ podman run --name con_2 -dp 8080:80 myimage1.1 
```
## Step 2.2  
```
$ podman exec -it con_2 /bin/bash
```
## Step 2.3  Update the index.html with some content in the "con_2" container
```
root@cfa21f02a77d:/# echo 'This is the output from con_2' > /usr/share/nginx/html/index.html
```
## Step 2.4  Get out of the "con_2" container
```
root@cfa21f02a77d:/# exit
```
## Step 2.5  Check the output of "con_2" container webserver
```
$ curl 127.0.0.1:8080
This is the output from con_2
```
## Step 2.6  Stop the "con_2" container
```
$ podman stop con_2
```
## Step 2.7  Take the backup of the "con_2" container in the name of "myimage_1.2" image in the localhost
```
$ podman commit -a <author Name> <current_container_name> <new_current_image_name>
$ podman commnit -a arun con_2 image_1.2
```
## Step 2.8  Check the available images
```
$ podman images 
```
## Step 2.9  Delete the image_1.1 from the localhost
```
$ podman rm image_1.1
```
