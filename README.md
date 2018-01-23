# Microsoft Azure Machine Learning Service
Microsoft China 0 Bejing hackfest ppt and demo repository

## Azure workbench
### Setup instruction
Deploy ML Expriment and install Workbench
[Create Azure Machine Learning Preview accounts and install Azure Machine Learning Workbench](https://docs.microsoft.com/en-us/azure/machine-learning/preview/quickstart-installation)

### local execution
- Nothing to prepare, just run on Workbench or CLI
```
az ml experiment submit -c local tf_mnist.py
```

### remote execution
[Configuring Azure Machine Learning Experimentation Service](https://docs.microsoft.com/en-us/azure/machine-learning/preview/experimentation-service-configuration)

- deploy linux DSVM on Azure
```
az ml computetarget attach remotedocker --name gpu-vm1 --address 52.226.18.127 --username konan94 --password yourpassword
```

- change .compute definition file, add definition
```
baseDockerImage: microsoft/mmlspark:plus-gpu-0.9.9
nvidiaDocker: true
```

- prepare remote docker
```
az ml experiment prepare -c gpu-vm1
```
- execute GPU training
```
az ml experiment submit -c gpu-vm1 tf_mnist.py
```

- multiple DSVM execution
```
az ml computetarget attach remotedocker --name gpu-vm2 --address 40.79.67.1 --username konan94 --password yourpassword
az ml experiment prepare -c gpu-vm2
az ml experiment submit -c gpu-vm2 tf_mnist.py
```

EOF