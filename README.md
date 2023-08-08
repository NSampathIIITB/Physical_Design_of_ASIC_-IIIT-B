# Physical_Design_of_ASIC_IIIT-B

This github repository summarises the progress made in the Physical Design of ASIC program. Quick links:

[Day-1](#day-1)

[Day-2](#day-2)

[Acknowledgement](#acknowledgement)

[Reference](#reference)


## Day-1 
<details>
 <summary> Summary </summary>
 
	
I installed all the needed Software tools.

</details>	

<details>
 <summary> Yosys </summary>


 I installed Yosys using the following commands:
 
```
git clone https://github.com/YosysHQ/yosys.git
cd yosys-master 
sudo apt install make 
sudo apt-get install build-essential clang bison flex \
    libreadline-dev gawk tcl-dev libffi-dev git \
    graphviz xdot pkg-config python3 libboost-system-dev \
    libboost-python-dev libboost-filesystem-dev zlib1g-dev
make 
sudo make install

```

Below is the screenshot showing sucessful installation:

![Screenshot from 2023-07-31 18-25-48](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/edbd81f3-dc1f-4618-91b2-b6cbc66876a9)
</details>

 <details>
 <summary> OpenSTA </summary>


 I installed and built OpenSTA (including the needed packages) using the following commands:
 ```
sudo apt-get install cmake clang gcctcl swig bison flex
git clone https://github.com/The-OpenROAD-Project/OpenSTA.git
cd OpenSTA
mkdir build
cd build
cmake ..
make
```
Below is the screenshot showing sucessful installation:

![Screenshot from 2023-07-31 18-52-06](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/45fca339-3b10-4afa-9e49-48c358cc07f1)
</details>

<details>
 <summary> iverilog </summary>


 I installed iverilog using the following command:
  ```
sudo apt-get install iverilog
 ```
 Below is the screenshot showing sucessful installation:

 ![Screenshot from 2023-07-31 18-26-28](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/39cb367f-8681-41db-a1ef-9de239845657)
</details>

<details>
 <summary> gtkwave </summary>


 I installed gtkwave using the following command:
  ```
sudo apt-get install gtkwave
 ```
 Below is the screenshot showing sucessful installation:
![Screenshot from 2023-07-31 18-27-35](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/6fcb06cc-816a-41b4-9e53-b55f9315b92a)
</details>

<details>
 <summary> ngspice </summary>


 I downloaded the tarball from https://sourceforge.net/projects/ngspice/files/ to a local directory and unpacked it using the following commands:
 ```
tar -zxvf ngspice-37.tar.gz
cd ngspice-37
mkdir release
cd release
../configure  --with-x --with-readline=yes --disable-debug
make
sudo make install
 ```
Below is the screenshot showing sucessful installation:

![Screenshot from 2023-07-31 19-00-53](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/4f8b2756-fa2a-4e9a-8a06-1b7a7fdc6d5c)
</details>

<details>
 <summary> OpenLANE </summary>


 I installed gtkwave using the following command:
 
  ```sudo apt-get update
sudo apt-get upgrade
sudo apt install -y build-essential python3 python3-venv python3-pip make git
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io
sudo docker run hello-world
sudo groupadd docker
sudo usermod -aG docker $USER
sudo reboot
 ```
 Below is the screenshot showing sucessful installation:

 ![Screenshot from 2023-07-31 19-33-48](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/82feea18-9b24-4377-83bd-ccafdd2205c5)
 </details>















 ## Acknowledgement
 
- Kunal Ghosh, VSD Corp. Pvt. Ltd.
- Skywater Foundry
- Kanish R,Colleague,IIIT B
- DantuNandini,Senior,IIIT B
- Mariam Rakka

  
## Reference 

- https://github.com/kunalg123
- https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
  
 
 

 
