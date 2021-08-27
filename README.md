# CAD Autograder

The CAD autograder is a python program designed to facilitate quick, customizable, and fair grading for CAD drawings in the DXF file format. It requires a user to input a correct CAD file, one or more student
files, and several grading parameters, such as the number of points to take off for errors and how detailed to make the output text. It was created by several undergraduate students 
at Duke University under the supervision of Professor Rabih Younes. It has been deployed on the Duke University virtual machine (VM) servers and can be accessed at this address:

http://vcm-20929.vm.duke.edu/

## Usage
This program can be accessed at:

http://vcm-20929.vm.duke.edu/

Instructions on how to run the program are found on that page.

##File breakdown:
The cad.py file is the python backend to this program. Within the templates folder is index.html which provides the HTML frontend. Inside static/styles is the styles.css which provides the
formatting and presentation for the HTML.

## Local access
The repository can be cloned by typing

```cmd
git clone https://github.com/johnzehr/cad.git
```

This will create a folder called "cad" which contains the repo files. After using the cd command to access the folder,
run this command to install the packages in the requirements.txt file:

```cmd
pip install -r requirements.txt
```
The files in this folder can then be edited locally. 

## Virtual machine access
As mentioned in an earlier section, this web app is running as a "forever process" on the Duke University VM servers. Those with root access to the vcm-20929 server 
can make edits to the code that will be reflected in the web app. The editing process is described below.

1. ssh into the VM using your username (ex: username@vcm-20929.vm.duke.edu) and password.
```cmd
ssh username@vcm-20929.vm.duke.edu
```
2. cd into the finaltest3 folder
```cmd
cd finaltest3
```
3. At this point you will be able to edit the files. The most direct way to do this is by using Vim, the built in Unix text editor. Vim can be initialized by writing "vi" before
the file you wish to edit. For example:
```cmd
vi cad.py
```

Editing in Vim - though the most direct way to modify a file - can be a bit abtruse. Therefore a better alternative could be to edit the repository locally using an IDE 
of your choice then manually transferring the updated files to a folder on the VM using SFTP. A thorough explanation of how to do that can be found here:

https://www.digitalocean.com/community/tutorials/how-to-use-sftp-to-securely-transfer-files-with-a-remote-server

4. Once you have transferred the updated files to the VM, you will likely want to run the updated program as a forever process to ensure that it stays running remotely on the VM.
You will first want to install the forever module with this command. 
```cmd
npm i -g forever
```
Next, kill the existing forever processes (the older version of the Autograder) with this command.

```cmd
sudo forever stopall 
```

Finally, after using cd to enter the folder containing your files, run the new version of the Autograder with this command.
```cmd
forever start -c python3 cad.py
```
Now your updated version is running on the VM server! To look at all existing forever processes, type
```cmd
forever list
```
## NOTE
A brief note about testing. If you clone the Github repo and attempt to run the program, you will notice that you cannot actually get to the HTML page. This is because of the last
line of the cad.py code where host is set to '0.0.0.0':

```python
app.run(host='0.0.0.0', port='80', debug=True)
```
0.0.0.0 means all IPv4 addresses on the local machine and will block connections from the machine you are using. Therefore, you must use the localhost instead and set host to
'127.0.0.1':
```python
app.run(host='127.0.0.1', port='80', debug=True)
```
## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.
